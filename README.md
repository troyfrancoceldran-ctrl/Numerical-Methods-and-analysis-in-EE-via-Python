# Numerical Methods in Python

![tests](https://github.com/troyfrancoceldran-ctrl/numerical-methods-python/actions/workflows/tests.yml/badge.svg)

From-scratch implementations of root-finding, linear-system and nonlinear-system solvers in Python, cross-checked against NumPy and SciPy and applied to small battery, circuit and network problems.

> **Status:** the solvers, tests and starter notebooks run. The written observations in each notebook are still to be completed. [Update this line as you finish them.]

## Where this comes from

I learned these methods in a Numerical Methods course (EEE102) at Mindanao State University - Iligan Institute of Technology. This repository contains no course handouts, problem statements, diagrams, grading rubrics or exam material, and its example problems are original.

## Methods

- **Root-finding:** bisection, secant, Newton-Raphson
- **Linear systems:** Gaussian elimination with partial pivoting, determinant, inverse and 1-norm condition number
- **Nonlinear systems:** Newton's method with an analytic or finite-difference Jacobian and an optional backtracking line search

The solvers do not call SciPy. SciPy and NumPy appear only in the tests and notebooks, as independent references.

## Notebooks

| # | Notebook | Method | Problem (original) |
|---|----------|--------|--------------------|
| 01 | `01_bisection.ipynb` | Bisection | State of charge from an open-circuit-voltage model (illustrative, not a fitted cell) |
| 02 | `02_secant.ipynb` | Secant | Operating point of a series diode circuit |
| 03 | `03_newton_raphson.ipynb` | Newton-Raphson | The same SOC inversion, convergence order, and two failure cases |
| 04 | `04_linear_systems.ipynb` | Gaussian elimination | Node voltages of a resistor network; pivoting; Hilbert-matrix conditioning |
| 05 | `05_nonlinear_systems.ipynb` | Newton for systems | A two-diode network; analytic vs finite-difference Jacobian; damping |

Each notebook ends with an **Observations** cell. Those are meant to be written from your own plots and numbers.

## Results

[After you run the notebooks, summarize what you found here in your own words: convergence rates you measured, where methods failed, and what surprised you.]

## Quick start

```bash
git clone https://github.com/troyfrancoceldran-ctrl/numerical-methods-python.git
cd numerical-methods-python
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt  # installs the dependencies and the nummeth package
pytest                           # runs the test suite
jupyter lab                      # then open the notebooks/ folder
```

Python 3.10 or newer.

## Repository layout

```
numerical-methods-python/
├── README.md
├── LICENSE
├── pyproject.toml
├── requirements.txt
├── notebooks/        # one notebook per method
├── src/nummeth/      # rootfinding.py, linsys.py, nonlinear.py
├── tests/            # pytest checks against SciPy and NumPy
└── .github/workflows/tests.yml
```

## Testing

The test suite checks, among other things:

- bisection's iteration count against its theoretical bound, and its refusal to run without a sign change
- Newton's quadratic convergence on a simple root, and its divergence on a cube root
- Gaussian elimination against `numpy.linalg.solve`, and a case that fails without pivoting
- the Newton system solver against SciPy and against an independent one-dimensional reduction

## Known limitations

- Dense matrices only, written with plain Python loops, so it is slow beyond a few hundred unknowns.
- The singular-matrix test uses a pivot tolerance relative to each row, so a severely ill-conditioned matrix (a Hilbert matrix of size 12, for example) is rejected as singular.
- Newton's method can still fail from a poor start. Damping helps from some starting points and not others (see notebook 05).

## Use of AI tools

The initial code scaffold (package structure, solvers, tests and starter notebooks) was generated with an AI assistant (Claude, Anthropic). [Describe what you then read, ran, changed and verified yourself, and which parts of the observations are your own, in line with the MSU Policy on the Fair and Ethical Use of AI and Its Applications.]

## Acknowledgments

The EEE102 course at MSU-IIT introduced these methods. 
## License

MIT License (see `LICENSE`).

## Contact

Troy Franco G. Celdran - [LinkedIn](https://www.linkedin.com/in/troy-franco-celdran-aa614838a/) - [GitHub](https://github.com/troyfrancoceldran-ctrl)
