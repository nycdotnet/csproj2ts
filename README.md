﻿# csproj2ts

Queries a Visual Studio project file (.csproj or .vbproj) for TypeScript configuration information.  Will also find default config in a `Microsoft.TypeScript.Default.props` file, if referenced by the project.

Tested with project configuration settings in TypeScript 1.4.

## Install

To install, run `npm install csproj2ts`.  Current version v0.0.2.

This module only *collects* the information.  What you do with it after is up to you.

## Example Usage:
```javascript

    var csproj2ts = require('csproj2ts');
    
    var vsProjInfo = {
        ProjectFileName: "path/to/my/project.csproj", // the name and path to the project file
        ActiveConfiguration: "Release"                // the MSBuild config to query
    }

    csproj2ts.getTypeScriptSettings(vsProjInfo).then(function (settings) {
        console.log(settings.files);          // will output the array of files
        console.log(settings.RemoveComments); // will output true or false.
        console.log(settings.OutDir);         // will output the OutDir string or undefined.
        console.log(settings);                // will output all identified configuration.
    });

```

## Developing:

You have to run `npm install` to fetch dependencies prior to developing or testing csproj2ts.

To build, run `grunt`.

To build and run tests with nodeunit, run `grunt test`.

To build, run tests, and launch the demo script, run `grunt demo`.  (You can also run `node demo.js` directly (assumes `csproj2ts.csproj` in current folder).)


## API:

The returned settings object has the following documented properties:

  * files: string[] - This is an array of the files that will be compiled.
  * VSProjectDetails - This object has the following properties:
    * ProjectFileName: string
    * MSBuildExtensionsPath32: string
    * VisualStudioVersion: string
    * TypeScriptVersion: string
    * ActiveConfiguration: string
    * DefaultProjectConfiguration?: string;
    * DefaultVisualStudioVersion?: string;
    * TypeScriptDefaultPropsFilePath: string;
    * TypeScriptDefaultConfiguration: - this property has the settings (seen below) that correspond to the defaults on the referenced .props file.


The returned settings object has the following properties that correspond to TypeScript configuration settings:

  * AdditionalFlags?: string;
  * Charset?: string;
  * CodePage?: string;
  * CompileOnSaveEnabled?: boolean;
  * EmitBOM?: boolean;
  * GeneratesDeclarations?: boolean;
  * MapRoot?: string;
  * ModuleKind?: string;
  * NoEmitOnError?: boolean;
  * NoImplicitAny?: boolean;
  * NoLib?: boolean;
  * NoResolve?: boolean;
  * OutFile?: string;
  * OutDir?: string;
  * PreserveConstEnums?: boolean;
  * RemoveComments?: boolean;
  * SourceMap?: boolean;
  * SourceRoot?: string;
  * SuppressImplicitAnyIndexErrors?: boolean;
  * Target?: string;
