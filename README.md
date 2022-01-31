# GSOC2022

CVXPY is an open source Python-embedded modeling language for convex optimization problems. 
It lets you express your problem in a natural way that follows the math, 
rather than in the restrictive standard form required by solvers.

[CVXPY](https://www.cvxpy.org/) will be a participating sub-organization in [NumFOCUS](http://numfocus.org/)'s application
for [Google Summer of Code 2022](https://summerofcode.withgoogle.com/). For more information about this application see:

- [NumFOCUS's main GSoC page](https://github.com/numfocus/gsoc)

## Mentors

- [Steven Diamond](https://github.com/SteveDiamond)
- [Akshay Agrawal](https://github.com/akshayka)
- [Riley Murray](https://github.com/rileyjmurray)
- [Bartolomeo Stellato](https://github.com/bstellato)

## Ideas

### Performance benchmarks with continuous integration \[Medium\]

#### Abstract

Improving the speed of problem compilation is a major development goal for CVXPY. We need a thorough benchmark suite to measure improvements, ideally deployed via continuous integration (CI). It should be easy to see the performance changes due to any PR or commit, and to track performance changes over time. 

#### Further details

A [small benchmark suite](https://github.com/cvxpy/cvxpy/blob/master/cvxpy/tests/test_benchmarks.py) already exists for CVXPY. The suite measures both the time to compile a problem into the solver standard form, and the time spent in the solver. We are focused on the former. The benchmark suite needs to be extended substantially, with a wider range of problems. We are particularly concerned about measuring performance for standard problem formats (e.g., quadratic programs) and measuring how well CVXPY scales to larger problems (>1e5 variables or constraints).

#### Helpful experience

- Familiarity with Python benchmarking.
- Familiarity with CI tools such as Github Actions.

#### Steps

**Initial steps**

- Study the [existing benchmark suite](https://github.com/cvxpy/cvxpy/blob/master/cvxpy/tests/test_benchmarks.py).
- Study tools for benchmarking with CI.

**Key deliverables**

- An expanded benchmark suite, sufficient to provide confidence that we are accurately measuring changes in performance.
- Benchmarking CI, or some equivalent system for tracking performance changes across commits.

**Stretch goals**

- Help speed up CVXPY problem compilation.

### Support for nonlinear problems \[Medium\]

#### Abstract

CVXPY currently supports convex optimization problems and mixed-integer programs. We would like to extend support to (nonconvex) nonlinear problems, 
such as those solved by [Ipopt](https://coin-or.github.io/Ipopt/) or [Bonmin](https://github.com/coin-or/Bonmin).

#### Further details

#### Helpful experience

- Familiarity with convex optimization.
- Familiarity with nonlinear optimization.

#### Steps

**Initial steps**

**Key deliverables**

**Stretch goals**
