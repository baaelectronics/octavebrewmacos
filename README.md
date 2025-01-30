# Install and use Octave and symbolic on macOS with Brew
## Install homebrew
[View installation instructions here.](https://brew.sh/)
## Install octave
[View installation instructions here.](https://wiki.octave.org/Octave_for_macOS)
## Install symbolic
In a terminal, run `octave` and type `pkg install -forge symbolic` to install the symbolic package from Forge.
## Create venv
[Learn about venvs.](https://docs.python.org/3/library/venv.html)  
Create (and enter) a new directory where you want your symbolic octave environment to be.  

Example:  
```
cd Library/CloudStorage/OneDrive-HoustonChristianUniversity/ACS
```
```
mkdir octave_venv && cd $_
```
Your current directory should now be <octave_venv>.

Create a Python virtual environment.  
```
python3 -m venv venv
```
```
source venv/bin/activate
```
## Install sympy into venv
```
pip install sympy
```
## Use Octave.  
Example with expected output:
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
