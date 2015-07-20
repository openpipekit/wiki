# Open Pipe Kit Developer Reference 

## Standards
### Package
A package is a repository that contains Command Line Interfaces (CLI) for a device (which has a sensor) or a database.
- A `pull` command for a device with a sensor.
- A `push` command for a database.
- An `install` command if needed.
- Each command must have a `--help` option and output must follow [docopt standard](http://docopt.org/). This is important for both being friendly to your neighbors and compatibility with tools like the Open Pipe Kit Bakery.
- Optionally prefix your package's name with `opk-cli--` so friends can find it.

### pull commands
- Issuing a pull command will print a value on a new line and then exit.

### push commands
- Accepts input over a `--value=<value>` option or over STDIN (`echo "42" | ./database-cli/push`) and then exits. 
- When the database requires a schema and at least one field name, use the `--field_name=<field_name>` option. To keep thing simple for now, we take a schemaless approach. See experimental specifications below for schema based approaches.

__Example__
```
# Get the opk-cli--yoctopuce-temperature package
wget  -O opk-cli--yoctopuce-temperature.tar.gz https://github.com/openpipekit/opk-cli--yoctopuce-temperature/archive/0.1.0.tar.gz
mkdir opk-cli--yoctopuce-temperature
tar xzf opk-cli--yoctopuce-temperature.tar.gz --strip-components=1 -C opk-cli--yoctopuce-temperature

# Get the opk-cli--phant package 
wget  -O opk-cli--phant.tar.gz https://github.com/openpipekit/opk-cli--phant/archive/0.5.0.tar.gz
mkdir opk-cli--phant
tar xzf opk-cli--phant.tar.gz --strip-components=1 -C opk-cli--phant
# Install it
./opk-cli--phant/install

# Start the pipe running every 60 seconds 
watch -n60 "./opk-cli--yoctopuce-temperature/pull  | ./opk-cli--phant/push  --public_key <public_key> --private_key <private_key> --url <url> --field_name <field_name>"
```

## Experimental 
### pull commands
- A `--format` options where values may be csv or json for when a pull might return values from multiple sensors.
- A `--timestamp` option. When this option is used, it must also be used in conjunction with the `--format` option.
- An optional `--stream=<resolution>` option for event oriented sensors that don't exit after one value is returned. A new line is delimiter of seperate readings. 

### push commands
- Support for streams delimited by new lines in the case of an event oriented sensor.
- For databases that maintain structured data and the sensor returns multiple values, a `--format` options where values may be csv or json for when a pull might return values from multiple sensors.







