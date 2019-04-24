# AIBECS Demo

This repo contains a Jupyter notebook to beta test the AIBECS package.

This [README](https://github.com/briochemc/AIBECS_demo/blob/master/README.md) provides a set of instructions and prerequisites to run the notebook.

## Prerequisites

To run the notebook, you must ensure that you have installed the required software.
If not, you must first go through these steps:

1. Install Julia

    First things first, you must install [Julia](https://julialang.org). Click on the link, look for the "download" buttons, and install the correct version for your OS.
    Once this is done, you should be able to start Julia by typing
    
    ```bash
    julia
    ```
    
    in command prompt.
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

    Great, Julia is now running on your computer!
    If you want to learn more about Julia, you can read [the documentation](https://docs.julialang.org/en/v1/), and there is a helpful [Slack channel](https://julialang.slack.com/messages) to ask questions if you are stuck.
    But for now you should not need any of those: The notebook will just require you to press Shift + Enter a couple of times.

2. Add the IJulia package to edit/run the notebook via JupyterLab

    Now let's install JupyterLab, which is a tool to run this notebook.
    Once Julia is installed, you will need the [IJulia package](https://github.com/JuliaLang/IJulia.jl) to launch JupyterLab. 
    In Julia, just type `]` and then `add IJulia`.
    Once you type `]`, the Julia prompt changes to

    ```julia
    (v1.1) pkg>
    ```

    This means you're in the package-manager mode. Now typing `add IJulia` (and pressing return), you should see something like:

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

    You can exit the package-manager mode by typing `delete`, and this will revert the Julia prompt to its original form:

    ```julia
    julia>
    ```
    
    Once this is done (it should only take a few seconds), tell Julia that you want to "use" IJulia and then you can install and start JupyterLab by simply typing `jupyerlab()` in Julia. It should look like

    ```julia
    julia> using IJulia
    [ Info: Precompiling IJulia [7073ff75-c697-5162-941a-fcdaad2a7d2a]
    
    julia> jupyterlab()
    ```

    (The precompilation only happens if necessary.)
    When Julia asks you if you want Conda to install JupyterLab, just type `y`. After a couple seconds/minutes of downloads and installations, you should be all set up and a browser window should open with JupyterLab!
    
    Just navigate to this notebook within JupyterLab, and now you should be able to just follow the notebook!    

3. Add the TransportMatrixTools package to create global steady-state biogeochemistry models

    The final setup stage is to install the TransportMatrixTools package.
    To do that, we reactivate the package manager with `]`, and "add" the package:

    ```julia
    ] add https://github.com/briochemc/TransportMatrixTools.jl.git
    ```

4. Add the XXX package to plot things

    In order to look at the output in this demo, you will need a plotting package.
    I suggest using XXX.
    Just install it via
    ```julia
    ] add XXXX
    ```

