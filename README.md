# Install and use Octave and symbolic on macOS with Brew
This is a tutorial meant for users who wish to use `symbolic` functionality in octave on macOS. It assumes that `homebrew` manages all packages, including `octave` and `python`. The complication for me was installing `sympy` in a way that it is compatible with `homebrew`'s installation of `octave` and `python`.
## First, install `homebrew`.
`brew` is a macOS package manager that is recommended to be used exclusively, not with other managers like MacPorts.

[View installation instructions here.](https://brew.sh/) Try your best to understand the commands and what they're doing. Follow *all* directions that `brew` gives you in the terminal when installing.
## Next, install `octave`.
Use `brew` to install the latest version of `octave` and its dependencies. [View installation instructions here.](https://wiki.octave.org/Octave_for_macOS) Again, follow *all* directions outlined here, and try your best to understand what each command is doing.

The 'Creating a launcher app' segment is helpful for when you want to use the Octave GUI, but this guide does not use it. All commands outlined in this guide can just as easily be entered into the command window in the Octave GUI later on.

Octave will be installed to the default location for all `homebrew`-managed packages. This makes it easy to update, but causes a bit of complication with installing Python libraries. We'll work around those complications in a bit.

## Install `python`, if you haven't already.
```
brew install python
```

## Install `symbolic`.
If you haven't already, in a terminal, run `octave` to try out your new installation. You should arrive at an `octave:1>` prompt.  
To add the `symbolic` package to this installation of `octave`, type
```
pkg install -forge symbolic
```
to install the symbolic package from Forge. After completion, type `exit` to return to a command prompt.
## Create venv
Take a few minutes to [learn about venvs.](https://docs.python.org/3/library/venv.html)

If `python` is managed by a package manager like `brew`, venvs are used to install specific packages to *only* the project that you're currently working in. It's also easy to delete and start again if you mess something up; for this reason, it's recommended to use venvs in any Python project you're working on to keep it isolated from others.

Create (and enter) a new directory where you want your symbolic octave environment to be.  

Example:  
```
cd Library/CloudStorage/OneDrive-HoustonChristianUniversity/ACS
```
```
mkdir octave_venv && cd $_
```
Your current directory should now be whatever directory you just created.

Next, create a Python virtual environment. This creates a new folder in your directory called `venv`. This is where all your site-specific packages will go.  
```
python3 -m venv venv
```
Now, activate this venv as your current working project. Any future Python commands will use this venv as its current environment, rather than the one made by `brew` that you can't do anything with.
```
source venv/bin/activate
```
## Install `sympy` into venv.
Assuming your venv is activated now, the following command will install `sympy` to *only* this current venv. This can be done to any venv for any package on any project. Just make sure to `cd` to the right directory next time you're working on a project!
```
pip install sympy
```
## Use Octave.  
Example in CLI mode with expected output:
```
(venv) blakealley@Blakes-MacBook-Pro octave_venv % octave
GNU Octave, version 9.3.0
Copyright (C) 1993-2024 The Octave Project Developers.

octave:1> pkg load symbolic
octave:2> syms s t
Symbolic pkg v3.2.1: Python communication link active, SymPy v1.13.3.
octave:3> f(t) = 2*t^3 - 5*e^(-t) 
f(t) = (symfun)

     3      -t
  2⋅t  - 5⋅ℯ  

octave:4> F(s) = laplace (f(t), t, s)
F(s) = (symfun)

      5     12
  - ───── + ──
    s + 1    4
            s 

octave:5> exit


(venv) blakealley@Blakes-MacBook-Pro octave_venv % 
```

Like stated above, the Python venv commands can be used in the Octave GUI Command Window as well. Ensure that your current working directory is the `octave_venv` folder you made earlier, though.
