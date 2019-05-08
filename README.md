# AIBECS Demo

This repository contains a Jupyter notebook to beta test the AIBECS package.

This [README](https://github.com/briochemc/AIBECS_demo/blob/master/README.md) provides a set of instructions and prerequisites to run the notebook.

To run the notebook, you must ensure that you have installed the required software (including the package to run the notebook).
Here are the steps:

## 1. Install Julia

First things first, you must install [Julia](https://julialang.org). Click on the [Julia](https://julialang.org) link, look for the "download" buttons, and install the correct version for your OS.
Once this is done, you should be able to start Julia by typing

```bash
julia
```

in the terminal.
If not, find the Julia executable, and simply double click on it!
This should open a terminal session, and display something like this:

```julia
               _
   _       _ _(_)_     |  Documentation: https://docs.julialang.org
  (_)     | (_) (_)    |
   _ _   _| |_  __ _   |  Type "?" for help, "]?" for Pkg help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 1.1.0 (2019-01-21)
 _/ |\__'_|_|_|\__'_|  |  Official https://julialang.org/ release
|__/                   |

julia>
```

This is called the Julia REPL (for Read Eval Loop Print) and is used for interactive use of Julia.
Anyway, this great, Julia is now running on your computer! Congratulations!

If you want to learn more about Julia, you can read [the documentation](https://docs.julialang.org/en/v1/), there is a [Discourse forum](https://discourse.julialang.org/), and there is a [Slack channel](https://julialang.slack.com/messages) if you need help.
But for now you should not need any of those: The notebook will just require you to press Shift + Enter a couple of times.

## 2. Add some Julia packages

In Julia, you can access the package manager by simply typing `]` in the REPL.
Once you type `]`, the REPL changes to

```julia
(v1.1) pkg>
```

This means you're in the package-manager (or `pkg`) mode.

Note that you can exit the `pkg` mode by pressing the `delete` key, and this will revert the Julia prompt to its original form:

```julia
julia>
```

The packages you must install are:

- **a)** The **AIBECS** package

    To create a global steady-state biogeochemistry model, we will be using the [AIBECS](https://github.com/briochemc/AIBECS.jl) package.

    Because this package is not registered with Julia yet, and depends on one of my other unregistered (yet) packages, we must first install the latter.

    Activate the package manager with `]`, and "add" the package by typing first

    ```julia
    add https://github.com/briochemc/WorldOceanAtlasTools.jl.git
    ```

    It should look like this:

    ```julia
    (v1.1) pkg> add https://github.com/briochemc/WorldOceanAtlasTools.jl.git
      Updating git-repo `https://github.com/briochemc/WorldOceanAtlasTools.jl.git`
     Resolving package versions...
      Updating `~/.julia/environments/v1.1/Project.toml`
      [04f20302] + WorldOceanAtlasTools v0.2.0 #master (https://github.com/briochemc/WorldOceanAtlasTools.jl.git)
      Updating `~/.julia/environments/v1.1/Manifest.toml`
      [9e28174c] + BinDeps v0.8.10
      [a9693cdc] + CondaBinDeps v0.1.0
      [124859b0] + DataDeps v0.6.2
      [864edb3b] + DataStructures v0.15.0
      [59287772] + Formatting v0.3.5
      [cd3eb016] + HTTP v0.8.0
      [83e8ac13] + IniFile v0.5.0
      [7eb4fadd] + Match v1.0.2
      [c03570c3] + Memoize v0.3.0
      [e1d29d7a] + Missings v0.4.0
      [30363a11] + NetCDF v0.7.3
      [189a3867] + Reexport v0.2.0
      [a2af1166] + SortingAlgorithms v0.3.1
      [2913bbd2] + StatsBase v0.30.0
      [30578b45] + URIParser v0.4.0
      [1986cc42] + Unitful v0.15.0
      [04f20302] + WorldOceanAtlasTools v0.2.0 #master (https://github.com/briochemc/WorldOceanAtlasTools.jl.git)
    ```

    Then you can add the parent package by typing

    ```julia
    add https://github.com/briochemc/AIBECS.jl.git
    ```

    in `pkg` mode, which should look like

    ```julia
    (v1.1) pkg> add https://github.com/briochemc/AIBECS.jl.git
      Updating git-repo `https://github.com/briochemc/AIBECS.jl.git`
     Resolving package versions...
      Updating `~/.julia/environments/v1.1/Project.toml`
      [3487739c] + TransportMatrixTools v0.3.0 #master (https://github.com/briochemc/AIBECS.jl.git)
      Updating `~/.julia/environments/v1.1/Manifest.toml`
      [4fba245c] + ArrayInterface v0.1.1
      [a74b3585] + Blosc v0.5.1
      [e1450e63] + BufferedStreams v1.0.0
      [631607c0] + CMake v1.1.1
      [d5fb7624] + CMakeWrapper v0.2.2
      [49dc2e85] + Calculus v0.4.1
      [324d7699] + CategoricalArrays v0.5.2
      [944b1d66] + CodecZlib v0.5.2
      [a93c6f00] + DataFrames v0.17.1
      [9a8bc11e] + DataStreams v0.4.1
      [2b5f629d] + DiffEqBase v5.6.4
      [ffbed154] + DocStringExtensions v0.7.0
      [31f4e45d] + DualMatrixTools v1.2.4
      [fa6b7ba4] + DualNumbers v0.6.2
      [bf96fef3] + FieldMetadata v0.0.3
      [5789e2e9] + FileIO v1.0.6
      [4c728ea3] + Flatten v0.1.0
      [f67ccb44] + HDF5 v0.11.1
      [0862f596] + HTTPClient v0.2.1
      [d9be37ee] + Homebrew v0.7.1
      [04d39a18] + HyperDualMatrixTools v2.0.2
      [50ceba7f] + HyperDualNumbers v4.0.0
      [82899510] + IteratorInterfaceExtensions v0.1.1
      [033835bb] + JLD2 v0.1.2
      [b27032c2] + LibCURL v0.5.0
      [522f3ed2] + LibExpat v0.5.0
      [2ec943e9] + Libz v1.0.0
      [23992714] + MAT v0.5.0
      [77ba4419] + NaNMath v0.3.2
      [d96e819e] + Parameters v0.10.3
      [3cdcf5f2] + RecipesBase v0.6.0
      [731186ca] + RecursiveArrayTools v0.20.0
      [ae029012] + Requires v0.5.2
      [f2b01f46] + Roots v0.8.1
      [276daf66] + SpecialFunctions v0.7.2
      [90137ffa] + StaticArrays v0.10.3
      [3783bdb8] + TableTraits v0.4.1
      [bd369af6] + Tables v0.1.18
      [3bb67fe8] + TranscodingStreams v0.9.4
      [3487739c] + AIBECS v1.0.0 #master (https://github.com/briochemc/TransportMatrixTools.jl.git)
      [a2a6695c] + TreeViews v0.3.0
      [6fb2a4bd] + UnitfulAngles v0.5.0
      [6112ee07] + UnitfulAstro v0.2.0
      [ea10d353] + WeakRefStrings v0.5.8
      [c17dfb99] + WinRPM v0.4.2
      [9fa8497b] + Future
      [4607b0f0] + SuiteSparse
    ```

    This should only take a few seconds.

- **b)** the **Plots** package

    In order to plot things, i.e., to look at the output of the beautiful work you will be doing in this demo, you will need a plotting package.
    Just like before, make sure you are in `pkg` mode and type `add Plots` (and press return), and you should see something like:

    ```julia
    (v1.1) pkg> add Plots
      Updating registry at `~/.julia/registries/General`
      Updating git-repo `https://github.com/JuliaRegistries/General.git`
     Resolving package versions...
     Installed Showoff ─────────── v0.2.1
     Installed PlotThemes ──────── v0.3.0
     Installed Measures ────────── v0.3.0
     Installed ColorTypes ──────── v0.7.5
     Installed Plots ───────────── v0.24.0
     Installed PlotUtils ───────── v0.5.8
     Installed Contour ─────────── v0.5.1
     Installed FixedPointNumbers ─ v0.5.3
     Installed Colors ──────────── v0.9.5
     Installed GR ──────────────── v0.39.1
      Updating `~/.julia/environments/v1.1/Project.toml`
      [91a5bcdd] + Plots v0.24.0
      Updating `~/.julia/environments/v1.1/Manifest.toml`
      [3da002f7] + ColorTypes v0.7.5
      [5ae59095] + Colors v0.9.5
      [d38c429a] + Contour v0.5.1
      [53c48c17] + FixedPointNumbers v0.5.3
      [28b8d3ca] + GR v0.39.1
      [442fdcdd] + Measures v0.3.0
      [ccf2f8ad] + PlotThemes v0.3.0
      [995b91a9] + PlotUtils v0.5.8
      [91a5bcdd] + Plots v0.24.0
      [992d4aef] + Showoff v0.2.1
      Building GR ───→ `~/.julia/packages/GR/KGODl/deps/build.log`
      Building Plots → `~/.julia/packages/Plots/47Tik/deps/build.log`
    ```

    And again, this should only take a few seconds.

- **c)** the **IJulia** package

    Finally, the [IJulia](https://github.com/JuliaLang/IJulia.jl) package will be your tool to launch JupyterLab from Julia.

    Same as above, in `pkg` mode, type `add IJulia` (and press return), and you should see something like:

    ```julia
    (v1.1) pkg> add IJulia
      Updating registry at `~/.julia/registries/General`
      Updating git-repo `https://github.com/JuliaRegistries/General.git`
     Resolving package versions...
     Installed SoftGlobalScope ─ v1.0.10
     Installed ZMQ ───────────── v1.0.0
     Installed IJulia ────────── v1.18.1
      Updating `~/.julia/environments/v1.1/Project.toml`
      [7073ff75] + IJulia v1.18.1
      Updating `~/.julia/environments/v1.1/Manifest.toml`
      [7073ff75] + IJulia v1.18.1
      [b85f4697] + SoftGlobalScope v1.0.10
      [c2297ded] + ZMQ v1.0.0
      Building ZMQ ───→ `~/.julia/packages/ZMQ/ABGOx/deps/build.log`
      Building IJulia → `~/.julia/packages/IJulia/gI2uA/deps/build.log`
    ```

    This should only take a few seconds as well.

- **d)** Building extra packages:

    Some of Julia's packages must be built for the notebook to work.
    Don't worry, this is pretty easy too.
    Get in `pkg` mode (type `]` in the REPL), and then
    - type `build CodecZlib`.
        It should look like this:
        ```julia
        (v1.1) pkg> build CodecZlib
          Building CodecZlib → `~/.julia/packages/CodecZlib/9jDi1/deps/build.log`
        ```

Great! You can now proceed to starting the notebook!

## 3. Start JupyterLab

The final step is to start JupyterLab.
First, make sure you are in the normal Julia REPL mode (i.e., press `delete` if you are in `pkg` mode.)
Then, tell Julia that you want to "use" IJulia:

```julia
julia> using IJulia
```

Note you can just copy paste the code above (including the `julia>` bits), and the REPL will know to not paste those automatically.
Everytime a package is used for the first time, Julia will precompile it (which can take a few seconds to minutes, depending on the package — don't worry, just let it finish).

and finally tall Julia to install and start JupyterLab by simply typing `jupyerlab()` in Julia. It should look like:

```julia
julia> jupyterlab()
```

If Julia asks you if you want Conda to install JupyterLab, just say "yes" (i.e., type `y`).
After a couple seconds/minutes of downloads and installations, you should be all set up and a browser window should open with JupyterLab!

Just navigate to the notebook within the JupyterLab of your browser and double-click on the notebook!

