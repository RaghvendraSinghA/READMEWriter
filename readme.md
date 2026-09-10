# JavaScript Drills

This project contains JavaScript problems on a car inventory which have 50 cars.We have to solve some given problems.

## Project Structure


- `data/data.js` contains the data used by the tests files while calling problem specific function from problems.
- `problems/` contains the functions which solves the specific problem.
- `tests/` contains files that import the data from data.js and function from `problems/`.


## Prerequisites

Make sure Node.js is installed.

Check the Node.js version:

```bash
node --version
```

## Run the Problems

First, move to the project root:

```bash
cd js-drills/drill-1
```

Then, Execute Using Test Files

Internally the `tests/` files import the functions from the corresponding files from problems folder and execute them.     

Just run test files to execute problems.

For example:

```bash
node tests/testProblem1.js
```

Similarly:

```bash
node tests/testProblem2.js
node tests/testProblem3.js
```
