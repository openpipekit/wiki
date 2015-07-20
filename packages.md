# Open Pipe Kit Packages
An Open Pipe Kit Package is a bundle of software that follows the [OPK Specification for Command Line Interfaces](opk-specification) with a package.json file that describes the CLIs contained in the package and the options associated with using those CLIs.   


## package.json

```
{
  "name": "opk-cli--example-package"
  "cli": {
    "push": { 
      "public_key": "String",
      "private_key": "String",
      "url": "String"
    },
    "install": {}
  }
}
```

```
[
  {
    "command": "push",
    "options": {
      "public_key": "String",
      "private_key": "String",
      "url": "String"
    }
  },
  {
    "command": "install",
    "options": {}
  }
]
```
