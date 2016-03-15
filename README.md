SublimeLinter-javac
=========================

[![Build Status](https://travis-ci.org/SublimeLinter/SublimeLinter-javac.svg?branch=master)](https://travis-ci.org/SublimeLinter/SublimeLinter-javac)

This linter plugin for [SublimeLinter](http://sublimelinter.readthedocs.org) provides an interface to [javac](http://docs.oracle.com/javase/6/docs/technotes/tools/solaris/javac.html). It will be used with files that have the “Java” syntax.

##### IMPORTANT!
Please note that because `javac` requires a complete directory context in order to work, this linter plugin currently will only lint a file **when it has been saved**. As soon as you modify the file, all linter marks will be cleared.

## Installation
SublimeLinter 3 must be installed in order to use this plugin. If SublimeLinter 3 is not installed, please follow the instructions [here](http://sublimelinter.readthedocs.org/en/latest/installation.html).

### Linter installation
Before using this plugin, you must ensure that `javac` is installed on your system. `javac` is part of the `java` developer SDK, which can be downloaded [here](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

**NOTE:** This plugin currently supports only JDK 1.7+.

### Linter configuration
In order for `javac` to be executed by SublimeLinter, you must ensure that its path is available to SublimeLinter. Before going any further, please read and follow the steps in [“Finding a linter executable”](http://sublimelinter.readthedocs.org/en/latest/troubleshooting.html#finding-a-linter-executable) through “Validating your PATH” in the documentation.

Once `javac` is installed and configured, you can proceed to install the SublimeLinter-javac plugin if it is not yet installed.

### Plugin installation
Please use [Package Control](https://sublime.wbond.net/installation) to install the linter plugin. This will ensure that the plugin will be updated when new versions are available. If you want to install from source so you can modify the source code, you probably know what you are doing so we won’t cover that here.

To install via Package Control, do the following:

1. Within Sublime Text, bring up the [Command Palette](http://docs.sublimetext.info/en/sublime-text-3/extensibility/command_palette.html) and type `install`. Among the commands you should see `Package Control: Install Package`. If that command is not highlighted, use the keyboard or mouse to select it. There will be a pause of a few seconds while Package Control fetches the list of available plugins.

1. When the plugin list appears, type `javac`. Among the entries you should see `SublimeLinter-javac`. If that entry is not highlighted, use the keyboard or mouse to select it.

## Settings
For general information on how SublimeLinter works with settings, please see [Settings](http://sublimelinter.readthedocs.org/en/latest/settings.html). For information on generic linter settings, please see [Linter Settings](http://sublimelinter.readthedocs.org/en/latest/linter_settings.html).

In addition to the standard SublimeLinter settings, SublimeLinter-javac provides its own setting, which may also be used as an [inline setting](http://sublimelinter.readthedocs.org/en/latest/settings.html#inline-settings).

|Setting|Description|
|:------|:----------|
|lint|A comma-delimited list of rules to apply.|

Valid rule names are: all, cast, classfile, deprecation, dep-ann, divzero, empty, fallthrough, finally, options, overrides, path, processing, rawtypes, serial, static, try, unchecked, varargs, -cast, -classfile, -deprecation, -dep-ann, -divzero, -empty, -fallthrough, -finally, -options, -overrides, -path, -processing, -rawtypes, -serial, -static, -try, -unchecked, -varargs, none.

For example, to ignore deprecation warnings for all files in a project, you would add this to the linter settings:

```
"javac": {
    "lint": "all,-deprecation"
}
```

To change the settings in the same way for a single file, you would put this comment on the first or second line of the file:

```
// [SublimeLinter javac-lint:all,-deprecation]
```

### Passing options to `javac`

In order to configure `javac` options like the class path, source path, or file encoding,
the `args` setting can be used.

|Setting|Description|
|:------|:----------|
|`args`|An array of strings, alternating between an option and the corresponding value.|

A full list of available options is given [here][1].

For example, the following configuration defines the source file encoding,
includes the two libraries `lib/some_lib.jar` and `lib/some_other_lib.jar`
in the classpath,
and defines `src/` as the project's source path:

```
"args": [
    "-encoding", "UTF8",
    "-cp", "${project}/lib/some_lib.jar:${project}/lib/some_other_lib.jar",
    "-sourcepath", "${project}/src/"
]
```

Note that options and their values must be separate elements in the array
(i.e. `"args": ["-sourcepath", "/path/to/src"]` does work, while
`"args": ["-sourcepath /path/to/src"]` does not work).

See the [general SublimeLinter documentation on Settings][2] for how to
incorporate this setting into your SublimeLinter configuration.

#### Project-specific options

Settings like the class path often only apply to one specific project.
The general SublimeLinter documentation also [explains][3] how to specify
project-specific settings in the `sublime-project` file.

For the example above, such a project file could look like this:
```
{
    "folders":
    [
        {
            "path": "."
        }
    ],
    "SublimeLinter":
    {
        "linters":
        {
            "javac": {
                "lint": "all",
                "args": [
                    "-encoding", "UTF8",
                     "-cp", "${project}/lib/some_lib.jar:${project}/lib/some_other_lib.jar",
                    "-sourcepath", "${project}/src/"
                ]
            }
        }
    }
}
```

## Contributing
If you would like to contribute enhancements or fixes, please do the following:

1. Fork the plugin repository.
1. Hack on a separate topic branch created from the latest `master`.
1. Commit and push the topic branch.
1. Make a pull request.
1. Be patient.  ;-)

Please note that modications should follow these coding guidelines:

- Indent is 4 spaces.
- Code should pass flake8 and pep257 linters.
- Vertical whitespace helps readability, don’t be afraid to use it.
- Please use descriptive variable names, no abbrevations unless they are very well known.

Thank you for helping out!

[1]:http://docs.oracle.com/javase/7/docs/technotes/tools/windows/javac.html
[2]:http://sublimelinter.readthedocs.org/en/latest/settings.html#settings
[3]:http://sublimelinter.readthedocs.org/en/latest/settings.html#project-settings
