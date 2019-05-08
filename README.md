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
      (...)
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
      [3487739c] + AIBECS v1.0.0 #master (https://github.com/briochemc/AIBECS.jl.git)
      (...)
    ```

    This should only take a few seconds.

- **b)** the **Cartopy** packages

    In order to plot things, i.e., to look at the output of the beautiful work you will be doing in this demo, you will need a plotting package.
    Here, we are going to try Python's [Cartopy](https://scitools.org.uk/cartopy/docs/latest/).
    First, we need to install it via the `Conda` package, which we need to install via `add Conda` (and press return), and you should see something like:

    ```julia
    (v1.1) pkg> add Conda
     Resolving package versions...
      Updating `~/.julia/environments/v1.1/Project.toml`
      [8f4d0f93] + Conda v1.2.0
    ```

    Then we install PyPlot:
    ```julia
    (v1.1) pkg> add PyPlot
    ```

    And we also need PyCall:
    ```julia
    (v1.1) pkg> add PyCall
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

