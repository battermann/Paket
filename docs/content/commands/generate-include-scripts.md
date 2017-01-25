## Generating include scripts for all NuGet packages

It is possible to generate include scripts for all registered NuGet packages defined in the [`paket.dependencies` file](dependencies-file.html).

    [lang=batchfile]
    $ paket generate-include-scripts framework net45

This will create .csx and .fsx scripts under `paket-files/include-scripts/net45/`, those files can now be 
used in your scripts without having to bother with the list and order of all dependencies for given package.

Note: this command only works after packages have been restored, please call `paket restore` before using `paket generate-include-scripts` or `paket install` if you just changed your `paket.dependencies` file.

## Sample

Consider the following [`paket.dependencies` file](dependencies-file.html):

    [lang=paket]
    source https://nuget.org/api/v2

    nuget FsLab

Now we run `paket install` to install the packages.

Then we run `paket generate-include-scripts framework net45` to generate include scripts.

In a .fsx script file you can now use
    
    [lang=fsharp]
    
    #load @"paket-files/include-scripts/net45/include.fslab.fsx"

    // now ready to use FsLab and any of it's dependencies

You'll see messages when you execute the `#load` line in FSI:

    Loaded deedle
    Loaded deedle.rplugin
    Loaded dynamicinterop
    Loaded foogle.charts
    Loaded fsharp.charting
    Loaded zlib.portable
    Loaded fsharp.data
    Loaded google.datatable.net.wrapper
    Loaded taskparallellibrary
    Loaded mathnet.numerics
    Loaded mathnet.numerics.fsharp
    Loaded newtonsoft.json
    Loaded r.net.community
    Loaded r.net.community.fsharp
    Loaded rprovider
    Loaded xplot.googlecharts
    Loaded xplot.googlecharts.deedle
    Loaded http.fs
    Loaded xplot.plotly
    Loaded fslab
    
## Generate include scripts while installing packages

Alternatively, the include scripts can be generated automatically when running the `paket install` command.

To enable this, add the `generate_load_scripts` option to the `paket.dependencies` file:

    [lang=paket]
    generate_load_scripts: true
    source https://nuget.org/api/v2

    nuget Suave
    
