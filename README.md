# `bioptim`
`Bioptim` is an optimal control program (OCP) framework for biomechanics. 
It is based on the efficient [biorbd](https://github.com/pyomeca/biorbd) biomechanics library and benefits from the powerful algorithmic diff provided by [CasADi](https://web.casadi.org/).
It interfaces the robust [̀`Ipopt`](https://github.com/coin-or/Ipopt) and the fast [̀`Acados`](https://github.com/acados/acados) solvers to suit all your needs for solving OCP in biomechanics. 

## Status

| | |
|---|---|
| License | <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/license-MIT-success" alt="License"/></a> |
| Continuous integration | [![Build Status](https://travis-ci.org/pyomeca/bioptim.svg?branch=master)](https://travis-ci.org/pyomeca/bioptim) |
| Code coverage | [![codecov](https://codecov.io/gh/pyomeca/bioptim/branch/master/graph/badge.svg?token=NK1V6QE2CK)](https://codecov.io/gh/pyomeca/bioptim) |

# How to install 
The preferred way to install for the lay user is using anaconda. 
Another way, more designed for the core programmers is from the sources. 
While it is theoretically possible to use `bioptim` from Windows, it is highly discouraged since it will require to manually compile all the dependencies. 
A great alternative for the Windows users is *Ubuntu* on *Windows supporting Linux*.

## Installing from Anaconda (For Linux and Mac)
The easiest way to install `bioptim` is to download the binaries from [Anaconda](https://anaconda.org/) repositories. 
The project is hosted on the conda-forge channel (https://anaconda.org/conda-forge/bioptim).

After having installed properly an anaconda client [my suggestion would be Miniconda (https://conda.io/miniconda.html)] and loaded the desired environment to install `bioptim` in, just type the following command:
```bash
conda install -c conda-forge bioptim
```
This will download and install all the dependencies and install `bioptim`. 
And that is it! 
You can already enjoy bioptiming!

The current status of `bioptim` on conda-forge is
| License | Name | Downloads | Version | Platforms |
| --- | --- | --- | --- | --- |
|   <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/license-MIT-success" alt="License"/></a> | [![Conda Recipe](https://img.shields.io/badge/recipe-bioptim-green.svg)](https://anaconda.org/conda-forge/bioptim) | [![Conda Downloads](https://img.shields.io/conda/dn/conda-forge/bioptim.svg)](https://anaconda.org/conda-forge/bioptim) | [![Conda Version](https://img.shields.io/conda/vn/conda-forge/bioptim.svg)](https://anaconda.org/conda-forge/bioptim) | [![Conda Platforms](https://img.shields.io/conda/pn/conda-forge/bioptim.svg)](https://anaconda.org/conda-forge/bioptim) |


## Installing from the sources (For Windows, Linux and Mac)
Installing from the sources is basically as easy as installing from Anaconda, with the difference that you will be required to download and install the dependencies by hand (see section below). 

Once you have downloaded `bioptim`, navigate to the root folder and (assuming your conda environment is loaded if needed), you can type the following command:
```bash 
python setup.py install
```
Assuming everything went well, that is it! 
You can already enjoy bioptiming!

Please note that Windows is shown here as a possible OS. 
As stated before, while this is theoretically possible, it will require that you compile `CasADi`, `RBDL` and `biorbd` by hand since the Anaconda packages are not built for Windows.
This is therefore highly discouraged. 

## Dependencies
`bioptim` relies on several libraries. 
The most obvious one is the `biorbd` suite (including indeed `biorbd` and `bioviz`), but some extra more are required.
Due to the amount of different dependencies, it would be tedious to show how to install them all here. 
The user is therefore invited to read the relevant documentations. 

Here is a list of all direct dependencies (meaning that some dependencies may require other libraries themselves):
- [Python](https://www.python.org/)
- [numpy](https://numpy.org/)
- [scipy](https://scipy.org/)
- [packaging](https://packaging.python.org/)
- [setuptools](https://pypi.org/project/setuptools/)
- [matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [pyomeca](https://github.com/pyomeca/pyomeca)
- [CasADi](https://web.casadi.org/)
- [rbdl-casadi](https://github.com/pyomeca/rbdl-casadi) compiled with the CasADi backend
- [tinyxml](http://www.grinninglizard.com/tinyxmldocs/index.html)
- [biorbd](https://github.com/pyomeca/biorbd)
- [vtk](https://vtk.org/)
- [PyQt](https://www.riverbankcomputing.com/software/pyqt)
- [bioviz](https://github.com/pyomeca/bioviz)
- [̀`Ipopt`](https://github.com/coin-or/Ipopt)
- [̀`Acados`](https://github.com/acados/acados)

and optionally:
- [The linear solvers from the HSL Mathematical Software Library](http://www.hsl.rl.ac.uk/index.html)

All these (except for ̀`Acados` and the HSL lib) can manually be installed using (assuming the anaconda environment is loaded if needed) the `pip3` command, or the Anaconda's following command:
```bash
conda install casadi rbdl=*=*casadi* biorbd=*=*casadi* [bioviz=*=*casadi*] -cconda-forge
```

Since there isn't any `Anaconda` nor `pip3` package of ̀`Acados`, a convenient installer is provided with `bioptim`. 
The installer can be found and run at `[ROOT_BIOPTIM]/external/acados_install.sh`.
However, the installer requires an `Anaconda` environment.
If you have an `Anaconda` environment loaded, the installer should find itself where to install. 
If you want to install elsewhere, you can provide the script with a first argument which is the `$CONDA_PREFIX`. 
The second argument that can be passed to the script is the `$BLASFEO_TARGET`. 
If you don't know what it is, it is probably better to keep the default. 
Please note that depending on your computer architecture, ̀`Acados` may or may not work properly.

HSL is a collection of state-of-the-art packages for large-scale scientific computation. 
Among its best known packages are those for the solution of sparse linear systems (`ma27`, `ma57`, etc.), compatible with ̀`Ipopt`.
HSL packages are [available](http://www.hsl.rl.ac.uk/download/coinhsl-archive-linux-x86_64/2014.01.17/) at no cost for academic research and teaching. 
Once you obtain the HSL dynamic library (libhsl.so), you just have place it in your `Anaconda` environment into the `lib/` folder.
You are now able to use all the options of `bioptim`, including the HSL linear solvers with `Acados`.
We recommend that you use `ma57` as a default linear solver by calling as such:
```python
ocp.solve(solver_options={"linear_solver": "ma57"})
```

# Getting started
The easiest way to learn `bioptim` is to dive into it.
So let's do that and build our first optimal control program together.
Please note that this tutorial is designed to recreate the `examples/getting_started/pendulum.py` file where a pendulum is asked to start in a downward position and to end, balanced, in an upward position while only being able to actively move sideways.

## The import
We won't spend time explaining the import, since every one of them will be explained in details later, and that it is pretty straightforward anyway.
```python
import biorbd
from bioptim import (
    OptimalControlProgram,
    DynamicsFcn,
    Dynamics,
    Bounds,
    QAndQDotBounds,
    InitialGuess,
    ObjectiveFcn,
    Objective,
)
```

## Building the ocp
First of all, let's load a bioMod file using `biorbd`:
```python
biorbd_model = biorbd.Model("pendulum.bioMod")
```
It is convenient since it will provide interesting functions such as the number of degrees of freedom (`biorbd_model.nbQ()`). 
Please note that a copy of `pendulum.bioMod` is available at the end of the *Getting started* section.
In brief, the pendulum consists of two degrees of freedom (sideways movement and rotation) with the center of mass near the head.

The dynamics of the pendulum, as for a lot of biomechanics one as well, is to drive it by the generalized forces. 
That is forces and moments directly applied to the degrees of freedom as if virtual motors were to power them.
In `bioptim`, this dynamic is called torque driven. 
In a torque driven dynamics, the states are the positions (also called generalized coordinates, *q*) and the velocities (also called the generalized velocities, *qdot*) and the controls are the joint torques (also called generalized forces, *tau*). 
Let's define such a dynamics:
```python
dynamics = Dynamics(DynamicsFcn.TORQUE_DRIVEN)
```

The pendulum is required to start in a downward position (0 rad) and to finish in an upward position (3.14 rad) with no velocity at start and end nodes.
To define that, it would be nice to first define boundary constraints on the position (*q*) and velocities (*qdot*) that match those in the bioMod file and to apply them at the very beginning, the very end and all the intermediate nodes as well.
QAndQDotBounds waits for a biorbd model and returns a structure with the minimal and maximal bounds for all the degrees of freedom and velocities on three columns corresponding to the starting node, the intermediate nodes and the final node, respectively.
How convenient!
```python
x_bounds = QAndQDotBounds(biorbd_model)
```
Then, override the first and last column to be 0, that is the sideways and rotation to be null for both the position and the velocities
```python
x_bounds[:, [0, -1]] = 0
```
Finally, override once again the final node for the rotation, so it is upside down.
```python
x_bounds[1, -1] = 3.14
```
At that point, you may want to have a look at the `x_bounds.min` and `x_bounds.max` matrices to convince yourself that the initial and final position and velocities are prescribed and that all the intermediate points are free up to a certain minimal and maximal values. 

Up to that point, there is nothing preventing the solver to simply use the virtual motor of the rotation to rotate the pendulum upward (like clock hands) to get to the upside down rotation. 
What makes this example interesting is that we can prevent this by defining minimal and maximal bounds on the control (the maximal forces that these motors have)
```
u_bounds = Bounds([-100, 0], [100, 0])
```
Like this, the sideways force ranges from -100 Newton to 100 Newton, but the rotation force ranges from 0 N/m to 0 N/m.
Again, `u_bound` is defined for the first, the intermediate and the final nodes, but this time, we don't want to specify anything particular for the first and final nodes, so we can leave them as is. 

Who says optimization, says cost function.
Even though, it is possible to define an OCP without objective, it is not so much recommended, and let's face it... much less fun!
So the goal (or the cost function) of the pendulum is to perform its task while using the minimum forces as possible. 
Therefore, an objective function that minimizes the generalized forces is defined:
```python
objective_functions = Objective(ObjectiveFcn.Lagrange.MINIMIZE_TORQUE)
```

At that point, it is possible to solves the program.
Still, helping the solver is usually a good idea, so let's give ̀`Ipopt` a starting point to investigate.
The initial guess that we can provide are those for the states (`x_init`, here *q* and *qdot*) and for the controls (`u_init`, here *tau*). 
So let's define both of them quickly
```python
x_init = InitialGuess([0, 0, 0, 0])
u_init = InitialGuess([0, 0])
```
Please note that `x_init` is twice the size of `u_init` because it contains the two degrees of freedom from the generalized coordinates (*q*) and the two from the generalized velocities (*qdot*), while `u_init` only contains the generalized forces (*tau*)

We now have everything to create the ocp!
For that we have to decide how much time the pendulum has to get up there (`phase_time`) and how many shooting point are defined for the multishoot (`n_shooting`).
Thereafter, you just have to send everything to the `OptimalControlProgram` class and let `bioptim` prepare everything for you.
For simplicity's sake, I copy all the piece of code previously visited in the building of the ocp section here:
```python
ocp = OptimalControlProgram(
        biorbd_model,
        dynamics,
        n_shooting=25,
        phase_time=3,
        x_init=x_init,
        u_init=u_init,
        x_bounds=x_bounds,
        u_bounds=u_bounds,
        objective_functions=objective_functions,
    )
```

## Solving the ocp
It is now time to see `Ipopt` in action! 
To solve the ocp, you simply have to call the `solve()` method of the `ocp` class
```python
sol = ocp.solve(show_online_optim=True)
```
If you feel fancy, you can even activate the online optimization graphs!
However, for such an easy problem, `Ipopt` won't leave you the time to appreciate the realtime updates of the graph...
That's it!

## Show the results
If you want to have a look at the animated data, `bioptim` has an interface to `bioviz` which is designed to visualize bioMod files.
For that, simply call the `animate()` method of the solution:
```python
sol.animate()
```

If you did not fancy the online graphs, but would enjoy them anyway, you can call the method `graphs()`:
```python
sol.graphs()
```

If you are interested in the results of individual objective functions and constraints, you can print them using the `print()`:
```python
sol.print()
```

And that is all! 
You have completed your first optimal control program with `bioptim`! 

## The full files
If you did not completely follow (or were too lazy to!) you will find in this section the complete files described in the Getting started section.
You will find that the file is a bit different from the `example/getting_started/pendulum.py`, but it is merely differences on the surface.

### The pendulum.py file
```python
import biorbd
from bioptim import (
    OptimalControlProgram,
    DynamicsFcn,
    Dynamics,
    Bounds,
    QAndQDotBounds,
    InitialGuess,
    ObjectiveFcn,
    Objective,
)

biorbd_model = biorbd.Model("pendulum.bioMod")
dynamics = Dynamics(DynamicsFcn.TORQUE_DRIVEN)
x_bounds = QAndQDotBounds(biorbd_model)
x_bounds[:, [0, -1]] = 0
x_bounds[1, -1] = 3.14
u_bounds = Bounds([-100, 0], [100, 0])
objective_functions = Objective(ObjectiveFcn.Lagrange.MINIMIZE_TORQUE)
x_init = InitialGuess([0, 0, 0, 0])
u_init = InitialGuess([0, 0])

ocp = OptimalControlProgram(
        biorbd_model,
        dynamics,
        n_shooting=25,
        phase_time=3,
        x_init=x_init,
        u_init=u_init,
        x_bounds=x_bounds,
        u_bounds=u_bounds,
        objective_functions=objective_functions,
    )
    
sol = ocp.solve(show_online_optim=True)
sol.print()
sol.animate()
```
### The pendulum.bioMod file
Here is a simple pendulum that can be interpreted by `biorbd`. 
For more information on how to build a bioMod file, one can read the doc of [biorbd](https://github.com/pyomeca/biorbd).

```c
version 4

// Seg1
segment Seg1
    translations	y
    rotations	x
    ranges  -1 5
            -2*pi 2*pi
    mass 1
    inertia
        1 0 0
        0 1 0
        0 0 0.1
    com 0.1 0.1 -1
    mesh 0.0   0.0   0.0
    mesh 0.0  -0.0  -0.9
    mesh 0.0   0.0   0.0
    mesh 0.0   0.2  -0.9
    mesh 0.0   0.0   0.0
    mesh 0.2   0.2  -0.9
    mesh 0.0   0.0   0.0
    mesh 0.2   0.0  -0.9
    mesh 0.0   0.0   0.0
    mesh 0.0  -0.0  -1.1
    mesh 0.0   0.2  -1.1
    mesh 0.0   0.2  -0.9
    mesh 0.0  -0.0  -0.9
    mesh 0.0  -0.0  -1.1
    mesh 0.2  -0.0  -1.1
    mesh 0.2   0.2  -1.1
    mesh 0.0   0.2  -1.1
    mesh 0.2   0.2  -1.1
    mesh 0.2   0.2  -0.9
    mesh 0.0   0.2  -0.9
    mesh 0.2   0.2  -0.9
    mesh 0.2  -0.0  -0.9
    mesh 0.0  -0.0  -0.9
    mesh 0.2  -0.0  -0.9
    mesh 0.2  -0.0  -1.1
endsegment

    // Marker 1
    marker marker_1
        parent Seg1
        position 0 0 0
    endmarker

    // Marker 2
    marker marker_2
        parent Seg1
        position 0.1 0.1 -1
    endmarker
```

# A more in depth look at the `bioptim` API

In this section, we are going to have an in depth look at all the classes one can use to interact with the bioptim API. 
All the classes covered here, can be imported using the command:
```python
from bioptim import ClassName
```

## The OCP
An optimal control program is an optimization that uses control variables in order to drive some state variables.
There are mainly two different types of ocp, which is the `direct collocation` and the `direct multiple shooting`.
`Bioptim` is based on the latter. 
To summarize, it defines a large optimization problem by discretizing the control and the state variables into a predetermined number of intervals, the beginning of which are called the shooting points.
By defining strict constraints between the end of an interval and the beginning of the next, it can ensure a proper dynamics of the system, ???->while have good insight to solve the problem using gradient decending algorithms.

### Class: OptimalControlProgram
This is the main class that holds an ocp. 
Most of the attributes and methods are for internal use, therefore the API user should not care much about them.
Once an OptimalControlProgram is constructed, it is usually ready to be solved.

The full signature of the `OptimalControlProgram` can be scary at first, but should becomes clear soon.
Here it is:
```python
OptimalControlProgram(
    biorbd_model: [str, biorbd.Model, list],
    dynamics: [Dynamics, DynamicsList],
    n_shooting: [int, list],
    phase_time: [float, list],
    x_init: [InitialGuess, InitialGuess]
    u_init: [InitialGuess, InitialGuessList], 
    x_bounds: [Bounds, BoundsList],
    u_bounds: [Bounds, BoundsList],
    objective_functions: [Objective, ObjectiveList],
    constraints: [Constraint, ConstraintList],
    parameters: ParameterList,
    external_forces: list,
    ode_solver: OdeSolver,
    control_type: [ControlType, list],
    all_generalized_mapping: BiMapping,
    q_mapping: BiMapping,
    qdot_mapping: BiMapping,
    tau_mapping: BiMapping,
    plot_mappings: Mapping,
    phase_transitions: PhaseTransitionList,
    n_threads: int,
    use_sx: bool,
)
```
Of these, only the first 4 are mandatory.
`biorbd_model` is the `biorbd` model to use. If the model is not loaded, a string can be passed. 
In the case of a multiphase optimization, one model per phase should be passed in a list.
`dynamics` is the dynamics of the system during each phase (see The dynamics section).
`n_shooting` is the number of shooting point of the direct multiple shooting for each phase.
`phase_time` is the final time of each phase. If the time is free, this is the initial guess.
`x_init` is the initial guess for the states variables (see The initial conditions section)
`u_init` is the initial guess for the controls variables (see The initial conditions section)
`x_bounds` is the minimal and maximal value the states can have (see The bounds section)
`u_bounds` is the minimal and maximal value the controls can have (see The bounds section)
`objective_functions` is the objective function set of the ocp (see The objective functions section)
`constraints` is the constraint set of the ocp (see The constraints section)
`parameters` is the parameter set of the ocp (see The parameters section)
`external_forces` are the external forces acting on the center of mass of the bodies. 
It is list (one element for each phase) of np.array of shape (6, i, n), where the 6 components are [Mx, My, Mz, Fx, Fy, Fz], for the ith force platform (defined by the externalforceindex) for each node n
`ode_solver` is the ode solver used to solve the dynamic equations
`control_type` is the type of discretization of the controls (usually CONSTANT) (see ControlType section)
`all_generalized_mapping` is used to reduce the number of degrees of freedom by linking them (see The mappings section).
This ones applies the same mapping to the generalized coordinates (*q*), velocities (*qdot*) and forces (*tau*).
`q_mapping` the mapping applied to *q*.
`qdot_mapping` the mapping applied to *q_dot*.
`tau_mapping` the mapping applied to *tau*.
`plot_mappings` is to force some plot to be linked together. 
`n_threads` is to solve the optimization using multiple thread. 
This number is the number of thread to use.
`use_sx` is if the CasADi graph should be constructed in SX. 
SX will tend to solve much faster than MX graphs, however they can necessitate a huge amount of RAM.

Please note that a common ocp will usually define only these parameters:
```python
ocp = OptimalControlProgram(
    biorbd_model: [str, biorbd.Model, list],
    dynamics: [Dynamics, DynamicsList],
    n_shooting: [int, list],
    phase_time: [float, list],
    x_init: [InitialGuess, InitialGuess]
    u_init: [InitialGuess, InitialGuessList], 
    x_bounds: [Bounds, BoundsList],
    u_bounds: [Bounds, BoundsList],
    objective_functions: [Objective, ObjectiveList],
    constraints: [Constraint, ConstraintList],
    n_threads: int,
)
```

The main methods one will be interested in are:
```python
ocp.update_objectives()
ocp.update_constraints()
ocp.update_parameters()
ocp.update_bounds()
ocp.update_initial_guess()
```
These allow to modify the ocp after being defined. 
It is particularly useful when solving the ocp for a first time, and then adjusting some parameters and reoptimizing afterwards.

Moreover, the method 
```python
solution = ocp.solve(Solver, solver_options:{})
```
is called to actually solve the ocp (the solution structure is discussed later). 
The `Solver` parameter can be used to select the nonlinear solver to solve the ocp, ̀`Ipopt` being the default choice.
Note that options can be passed to the solver via the `solver_options` parameter.
One can refer to the documentation of their respective chosen solver to know which options exist.
The `show_online_optim` parameter can be set to `True` so the graphs nicely update during the optimization.
It is expected to slow down the optimization a bit though.

Finally, one can save and load previously optimized values by using
```python
ocp.save(solution, file_path)
ocp, solution = OptimalControlProgram.load(file_path)
```
Please note that this is `bioptim` version dependent, which means that an optimized solution from a previous version will not probably load on a newer `bioptim` version.
To save the solution in a version independent manner, you may want to manually save the data from the solution.

Finally, the `add_plot(name, update_function)` method can be used to create new dynamics plots.
The name is simply the name of the figure.
If one with the same name already exists, then the axes are merged.
The update_function is a function handler with signature: `update_function(states: np.ndarray, constrols: np.ndarray: parameters: np.ndarray) -> np.ndarray`.
It is expected to return a np.ndarray((n, 1)), where `n` is the number of elements to plot. 
The `axes_idx` parameter can be added to parse the data in a more exotic manner.
For instance, on a three axes figure, if one wanted to plot the first value on the third axes and the second value on the first axes and nothing on the second, the `axes_idx=[2, 0]` would do the trick.
The interested user can have a look at the `examples/getting_started/custom_plotting.py` example.

### Class: NonLinearProgram
The NonLinearProgram is by essence the phase of an ocp. 
The user is expected not to change anything from this class, but can retrieve useful information from it.

One of the main use of nlp is to get a reference to the biorbd_model for the current phase: `nlp.model`.
Another important value stored in nlp is the shape of the states and controls: `nlp.shape`, which is a dictionary where the keys are the names of the elements (for instance, *q* for the generalized coordinates)

It would be tedious, and probably not much useful, to list all the elements of nlp here.   
The interested user is invited to have a look at the docstrings for this particular class to get a detailed overview of it.

## The dynamics
By essence, an optimal control program (ocp) links two types of variables: the states (x) and the controls (u). 
Conceptually, the controls could be seen as the driving inputs of the system, which participate to changing the system states. 
In the case of biomechanics, the states (*x*) are usually the generalized coordinates (*q*) and velocities (*qdot*), i.e., the pose of the musculoskeletal model and the joint velocities. 
On the other hand, the controls (*u*) can be the generalized forces, i.e., the joint torques, but can also be the muscle excitations, for instance.
States and controls are linked through Ordinary differential equations of the form: dx/dt = f(x, u, p), where p can be additional parameters that act on the system, but are not time dependent.

The following section investigate how to instruct `bioptim` of the dynamic equations the system should follow.

 
### Class: Dynamics
This class is the main class to define a dynamics. 
It therefore contains all the information necessary to configure (i.e., determining which variables are states or controls) and perform the dynamics. 
When constructing an `OptimalControlProgram()`, Dynamics is the expected class for the `dynamics` parameter. 

The user can minimally define a Dynamics as follows: `dyn = Dynamics(DynamicsFcn)`.
The `DynamicsFcn` are the one presented in the corresponding section below. 

#### The options
The full signature of Dynamics is as follows:
```python
Dynamics(dynamics_type, configure: Callable, dynamic_function: Callable, phase: int)
```
The `dynamics_type` is the selected `DynamicsFcn`. 
It automatically defines both `configure` and `dynamic_function`. 
If a function is sent instead, this function is interpreted as `configure` and the DynamicsFcn is assumed to be `DynamicsFcn.CUSTOM`
If one is interested in changing the behaviour of a particular `DynamicsFcn`, they can refer to the Custom dynamics functions right below. 

The `phase` is the index of the phase the dynamics applies to. 
This is usually taken care by the `add()` method of `DynamicsList`, but it can be useful when declaring the dynamics out of order.

#### Custom dynamic functions
If an advanced user wants to define their own dynamic function, they can define the configuration and/or the dynamics. 

The configuration is what tells `bioptim` which variables are states and which are control.
The user is expected to provide a function handler with the follow signature: `custom_configure(ocp: OptimalControlProgram, nlp: NonLinearProgram)`.
In this function the user is expected to call the relevant `Problem` class methods: 
- `configure_q(nlp, as_states: bool, as_controls: bool)`
- `configure_qdot(nlp, as_states: bool, as_controls: bool)`
- `configure_q_qdot(nlp, as_states: bool, as_controls: bool)`
- `configure_tau(nlp, as_states: bool, as_controls: bool)`
- `configure_muscles(nlp, as_states: bool, as_controls: bool)`
where `as_states` add the variable to the states vector and `as_controls` to the controls vector.
Please note that this is not necessary mutually exclusive.
Finally, the user is expected to configure the dynamic by calling `Problem.configure_dynamics_function(ocp, nlp, custom_dynamics)`

Defining the dynamic function must be done when one provides a custom configuration, but can also be defined by providing a function handler to the `dynamic_function` parameter for `Dynamics`. 
The signature of this custom dynamic function is as follows: `custom_dynamic(states: MX, controls: MX, parameters: MX, nlp: NonLinearProgram`.
This function is expected to return a tuple[MX] of the derivative of the states. 
Some method defined in the class `DynamicsFunctions` can be useful, but will not be covered here since it is initially designed for internal use.
Please note that MX type is a CasADi type.
Anyone who wants to define custom dynamics should be at least familiar with this type beforehand. 


### Class: DynamicsList
A DynamicsList is simply a list of Dynamics. 
The `add()` method can be called exactly as if one was calling the `Dynamics` constructor. 
If the `add()` method is used more than one, the `phase` parameter is automatically incremented. 

So a minimal use is as follows:
```python
dyn_list = DynamicsList()
dyn_list.add(DynamicsFcn)
```

### Class: DynamicsFcn
The `DynamicsFcn` class is the configuration and declaration of all the already available dynamics in `bioptim`. 
Since this is an Enum, it is possible to use tab key on the keyboard to dynamically list them all, depending on the capabilities of your IDE. 

Please note that one can change the dynamic function associated to any of the configuration by providing a custom dynamics_function. 
For more information on this, please refer to the Dynamics and DynamicsList section right before. 

#### TORQUE_DRIVEN
The torque driven defines the states (x) as *q* and *qdot* and the controls (u) as *tau*. 
The derivative of *q* is trivially *qdot*.
The derivative of *qdot* is given by the biorbd function: `qddot = biorbd_model.ForwardDynamics(q, qdot, tau)`. 
If external forces are provided, they are added to the ForwardDynamics function. 

#### TORQUE_DRIVEN_WITH_CONTACT
The torque driven defines the states (x) as *q* and *qdot* and the controls (u) as *tau*. 
The derivative of *q* is trivially *qdot*.
The derivative of *qdot* is given by the `biorbd` function that includes non-acceleration contact point defined in the bioMod: `qddot = biorbd_model.ForwardDynamicsConstraintsDirect(q, qdot, tau)`.

#### TORQUE_ACTIVATIONS_DRIVEN
The torque driven defines the states (x) as *q* and *qdot* and the controls (u) as the level of activation of *tau*. 
The derivative of *q* is trivially *qdot*.
The actual *tau* is computed from the activation by the `biorbd` function: `tau = biorbd_model.torque(torque_act, q, qdot)`.
Then, the derivative of *qdot* is given by the `biorbd` function: `qddot = biorbd_model.ForwardDynamics(q, qdot, tau)`. 

Please note, this dynamics is expected to be very slow to converge, if it ever does. 
One is therefore encourage using TORQUE_DRIVEN instead, and to add the TORQUE_MAX_FROM_ACTUATORS constraint.
This has been shown to be more efficient and allows defining minimum torque.

#### TORQUE_ACTIVATIONS_DRIVEN_WITH_CONTACT
The torque driven defines the states (x) as *q* and *qdot* and the controls (u) as the level of activation of *tau*. 
The derivative of *q* is trivially *qdot*.
The actual *tau* is computed from the activation by the `biorbd` function that includes non-acceleration contact point defined in the bioMod: `tau = biorbd_model.torque(torque_act, q, qdot)`.
Then, the derivative of *qdot* is given by the `biorbd` function: `qddot = biorbd_model.ForwardDynamics(q, qdot, tau)`. 

Please note, this dynamics is expected to be very slow to converge, if it ever does. 
One is therefore encourage using TORQUE_DRIVEN instead, and to add the TORQUE_MAX_FROM_ACTUATORS constraint.
This has been shown to be more efficient and allows defining minimum torque.

#### MUSCLE_ACTIVATIONS_DRIVEN
The torque driven defines the states (x) as *q* and *qdot* and the controls (u) as the muscle activations. 
The derivative of *q* is trivially *qdot*.
The actual *tau* is computed from the muscle activation converted in muscle forces and thereafter converted to *tau* by the `biorbd` function: `biorbd_model.muscularJointTorque(muscles_states, q, qdot)`.
The derivative of *qdot* is given by the `biorbd` function: `qddot = biorbd_model.ForwardDynamics(q, qdot, tau)`. 

#### MUSCLE_ACTIVATIONS_AND_TORQUE_DRIVEN
The torque driven defines the states (x) as *q* and *qdot* and the controls (u) as the *tau* and the muscle activations (*a*). 
The derivative of *q* is trivially *qdot*.
The actual *tau* is computed from the sum of *tau* to the muscle activation converted in muscle forces and thereafter converted to *tau* by the `biorbd` function: `biorbd_model.muscularJointTorque(a, q, qdot)`.
The derivative of *qdot* is given by the `biorbd` function: `qddot = biorbd_model.ForwardDynamics(q, qdot, tau)`. 

#### MUSCLE_ACTIVATIONS_AND_TORQUE_DRIVEN_WITH_CONTACT
The torque driven defines the states (x) as *q* and *qdot* and the controls (u) as the *tau* and the muscle activations (*a*). 
The derivative of *q* is trivially *qdot*.
The actual *tau* is computed from the sum of *tau* to the *a* converted in muscle forces and thereafter converted to *tau* by the `biorbd` function: `biorbd_model.muscularJointTorque(a, q, qdot)`.
The derivative of *qdot* is given by the `biorbd` function that includes non-acceleration contact point defined in the bioMod: `qddot = biorbd_model.ForwardDynamics(q, qdot, tau)`. 

#### MUSCLE_EXCITATIONS_DRIVEN
The torque driven defines the states (x) as *q*, *qdot* and muscle activations (*a*) and the controls (u) as the *EMG*. 
The derivative of *q* is trivially *qdot*.
The actual *tau* is computed from *a* converted in muscle forces and thereafter converted to *tau* by the `biorbd` function: `biorbd_model.muscularJointTorque(muscles_states, q, qdot)`.
The derivative of *qdot* is given by the `biorbd` function: `qddot = biorbd_model.ForwardDynamics(q, qdot, tau)`. 
The derivative of *a* is computed by the `biorbd` function: `adot = model.activationDot(emg, a)`

#### MUSCLE_EXCITATIONS_AND_TORQUE_DRIVEN
The torque driven defines the states (x) as *q*, *qdot* and muscle activations (*a*) and the controls (u) as the *tau* and the *EMG*. 
The derivative of *q* is trivially *qdot*.
The actual *tau* is computed from the sum of *tau* to *a* converted in muscle forces and thereafter converted to *tau* by the `biorbd` function: `biorbd_model.muscularJointTorque(muscles_states, q, qdot)`.
The derivative of *qdot* is given by the `biorbd` function: `qddot = biorbd_model.ForwardDynamics(q, qdot, tau)`. 
The derivative of *a* is computed by the `biorbd` function: `adot = model.activationDot(emg, a)`

#### MUSCLE_EXCITATIONS_AND_TORQUE_DRIVEN_WITH_CONTACT
The torque driven defines the states (x) as *q*, *qdot* and muscle activations (*a*) and the controls (u) as the *tau* and the *EMG*. 
The derivative of *q* is trivially *qdot*.
The actual *tau* is computed from the sum of *tau* to *a* converted in muscle forces and thereafter converted to *tau* by the `biorbd` function: `biorbd_model.muscularJointTorque(muscles_states, q, qdot)`.
The derivative of *qdot* is given by the `biorbd` function that includes non-acceleration contact point defined in the bioMod: `qddot = biorbd_model.ForwardDynamics(q, qdot, tau)`. 
The derivative of *a* is computed by the `biorbd` function: `adot = model.activationDot(emg, a)`

#### CUSTOM
This leaves the user to define both the configuration (what are the states and controls) and to define the dynamic function. 
CUSTOM should not be called by the user, but the user should pass the configure_function directly. 
You can have a look at Dynamics and DynamicsList sections for more information about how to configure and define custom dynamics.


## The bounds
The bounds provide a class that has minimal and maximal values for a variable.
It is, for instance, useful for the inequality constraints that limit the maximal and minimal values of the states (x) and the controls (u) .
In that sense, it is what is expected by the `OptimalControlProgram` for its `u_bounds` and `x_bounds` parameters. 
It can however be used for much more.

### Class: Bounds
The Bounds class is the main class to define bounds.
The constructor can be called by sending two boundary matrices (min, max) as such: `bounds = Bounds(min_bounds, max_bounds)`. 
Or by providing a previously declared bounds: `bounds = Bounds(bounds=another_bounds)`.
The `min_bounds` and `max_bounds` matrices must have dimensions that fit the chosen `InterpolationType`, the default type being `InterpolationType.CONSTANT_WITH_FIRST_AND_LAST_DIFFERENT`, which is 3 columns.

The full signature of Bounds is as follows:
```python
Bounds(min_bounds, max_bound, interpolation: InterpolationType, phase: int)
```
The first parameters are presented before.
The `phase` is the index of the phase the bounds apply to.
This is usually taken care by the `add()` method of `BoundsList`, but it can be useful when declaring the bounds out of order.

If the interpolation type is CUSTOM, then the bounds are function handlers of signature: 
```python
custom_bound(current_shooting_point: int, n_elements: int, n_shooting: int)
```
where current_shooting_point is the current point to return, n_elements is the number of expected lines and n_shooting is the number of total shooting point (that is if current_shooting_point == n_shooting, this is the end of the phase)

The main methods the user will be interested in is the `min` property that returns the minimal bounds and the `max` property that returns the maximal bounds. 
Unless it is a custom function, `min` and `max` are numpy.ndarray and can be directly modified to change the boundaries. 
It is also possible to change `min` and `max` simultaneously by directly slicing the bounds as if it was a numpy.array, effectively defining an equality constraint: for instance `bounds[:, 0] = 0`. 
Finally, the `concatenate(another_bounds: Bounds)` method can be called to vertically concatenate multiple bounds.


### Class: BoundsList
A BoundsList is simply a list of Bounds. 
The `add()` method can be called exactly as if one was calling the `Bounds` constructor. 
If the `add()` method is used more than once, the `phase` parameter is automatically incremented. 

So a minimal use is as follows:
```python
bounds_list = BoundsList()
bounds_list.add(min_bounds, max_bounds)
```

### Class: QAndQDotBounds 
The QAndQDotBounds is a Bounds that uses a biorbd_model to define the minimal and maximal bounds for the generalized coordinates (*q*) and velocities (*qdot*). 
It is particularly useful when declaring the states bounds for *q* and *qdot*. 
Anything that was presented for Bounds, also applies to QAndQDotBounds


## The initial conditions
The initial conditions the solver should start from, i.e., initial values of the states (x) and the controls (u).
In that sense, it is what is expected by the `OptimalControlProgram` for its `u_init` and `x_init` parameters. 

### Class InitialGuess

The InitialGuess class is the main class to define initial guesses.
The constructor can be called by sending one initial guess matrix (init) as such: `bounds = InitialGuess(init)`. 
The `init` matrix must have the dimensions that fits the chosen `InterpolationType`, the default type being `InterpolationType.CONSTANT`, which is 1 column.

The full signature of Bounds is as follows:
```python
Bounds(initial_guess, interpolation: InterpolationType, phase: int)
```
The first parameters are presented before.
The `phase` is the index of the phase the initial guess applies to.
This is usually taken care by the `add()` method of `InitialGuessList`, but it can be useful when declaring the initial guess out of order.

If the interpolation type is CUSTOM, then the InitialGuess is a function handler of signature: 
```python
custom_bound(current_shooting_point: int, n_elements: int, n_shooting: int)
```
where current_shooting_point is the current point to return, n_elements is the number of expected lines and n_shooting is the number of total shooting point (that is if current_shooting_point == n_shooting, this is the end of the phase)

The main methods the user will be interested in is the `init` property that returns the initial guess. 
Unless it is a custom function, `init` is a numpy.ndarray and can be directly modified to change the initial guess. 
Finally, the `concatenate(another_initial_guess: InitialGuess)` method can be called to vertically concatenate multiple initial guesses.

### Class InitialGuessList
A InitialGuessList is a list of InitialGuess. 
The `add()` method can be called exactly as if one was calling the `InitialGuess` constructor. 
If the `add()` method is used more than one, the `phase` parameter is automatically incremented. 

So a minimal use is as follows:
```python
init_list = InitialGuessList()
init_list.add(init)
```


## The constraints
The constraints are hard penalties of the optimization program.
That means the solution won't be considered optimal unless all the constraint set is fully respected.
The constraints come in two format: equality and inequality. 

### Class: Constraint
The Constraint provides a class that prepares a constraint, so it can be added to the constraint set by `bioptim`.
When constructing an `OptimalControlProgram()`, Constraint is the expected class for the `constraint` parameter. 
It is also possible to later change the constraint by calling the method `update_constraints(the_constraint)` of the `OptimalControlProgram`

The Constraint class is the main class to define constraints.
The constructor can be called with the type of the constraint and the node to apply it to, as such: `constraint = Constraint(ConstraintFcn, node=Node.END)`. 
By default, the constraint will be an equality constraint equals to 0. 
To change this behaviour, one can add the parameters `min_bound` and `max_bound` to change the bounds to their desired values. 

The full signature of Constraint is as follows:
```python
Constraint(ConstraintFcn, node: node, index: list, phase: int, list_index: int, target: np.ndarray **extra_param)
```
The first parameters are presented before.
The `list` is the list of elements to keep. 
For instance, if one defines a TRACK_STATE constraint with `index=0`, then only the first state is tracked.
The default value is all the elements.
The `phase` is the index of the phase the constraint should apply to.
If it is not sent, phase=0 is assumed.
The `list_index` is the ith element of a list for a particular phase
This is usually taken care by the `add()` method of `ConstraintList`, but it can be useful when declaring the constraints out of order, or when overriding previously declared constraints using `update_constraints`.
The `target` is a value subtracted to the constraint value. 
It is useful to define tracking problems.
The dimensions of the target must be of [index, node]

The `ConstraintFcn` class provides a list of some predefined constraint functions. 
Since this is an Enum, it is possible to use tab key on the keyboard to dynamically list them all, assuming you IDE allows for it. 
It is possible however to define a custom constraint by sending a function handler in place of the `ConstraintFcn`.
The signature of this custom function is: `custom_function(pn: PenaltyNodes, **extra_params)`
The PenaltyNodes contains all the required information to act on the states and controls at all the nodes defined by `node`, while `**extra_params` are all the extra parameters sent to the `Constraint` constructor. 
The function is expected to return an MX vector of the constraint to be inside `min_bound` and `max_bound`. 
Please note that MX type is a CasADi type.
Anyone who wants to define custom constraint should be at least familiar with this type beforehand. 

### Class: ConstraintList
A ConstraintList is by essence simply a list of Constraint. 
The `add()` method can be called exactly as if one was calling the `Constraint` constructor. 
If the `add()` method is used more than one, the `list_index` parameter is automatically incremented for the prescribed `phase`.
If no `phase` are prescribed by the user, the first phase is assumed. 

So a minimal use is as follows:
```python
constraint_list = ConstraintList()
constraint_list.add(constraint)
```

### Class: ConstraintFcn
The `ConstraintFcn` class is the declaration of all the already available constraints in `bioptim`. 
Since this is an Enum, it is possible to use tab key on the keyboard to dynamically list them all, depending on the capabilities of your IDE. 

#### TRACK_STATE
Tracks the states variable towards a target

#### TRACK_MARKERS
Tracks the skin markers towards a target.
The extra parameter `axis_to_track: Axis = (Axis.X, Axis.Y, Axis.Z)` can be sent to specify the axes on which to track the markers

#### TRACK_MARKERS_VELOCITY
Tracks the skin marker velocities towards a target.

#### SUPERIMPOSE_MARKERS
Matches one marker with another one.
The extra parameters `first_marker_idx: int` and `second_marker_idx: int` informs which markers are to be superimposed

#### PROPORTIONAL_STATE
Links one state to another, such that `x[first_dof] = coef * x[second_dof]`
The extra parameters `first_dof: int` and `second_dof: int` must be passed to the `Constraint` constructor

#### PROPORTIONAL_CONTROL
Links one control to another, such that `u[first_dof] = coef * u[second_dof]`
The extra parameters `first_dof: int` and `second_dof: int` must be passed to the `Constraint` constructor

#### TRACK_TORQUE
Tracks the generalized forces part of the control variables towards a target

#### TRACK_MUSCLES_CONTROL
Tracks the muscles part of the control variables towards a target

#### TRACK_ALL_CONTROLS
Tracks all the control variables towards a target

#### TRACK_CONTACT_FORCES
Tracks the non-acceleration point reaction forces towards a target

#### TRACK_SEGMENT_WITH_CUSTOM_RT
Links a segment with an RT (for instance, an Inertial Measurement Unit). 
It does so by computing the homogenous transformation between the segment and the RT and then converting this to Euler angles.
The extra parameters `segment_idx: int` and `rt_idx: int` must be passed to the `Constraint` constructor

#### TRACK_MARKER_WITH_SEGMENT_AXIS
Tracks a marker using a segment, that is aligning an axis toward the marker.
The extra parameters `marker_idx: int`, `segment_idx: int` and `axis: Axis` must be passed to the `Constraint` constructor

#### TRACK_COM_POSITION
Constraints the center of mass towards a target.
The extra parameter `axis_to_track: Axis = (Axis.X, Axis.Y, Axis.Z)` can be sent to specify the axes on which to track the markers

#### TRACK_COM_VELOCITY
Constraints the center of mass velocity towards a target.
The extra parameter `axis_to_track: Axis = (Axis.X, Axis.Y, Axis.Z)` can be sent to specify the axes on which to track the markers

#### CONTACT_FORCE
Adds a constraint to the non-acceleration point reaction forces.
It is usually used in conjunction with changing the bounds, so it creates an inequality constraint on this contact force.
The extra parameter `contact_force_idx: int` must be passed to the `Constraint` constructor

#### NON_SLIPPING
Adds a constraint of static friction at contact points constraining for small tangential forces. 
This constraint assumes that the normal forces is positive (that is having an additional CONTACT_FORCE with `max_bound=np.inf`).
The extra parameters `tangential_component_idx: int`, `normal_component_idx: int` and `static_friction_coefficient: float` must be passed to the `Constraint` constructor

#### TORQUE_MAX_FROM_ACTUATORS
Adds a constraint of maximal torque to the generalized forces controls such that the maximal *tau* are computed from the `biorbd` method `biorbd_model.torqueMax(q, qdot).`
This is an efficient alternative to the torque activation dynamics. 
The extra parameter `min_torque` can be passed to ensure that the model is never too weak

#### TIME_CONSTRAINT
Adds the time to the optimization variable set. 
It will leave the time free, within the given boundaries

#### CUSTOM
CUSTOM should not be directly sent by the user, but the user should pass the custom_constraint function directly. 
You can have a look at Constraint and ConstraintList sections for more information about how to define custom constraints.


## The objective functions
The objective functions are soft penalties of the optimization program.
That means the solution tries to minimize the value as much as possible but won't complaint if it does a bad job at it.
The objective functions come in two format: Lagrange and Mayer. 

The Lagrange objective functions are integrated over the whole phase (actually over the selected nodes, which are usually Node.ALL). 
One should note that integration is not given by the dynamics function but by the rectangle approximation over a node.

The Mayer objective functions are values at a single node, usually the Node.LAST. 

### Class: Objective
The Objective provides a class that prepares an objective function, so it can be added to the objective set by `bioptim`.
When constructing an `OptimalControlProgram()`, Objective is the expected class for the `objective_functions` parameter. 
It is also possible to later change the objective functions by calling the method `update_objectives(the_objective_function)` of the `OptimalControlProgram`

The Objective class is the main class to define objectives.
The constructor can be called with the type of the objective and the node to apply it to, as such: `objective = Objective(ObjectiveFcn, node=Node.END)`. 
Please note that `ObjectiveFcn` should either be a `ObjectiveFcn.Lagrange` or `ObjectiveFcn.Mayer`.

The full signature of Objective is as follows:
```python
Objective(ObjectiveFcn, node: Node, index: list, phase: int, list_index: int, quadratic: bool, target: np.ndarray, weight: float, **extra_param)
```
The first parameters are presented before.
The `list` is the list of elements to keep. 
For instance, if one defines a MINIMIZE_STATE objective_function with `index=0`, then only the first state is minimized.
The default value is all the elements.
The `phase` is the index of the phase the objective function should apply to.
If it is not sent, phase=0 is assumed.
The `list_index` is the ith element of a list for a particular phase
This is usually taken care by the `add()` method of `ObjectiveList`, but it can be useful when declaring the objectives out of order, or when overriding previously declared objectives using `update_objectives`.
`quadratic` is used to defined if the objective function should be squared. 
This is particularly useful when one wants to minimize toward 0 instead of minus infinity
The `target` is a value subtracted to the objective value. 
It is useful to define tracking problems.
The dimensions of the target must be of [index, node].
Finally, `weight` is the weighting that should be applied to the objective. 
The higher the weight is, the more important the objective is compared to the other objective functions.

The `ObjectiveFcn` class provides a list of some predefined objective functions. 
Since `ObjectiveFcn.Lagrange` and `ObjectiveFcn.Mayer` are Enum, it is possible to use tab key on the keyboard to dynamically list them all, assuming you IDE allows for it. 
It is possible however to define a custom objective function by sending a function handler in place of the `ObjectiveFcn`.
If one do so, an additional parameter must be sent to the `Objective` constructor which is `custom_type` and must be either `ObjectiveFcn.Lagrange` or `ObjectiveFcn.Mayer`.
The signature of the custom function is: `custom_function(pn: PenaltyNodes, **extra_params)`
The PenaltyNodes contains all the required information to act on the states and controls at all the nodes defined by `node`, while `**extra_params` are all the extra parameters sent to the `Objective` constructor. 
The function is expected to return an MX vector of the objective function. 
Please note that MX type is a CasADi type.
Anyone who wants to define custom objective functions should be at least familiar with this type beforehand. 

### ObjectiveList
An ObjectiveList is a list of Objective. 
The `add()` method can be called exactly as if one was calling the `Objective` constructor. 
If the `add()` method is used more than one, the `list_index` parameter is automatically incremented for the prescribed `phase`.
If no `phase` are prescribed by the user, the first phase is assumed. 

So a minimal use is as follows:
```python
objective_list = ObjectiveList()
objective_list.add(objective)
```

### Class: ObjectiveFcn

#### MINIMIZE_TIME (Lagrange and Mayer)
Adds the time to the optimization variable set. 
It will try to minimize the time towards minus infinity or towards a target.
If the Mayer term is used, `min_bound` and `max_bound` can also be defined.

#### MINIMIZE_STATE (Lagrange and Mayer)
Minimizes the states variable towards zero (or a target)

#### TRACK_STATE (Lagrange and Mayer)
Tracks the states variable towards a target

#### MINIMIZE_MARKERS (Lagrange and Mayer)
Minimizes the position of the markers towards zero (or a target)
The extra parameter `axis_to_track: Axis = (Axis.X, Axis.Y, Axis.Z)` can be sent to specify the axes on which to track the markers

#### TRACK_MARKERS (Lagrange and Mayer)
Tracks the skin markers towards a target.
The extra parameter `axis_to_track: Axis = (Axis.X, Axis.Y, Axis.Z)` can be sent to specify the axes on which to track the markers

#### MINIMIZE_MARKERS_DISPLACEMENT (Lagrange)
Minimizes the difference between a state at a node and the same state at the next node, effectively minimizing the velocity
The extra parameter `coordinates_system_idx` can be specified to compute the marker position in that coordinate system. 
Otherwise, it is computed in the global reference frame. 

#### MINIMIZE_MARKERS_VELOCITY (Lagrange and Mayer)
Minimizes the skin marker velocities towards zero (or a target)

#### TRACK_MARKERS_VELOCITY (Lagrange and Mayer)
Tracks the skin marker velocities towards a target.

#### SUPERIMPOSE_MARKERS (Lagrange and Mayer)
Tracks one marker with another one.
The extra parameters `first_marker_idx: int` and `second_marker_idx: int` informs which markers are to be superimposed

#### PROPORTIONAL_STATE (Lagrange and Mayer)
Minimizes the difference between one state and another, such that `x[first_dof] ~= coef * x[second_dof]`
The extra parameters `first_dof: int` and `second_dof: int` must be passed to the `Objective` constructor

#### PROPORTIONAL_CONTROL (Lagrange)
Minimizes the difference between one control and another, such that `u[first_dof] ~= coef * u[second_dof]`
The extra parameters `first_dof: int` and `second_dof: int` must be passed to the `Objective` constructor

#### MINIMIZE_TORQUE (Lagrange)
Minimizes the generalized forces part of the controls variable towards zero (or a target)

#### TRACK_TORQUE (Lagrange)
Tracks the generalized forces part of the controls variable towards a target

#### MINIMIZE_STATE_DERIVATIVE (Lagrange)
Minimizes the difference between a state at a node and the same state at the next node, effectively minimizing the generalized forces derivative

#### MINIMIZE_TORQUE_DERIVATIVE (Lagrange)
Minimizes the difference between a *tau* at a node and the same *tau* at the next node, effectively minimizing the generalized forces derivative

#### MINIMIZE_MUSCLES_CONTROL (Lagrange)
Minimizes the muscles part of the controls variable towards zero (or a target)

#### TRACK_MUSCLES_CONTROL (Lagrange)
Tracks the muscles part of the controls variable towards a target

#### MINIMIZE_ALL_CONTROLS (Lagrange)
Minimizes all the controls variable towards zero (or a target)

#### TRACK_ALL_CONTROLS (Lagrange)
Tracks all the controls variable towards a target

#### MINIMIZE_CONTACT_FORCES (Lagrange)
Minimizes the non-acceleration points reaction forces towards zero (or a target)

#### TRACK_CONTACT_FORCES (Lagrange)
Tracks the non-acceleration points reaction forces towards a target

#### MINIMIZE_COM_POSITION (Lagrange and Mayer)
Minimizes the center of mass position towards zero (or a target).
The extra parameter `axis_to_track: Axis = (Axis.X, Axis.Y, Axis.Z)` can be sent to specify the axes on which to track the markers

#### MINIMIZE_COM_VELOCITY (Lagrange and Mayer)
Minimizes the center of mass velocity towards zero (or a target).
The extra parameter `axis_to_track: Axis = (Axis.X, Axis.Y, Axis.Z)` can be sent to specify the axes on which to track the markers

#### MINIMIZE_PREDICTED_COM_HEIGHT (Mayer)
Minimizes the prediction of the center of mass maximal height from the parabolic equation, assuming vertical axis is Z (2): CoM_dot[2]**2 / (2 * -g) + CoM[2].
To maximize a jump, one can use this function at the end of the push-off phase and declare a weight of -1.

#### TRACK_SEGMENT_WITH_CUSTOM_RT (Lagrange and Mayer)
Minimizes the distance between a segment and an RT (for instance, an Inertial Measurement Unit). 
It does so by computing the homogenous transformation between the segment and the RT and then converting this to Euler angles.
The extra parameters `segment_idx: int` and `rt_idx: int` must be passed to the `Objective` constructor

#### TRACK_MARKER_WITH_SEGMENT_AXIS (Lagrange and Mayer)
Minimizes the distance between a marker and an axis of a segment, that is aligning an axis toward the marker.
The extra parameters `marker_idx: int`, `segment_idx: int` and `axis: Axis` must be passed to the `Objective` constructor

#### CUSTOM (Lagrange and Mayer)
CUSTOM should not be directly sent by the user, but the user should pass the custom_objective function directly. 
You can have a look at Objective and ObjectiveList sections for more information about how to define custom objective function.


## The parameters
Parameters are time independent variables. 
It can be, for instance, the maximal value of the strength of a muscle, or even the value of gravity.
If affects the dynamics of the whole system. 
Due to the variety of parameters, it was impossible to provide predefined parameters, apart from time. 
Therefore, all the parameters are custom made.

### Class: ParameterList
The ParameterList provides a class that prepares the parameters, so it can be added to the parameter set to optimize by `bioptim`.
When constructing an `OptimalControlProgram()`, ParameterList is the expected class for the `parameters` parameter. 
It is also possible to later change the parameters by calling the method `update_parameters(the_parameter_list)` of the `OptimalControlProgram`

The ParameterList class is the main class to define parameters.
Please note that unlike other lists, `Parameter` is not accessible, this is for simplicity reasons as it would complicate the API quite a bit to permit it.
Therefore, one should not call the Parameter constructor directly. 

Here is the full signature of the `add()` method of the `ParameterList`:
```python
ParameterList.add(parameter_name: str, function: Callable, initial_guess: InitialGuess, bounds: Bounds, size: int, phase: int, penalty_list: Objective, **extra_parameters)
```
The `parameter_name` is the name of the parameter. 
This is how it will be referred to in the output data as well.
The `function` is the function that modifies the biorbd model, it will be called just prior to applying the dynamics
The signature of the custom function is: `custom_function(biorbd.Model, MX, **extra_parameters)`, where biorbd.Model is the model to apply the parameter to, the MX is the value the parameter will take, and the `**extra_parameters` are those sent to the add() method.
This function is expected to modify the biorbd_model, and not return anything.
Please note that MX type is a CasADi type.
Anyone who wants to define custom parameters should be at least familiar with this type beforehand.
The `initial_guess` is the initial values of the parameter.
The `bounds` are the maximal and minimal values of the parameter.
The `size` is the number of element of this parameter.
If an objective function is provided, the return of the objective function should match the size.
The `phase` that the parameter applies to.
Even though a parameter is time independent, one biorbd_model is loaded per phase. 
Since parameters are associate to a specific biorbd_model, one must define a parameter per phase.
The `penalty_list` is the index in the list the penalty is. 
If one adds multiple parameters, the list is automatically incremented. 
It is useful however to define this value by hand if one wants to declare the parameters out of order or to override a previously declared parameter using `update_parameters`.

## The phase transitions
`Bioptim` can declare multiphase optimisation programs. 
The goal of a multiphase ocp is usually to handle changing dynamics. 
The user must understand that each phase is therefore a full ocp by itself, with constraints that links the end of which with the beginning of the following.
Due to some limitations created by the use of MX variables, some things can be done and some cannot during a phase transition. 

### Class: PhaseTransitionList
The PhaseTransitionList provide a class that prepares the phase transitions.
When constructing an `OptimalControlProgram()`, PhaseTransitionList is the expected class for the `phase_transitions` parameter. 

The PhaseTransitionList class is the main class to define parameters.
Please note that unlike other lists, `PhaseTransition` is not accessible since phase transition don't make sense for single phase ocp.
Therefore, one should not call the PhaseTransition constructor directly. 

Here is the full signature of the `add()` method of the `PhaseTransitionList`:
```python
PhaseTransitionList.add(PhaseTransitionFcn, phase_pre_idx, **extra_parameters)
```
The `PhaseTransitionFcn` is transition phase function to use.
The default is CONTINUOUS.
If one wants to declare a custom transition phase, then PhaseTransitionFcn is the function handler to the custom function.
The signature of the custom function is: `custom_function(state_pre: MX, state_post: MX, **extra_parameters)`, where `state_pre` is the states variable at the end of the phase before the transition, `state_post` is those at the beginning of the phase after the transition, and the `**extra_parameters` are those sent to the add() method.
This function is expected to return the cost of the phase transition computed from the states pre and post in the form of an MX.
Please note that MX type is a CasADi type.
Anyone who wants to define phase transitions should be at least familiar with this type beforehand.
The `phase_pre_idx` is the index of the phase before the transition.

### Class: PhaseTransitionFcn
The `PhaseTransitionFcn` class is the already available phase transitions in `bioptim`. 
Since this is an Enum, it is possible to use tab key on the keyboard to dynamically list them all, depending on the capabailities of your IDE. 

#### CONTINUOUS
The states at the end of the phase_pre equals the states at the beginning of the phase_post

#### IMPACT
The impulse function of `biorbd`: `qdot_post = biorbd_model.ComputeConstraintImpulsesDirect, q_pre, qdot_pre)` is apply to compute the velocities of the joint post impact.
These computed states at the end of the phase_pre equals the states at the beginning of the phase_post.

If a bioMod with more contact points than the phase before is used, then the IMPACT transition phase should be used as well

#### CYCLIC
Apply the CONTINUOUS phase transition to the end of the last phase and the begininning the of first, effectively creating a cyclic movement

#### CUSTOM
CUSTOM should not be directly sent by the user, but the user should pass the custom_transition function directly. 
You can have a look at the PhaseTransitionList section for more information about how to define custom transition function.

## The results
`Bioptim` offers different ways to manage and visualize the results from an optimisation. 
This section explores the different methods that can be called to have a look at your data.

Everything related to managing the results can be accessed from the solution class returned from 
```python
sol = ocp.solve()
```

### Data manipulation
The Solution structure holds all the optimized values. 
To get the states variable, one can invoke the `states = sol.states` property.
Similarly, to get the controls variable, one can invoke the `states = sol.controls` property.
If the program was a single phase problem, then the returned values are dictionaries, otherwise it is a list of dictionaries of size equals to the number of phases.
The keys of the returned dictionaries correspond to the name of the variables. 
For instance, if generalized coordinates (*q*) are states, then the state dictionary has *q* as key.
In any cases, the key `all` is always there.
The values inside the dictionaries are np.array of dimension `n_elements` x `n_shooting`, unless the data were previously altered by integrating or interpolating (then the number of columns may differ).

The parameters are very similar, but differs by the fact that it is always a dictionary (since parameters don't depend on the phases).
Also, the values inside the dictionaries are of dimension `n_elements` x 1. 

It is possible to integrate (also called simulate) the states at will, by calling the `sol.integrate()` method.
The `shooting_type: Shooting` parameter allows to select the type of integration to perform (see the enum Shooting for more detail).
The `keepdims` parameter allows to keep the initial dimensions of the return structure. If set to false, depending on the integrator, intermediate points between the node can be added (usually a multiple of n_steps of the Runge-Kutta).
By definition, setting `keepdims` to True while asking for `Shooting.MULTIPLE` would return the exact same structure. This will therefore raise an error.
The same is true if `continusous` is set to False, which necessarily changes the dimension. It is therefore prohibited.
The `merge_phase: bool` parameter requests to merge all the phases into one [True] or not [False].
The `continuous: bool` parameter can be deceiving. If it mostly for internal purposes. 
In brief, it discards [True] or keeps [False] the arrival value of a node of integration, resulting in doubling the number of points at each node.
Most of the time, one wants to set `continuous` to True, unless you need to get the individual integrations of each node.

The `sol.interpolation(n_frames: [int, tuple])` method returns the states interpolated by changing the number of shooting points.
If the program is multiphase, but only a `int` is sent, then the phases are merged and the interpolation keeps their respective time ratio consistent.
If one does not want to merge the phases, then a `tuple` with one value per phase can be sent. 

Finally `sol.merge_phases()` returns a Solution structure with all the phases merged into one.

Please note that, apart from `sol.merge_phases()`, these data manipulation methods return an incomplete Solution structure.
This structure can be used for further analyses, but cannot be used for visualization. 
If one wants to visualize integrated or interpolated data, they are required to use the corresponding parameters or the visualization method they use.

### Data visualization
A first method to visualize the data is `sol.graphs()`. 
This method will spawn all the graphs associated with the ocp. 
This is the same method that is called by the online plotter. 
In order to add and modify plots, one should use the `ocp.add_plot()` method.
By default, this graphs the states as multiple shootings.
If one wants to simulate in single shooting, the option `shooting_type=Shooting.SINGLE` will do the trick.

A second one is `sol.animate()`.
This method summons one or more `bioviz` figures (depending if phases were merged or not) and animates the model.
Please note that despite `bioviz` best efforts, plotting a lot of meshing vertices in MX format is slow.
So even though it is possible, it is suggested to animate without the bone meshing (by passing the parameter `show_meshes=False`)
To do so, we strongly suggest saving the data and load them in an environment where `bioptim` is compiled with the Eigen backend, which will be much more efficient.
If `n_frames` is set, an interpolation is performed, otherwise, the phases are merged if possible, so a single animation is shown. 
To prevent from the phase merging, one can set `n_frames=-1`.

In order to print the values of the objective functions and constraints, one can use the `sol.print()` method.
If the parameter `cost_type=CostType.OBJECTIVE` is passed, only the values of each objective functions are printed.
The same is true for the constraints with `CostType.CONSTRAINTS`.
Please note that for readability purposes, this method prints the sum by phases for the constraints. 

## The extra stuff and the Enum
It was hard to categorize the remaining classes and enum. 
So I present them in bulk in this extra stuff section

### The mappings
The mapping are a way to link things stored in a list.
For instance, lets consider these vectors: a = [0, 0, 0, 10, -9] and b = [10, 9]. 
Even though they are quite different, they share some common values. 
It it therefore possible to retrieve a from b, and conversely.

This is what the Mapping class does, for the rows of numpy arrays.
So if one was to declare the following Mapping: `b_from_a = Mapping([3, -4])`.
Then, assuming a is a numpy.ndarray column vector (`a = np.array([a]).T`), it would be possible to summon b from a like so: 
```python
b = b_from_a.map(a)
```
Note that the `-4` opposed the forth value.
Conversely, using the `a_from_b = Mapping([None, None, None, 0, -1])` mapping, and assuming b is a numpy.ndarray column vector (`b = np.array([b]).T`), it would be possible to summon b from a like so:
```python
a = a_from_b.map(b)
```
Note the `None` are replaced by zeros.

The BiMapping is no more no less than a list of two mappings that link two matrices both ways: `BiMapping(a_to_b, b_to_a)`

### Enum: Node
The node targets some specific nodes of the ocp or of a phase

The accepted values are:
- START: The first node
- MID: The middle node
- INTERMEDIATES: All the nodes but the first and the last one
- END: The last node
- ALL: All the nodes

### Class: OdeSolver
The ordinary differential equation (ode) solver to solve the dynamics of the system. 
The RK4 and RK8 are the one with the most options available.
IRK is supposed to be a bit more robust, but may be slower too. 
CVODES is the one with the least options, since it is not in-house implemented.

The accepted values are:
- RK4: Runge-Kutta of the 4th order
- RK8: Runge-Kutta of the 8th order
- IRK: Implicit runge-Kutta
- CVODES: cvodes solver

### Enum: Solver
The nonlinear solver to solve the whole ocp. 
Each solver has some requirements (for instance, ̀`Acados` necessitates that the graph is SX). 
Feel free to test each of them to see which one fits the best your needs.
̀`Ipopt` is a robust solver, that may be a bit slow though.
̀`Acados` on the other is a very fast solver, but is much more sensitive to the relative weightings of the objective functions and to the initial guess.
It is perfectly designed for MHE and NMPC problems.

The accepted values are:
- ̀`Ipopt`
- ̀`Acados`

### Enum: ControlType
The type the controls are. 
Typically, the controls for an optimal control program are constant over the shooting intervals. 
However, one may wants to get non constant values.
`Bioptim` has therefore implemented some other types of controls.

The accepted values are:
- CONSTANT: The controls remain constant over the interval. The number of control is therefore equals to the number of shooting point
- LINEAR_CONTINUOUS: The controls are linearly interpolated over the interval. Since they are continuous, the end of an interval corresponds to the beginning of the next. There is therefore number of shooting point + 1 controls.

### Enum: PlotType
When adding a plot, it is possible to change the aspect of it.

The accepted values are:
PLOT: Normal plot that links the points.
INTEGRATED: Plot that links the points within an interval, but is discrete between the end of an interval and the beginning of the next one.
STEP: Step plot, constant over an interval

### Enum: InterpolationType
How a time dependent variable is interpolated.
It is mostly used for phases time span.
Therefore, first and last nodes refer to the first and last nodes of a phase

The accepted values are:
- CONSTANT: Requires only one column, all the values are equal during the whole period of time.
- CONSTANT_WITH_FIRST_AND_LAST_DIFFERENT: Requires three columns. The first and last columns correspond to the first and last node, while the middle corresponds to all the other nodes.
- LINEAR: Requires two columns. It corresponds to the first and last node. The middle nodes are linearly interpolated to get their values.
- EACH_FRAME: Requires as many columns as there are nodes. It is not an interpolation per se, but it allows the user to specify all the nodes individually.
- SPLINE: Requires five columns. It performs a cubic spline to interpolate between the nodes.
- CUSTOM: User defined interpolation function


### Enum: Shooting
The type of integration to perform
- MULTIPLE: resets the state at each node
- SINGLE: resets the state at each phase
- SINGLE_CONTINUOUS: never resets the state. The behaviour of SINGLE and SINGLE_CONTINUOUS are the same for a single phase program

### Enum: CostType
The type of cost
- OBJECTIVES: The objective functions
- CONSTRAINTS: The constraints
- ALL: All the previously described cost type

# Citing
If you use `bioptim`, we would be grateful if you could cite it as follows:
@misc{Michaud2020bioptim,
    author = {Michaud, Benjamin and Bailly, Francois and Begon, Mickael et al.},
    title = {bioptim, a Python interface for Musculoskeletal Optimal Control in Biomechanics},
    howpublished={Web page},
    url = {https://github.com/pyomeca/bioptim},
    year = {2020}
}
