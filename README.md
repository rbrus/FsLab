FsLab
=====

FsLab is a curated set of templates, libraries and literate scripting support for doing
data science with F#.

See https://fslab.org for getting started

Developer notes
---------------

### Project structure

The project produces three things:

 1. **FsLab** A NuGet package containing the `FsLab.fsx` load script for a consistent set of packages, plus some extra formatters
 2. **FsLab.Templates** Templates for 'dotnet new' and Visual Studio. Each template includes an FsLab build script and F5 launcher for processing the literate scripts into reports.
 3. **FSharp.Literate.Scripts** Used by FsLab build scripts to process F# literate scripts into HTML and LaTex

The source files in the repository are organized as follows:

| Directory or file  | Comment
|--------------------|---------------
| `misc`             | Icons and other non-source-code things
| `src/FSharp.Literate.Scripts` | Source for the DLL in the `FSharp.Literate.Scripts` NuGet package
| `src/Html`         | HTML formatters for literate scripts not included in other packages
| `src/Text`         | Text formatters for literate scripts not included in other packages
| `src/Shared`       | Styling and server support for literate scripts not included in other packages
| `src/experiments`  | Item templates
| `src/journal`      | Journal project template
| `src/dotnet-templates` | Extra files for 'dotnet new' template support
| `src/vs-templates` | Extra files for Visual Studio template support
| `src/FsLab.fsx`    | Script included in the `FsLab` NuGet package
| `src/*.nuspec`     | NuGet files for building the packages
| `build.fsx`        | FAKE script that does all the magic (below)

### Building FsLab

If you want to be able to build FsLab Journal template, you'll need Visual Studio 2017 SDK.
To update one or more dependencies, use the following steps:

* Run `build Clean` to make sure that there are only source files around
* Run `.paket/paket.exe update` to update the dependencies
* Run `build` to build everything or `build NuGet` to build everything except for
  the FsLab Journal template (useful if you don't have the SDK installed)
* Add new line with version information to `RELEASE_NOTES.md`!
* Run `publish` from command line to upload NuGet package (if you have the rights)

After running `build NuGet` for the first time, you can also edit the
extensions in `src/FsLab.fsx`. 

If there were any changes in the Journal template, you also need to update the
[journal template](https://github.com/fslaborg/journal/tree/journal) in the
[journal](https://github.com/fslaborg/journal) repository. At some
point, these should be generated automatically too!
