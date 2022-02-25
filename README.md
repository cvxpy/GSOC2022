# GSOC2022

CVXPY is an open-source Python-embedded modeling language for convex optimization problems. 
It lets you express your problem in a natural way that follows the math, 
rather than in the restrictive standard form required by solvers.

[CVXPY](https://www.cvxpy.org/) will be a participating sub-organization in [NumFOCUS](http://numfocus.org/)'s application
for [Google Summer of Code 2022](https://summerofcode.withgoogle.com/). For more information about this application see:

- [NumFOCUS's main GSoC page](https://github.com/numfocus/gsoc)

## Mentors

All four CVXPY Maintainers are preparred to serve as Mentors for the projects below.

- [Steven Diamond](https://github.com/SteveDiamond)
- [Akshay Agrawal](https://github.com/akshayka)
- [Riley Murray](https://github.com/rileyjmurray)
- [Bartolomeo Stellato](https://github.com/bstellato)

Riley Murray wrote the description for the first project and Steven Diamond wrote the description for the second project.



## Idea 1: Improve CVXPY's capabilities for quantum information modeling

*This is a large (350 hour) project.*

### Abstract

Convex optimization is an important tool in Quantum Information (QI).
CVXPY is used in QI-focused Python
packages like [QuTiP](https://github.com/qutip/qutip),
[qiskit-optimization](https://github.com/Qiskit/qiskit-optimization), Rigetti's [Grove](https://github.com/rigetti/grove),
and Sandia National Labs' [pyGSTi](https://github.com/pyGSTio/pyGSTi).
The goal of this project is to update CVXPY with breakthrough mathematical
methods to enable efficient optimization of quantum entropy, quantum relative entropy,
and many other important functions in QI.
These new tools will dramatically expand CVXPY's usefulness to QI theorists and quantum computer engineers.

### Difficulty and requirements

This is a very substantial project.
It'll involve learning about applied linear algebra, optimization, and software development.
We've put together a detailed roadmap which should make this project suitable for an advanced
undergraduate with an appropriate background.

Here are the project's hard requirements

- You've taken a course on linear algebra.
- You have experience with Python software development. E.g., writing unit tests.
- You're familiar with NumPy and SciPy.

Here are things which would help you succeed in this project (none of them are required!):

- A second course on linear algebra.
- A course that covered optimization models.
- Some familiarity with MATLAB.
- Some familiarity with CVXPY.
- *Any* knowledge of semidefinite programming.
- *Any* knowledge of QI.
- *Any* knowledge of basic numerical integration.
- *Any* knowledge of LaTeX (for mathematical writing).

### Expected Outcomes

We have organized the project into four phases (0, 1, 2, 3) in the Technical Project Roadmap below.
Completing Phase 1 will put the CVXPY Maintainers in an excellent position to see this project through to the end.
We are confident that it is possible for a GSoC intern to complete Phase 1 and possibly also Phase 2.
Phase 3 is very important but can be done in smaller chunks;
it can be considered a stretch goal for GSoC purposes.

### Technical Project Description and Plans

Below we've provided a lot of information on the project. We don't expect you to read it all in one go! It serves as a reference for the summer and as evidence for the fact that we have a good plan.

#### Technical Abstract

The matrix exponential is the most fundamental object in the study of ordinary differential equations.
For positive definite matrices (i.e., symmetric or Hermitian matrices with all positive eigenvalues)
we can also consider the matrix *log*.
If "expm" is the matrix exponential operator, then the matrix log can be defined as the operator "logm"
where logm(expm(A)) = A for every symmetric or Hermitian matrix A.

One can write down convex programs involving the matrix log for computing the capacity of quantum communications channels,
relative entropy of entanglement, and relative entropy of recovery; see
[Fawzi and Fawzi, 2017](https://arxiv.org/pdf/1705.06671.pdf).
Quantum state tomography can also be cast as a convex program involving the matrix log.

There are no widely available convex optimization solvers which support the matrix log.
However, a groundbreaking 2017 paper by Fawzi, Saunderson, and Parrilo ("[FSP2017](https://arxiv.org/abs/1705.00812)") showed how constraints
involving the matrix log can be approximated with constraints that are compatible with semidefinite programming (SDP).
The technical goal of this project is to incorporate these methods into CVXPY.

#### Technical Prep Work

We want you to have a fun and productive experience working on CVXPY for GSoC.
That'll require knowing a little about convex optimization before you write code.
Specifically, you should read the following material from the [MOSEK Modeling Cookbook](https://docs.mosek.com/modeling-cookbook/index.html):

- Sections 1 and 2.
  These sections provide an introduction to the type of optimization known as linear programming.
  Section 2.2 is very important. It explains how one can reformulate many nonlinear convex optimization
  problems into linear programming problems. This kind of reformulation is exactly what CVXPY aims to automate.
- Sections 3 and 6. These address
  second order cone programming
  (aka "quadratic cone programming") and semidefinite programming. You'll learn a ton about semidefinite programming
  while working on this GSoC project.
- Sections 4 and 5. These address how the power cone and 
  relative entropy cone (aka "exponential cone") can be used to model constraints involving logs and power functions.
  Skip Section 5.3. 
- Feel free to skip the Case Studies in Sections 3 through 6.

We'll ask that you give a presentation to the Project Mentors after reading Sections 1 and 2
and another presentation after reading Sections 3 and 6.

Naturally, you'll eventually need to read parts of FSP2017.
That paper defines functions including "(scalar) relative entropy," "operator relative entropy,"
and "the matrix geometric mean."
You can treat those terms as black-boxes for now.

#### Technical Project Roadmap

The methods in FSP2017 have been implemented in a Matlab package called [CVXQUAD](https://github.com/hfawzi/cvxquad),
which builds on another Matlab package called [CVX](http://cvxr.com/cvx/).
CVX and CVXPY serve similar purposes in constructing and processing optimization models.
We can summarize CVXQUAD's mathematical structure as follows:
 1. Provide a CVX function to reformulate "matrix geometric mean" constraints into equivalent SDP constraints.
 2. Provide a CVX function to approximate "operator relative entropy" constraints using matrix geometric mean
    constraints and a numerical integration technique.
 3. Provide CVX functions to reformulate constraints involving QI functions
    into constraints involving operator relative entropy.

Where CVXQUAD basically breaks the problem down into three phases, we'll have an additional "Phase 0"
help get things started.
We get into those phases below.
Don't let them scare you away!
Even getting to the point of completing Phase 1 would be a significant addition to CVXPY.
We hope to complete Phase 2 during GSoC.
Phase 3 can be done in much smaller chunks than the other phases, and so can be considered more of a stretch goal.


*Development Phase 0: approximating scalar relative entropy*

- Mimic the functionality in CVXQUAD's ``op_rel_entr_epi_cone`` function to develop an 
  approximation for scalar relative entropy. Where CVXQUAD relies on its internal 
  ``matrix_geo_mean_hypo_cone`` function, you can use CVXPY's ``geo_mean`` function.
- Develop new test cases for the functionality implemented above. Reference solutions can be computed
  by using ECOS, MOSEK, or SCS. The test suites for CVXOPT, SCIP, GUROBI, and CPLEX should
  be updated to include the new test cases.
- Update web documentation to explain that CVXOPT, SCIP, GUROBI, and CPLEX can be used to approximate
  problems which feature logarithms or exponential functions.

*Development Phase 1: matrix geometric mean*

- Implement FSP2017's techniques of reformulating matrix geometric mean constraints
  into equivalent SDP constraints (CVXQUAD's ``matrix_geo_mean_hypo_cone``). Design
  the implementation so that it should work with Hermitian (that is, conjugate-symmetric) matrices.
- Develop new test cases for this functionality. Include those test cases in the
  [StandardTestSDPs](https://github.com/cvxpy/cvxpy/blob/f93d6b24d2e51033f24e0fff4553e0cbd968d55c/cvxpy/tests/solver_test_helpers.py#L979).

*Development Phase 2: approximating operator relative entropy*

- Extend your implementation of scalar relative entropy approximation from Phase 0
  to support operator relative entropy. This should essentially have the same functionality
  as CVXQUAD's ``op_rel_entr_epi_cone`` module. Design the implementation so that it
  should work with Hermitian matrices.
- Develop new test cases for this functionality and include them in the StandardTestSDPs.

*Development Phase 3: functions for quantum information modeling*

- Create CVXPY functions for quantum entropy, quantum relative entropy, and perhaps a
  few others based on the features you added in Phases 1 and 2.
- Develop new test cases for this functionality.
- Create example Jupyter Notebooks which show how the new functions can be used.

*Other remarks*  

When writing tests for Development Phases 1 through 3, it would be good to consult
Hamza Fawzi's PhD thesis or other published papers.

If you complete all four development phases above, we would be delighted to guide them to contribute
in other areas.
Here are two suggestions:
 - Implement Hamza Fawzi's 2021 approximation method for the scalar and/or operator relative entropy cone.
   [This method](https://github.com/hfawzi/cvxquad/blob/master/doc/log_approx_bounds.pdf)
   controls whether the approximation produces under-estimators or over-estimators, and
   is important for using CVXPY in settings where "proofs" are desired.
 - Update CVXPY's functions like ``geo_mean`` and ``pow`` to use power cone constraints
   instead of the existing method with second order cone constraints. This would basically resolve
   [CVXPY GitHub Issue #1222](https://github.com/cvxpy/cvxpy/issues/1222).
 
## Idea 2: Performance benchmarks with continuous integration

*This is a medium (175 hour) project.*

### Abstract

Improving the speed of problem compilation is a major development goal for CVXPY. We need a thorough benchmark suite to measure improvements, ideally deployed via continuous integration (CI). It should be easy to see the performance changes due to any PR or commit, and to track performance changes over time. 

### Further details

A [small benchmark suite](https://github.com/cvxpy/cvxpy/blob/master/cvxpy/tests/test_benchmarks.py) already exists for CVXPY. The suite measures both the time to compile a problem into the solver standard form, and the time spent in the solver. We are focused on the former. The benchmark suite needs to be extended substantially, with a wider range of problems. We are particularly concerned about measuring performance for standard problem formats (e.g., quadratic programs) and measuring how well CVXPY scales to larger problems (>1e5 variables or constraints).

### Helpful experience

- Familiarity with Python benchmarking.
- Familiarity with CI tools such as Github Actions.

### Steps

**Initial steps**

- Study the [existing benchmark suite](https://github.com/cvxpy/cvxpy/blob/master/cvxpy/tests/test_benchmarks.py).
- Study tools for benchmarking with CI.

**Expected outcomes**

- An expanded benchmark suite, sufficient to provide confidence that we are accurately measuring changes in performance.
- Benchmarking CI, or some equivalent system for tracking performance changes across commits.

**Stretch goals**

- Help speed up CVXPY problem compilation.
