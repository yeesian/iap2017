# Nonlinear and Mixed-integer optimization

## Preassignment

For this class, we will be using the Gurobi mixed-integer programming solver, a few other nonlinear solvers (SCS and ECOS), and some other Julia packages.

### Installing Gurobi
Gurobi is commercial software, but they have a very permissive (and free!) academic license. If you have an older version of Gurobi (>= 5.5) on your computer, that should be fine.

1. Go to www.gurobi.com
2. Create an account, and request an academic license.
3. Download the installer for Gurobi 6.0
4. Install Gurobi, accepting default options. Remember where it installed to!
5. Go back to the website and navigate to the page for your academic license. You'll be given a command with a big code in it, e.g. grbgetkey aaaaa-bbbb
6. In a terminal, navigate to the ``gurobi600/<operating system>/bin`` folder where ``<operating system>`` is the name of your operating system.  
7. Copy-and-paste the command from the website into the command prompt---you need to be on campus for this to work!


### Install the Gurobi interface in Julia

Installing this is easy using the Julia package manager: 
```jl
julia> Pkg.add("Gurobi")
```

If you don't have an academic email or cannot get access for Gurobi for another reason, you should be able to follow along with the open source solver GLPK for much of the class. To install, simply do
```jl
julia> Pkg.add("GLPKMathProgInterface")
```

### Install remaining packages
We will use the following packages:
- Convex
- Distributions
- ECOS
- JuMP
- PyPlot
- SCS

First run ``Pkg.update()`` to update the package database, then install each one with ``Pkg.add("xxx")`` where ``xxx`` is the package name.

### Test the installation

In a blank IJulia notebook, paste the following code into a cell:

```julia
import Convex
x = Convex.Variable(Convex.Positive())
Convex.solve!(Convex.minimize(x))
Convex.evaluate(x)
```

and run it by pressing shift-enter. The result should be some iteration output from ECOS and then a small value that's very close to zero.

How about a simple knapsack problem? In the next cell, enter the following JuMP code and submit all the output to Stellar.

```julia
using JuMP, Gurobi
m = Model(solver=GurobiSolver(Presolve=0)) # turn presolve off to make it a lil more interesting
N = 100
@variable(m, x[1:N], Bin)
@constraint(m, dot(rand(N), x) <= 5)
@objective(m, Max, dot(rand(N), x))
solve(m)
```

## Questions?
Email yeesian@mit.edu or mlubin@mit.edu
