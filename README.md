# MCDA Research Ecosystem

A cross-language software ecosystem for **Multi-Criteria Decision Analysis (MCDA)** research, combining Python and TypeScript/JavaScript implementations.

This repository brings together two complementary MCDA libraries as Git submodules:

- **[pyrepo-mcda](https://github.com/energyinpython/pyrepo-mcda)** — a Python library for MCDA, suitable for scientific computing, data analysis, and systematic computational experiments.
- **[MCDA.js](https://github.com/mcdait/mcda.js)** — an object-oriented MCDA library for TypeScript and JavaScript, suitable for integration into web applications and interactive decision-support tools.

The two implementations provide a shared methodological foundation for MCDA research across different programming environments.

## Repository structure

```text
mcda-research/
├── python/       # Python implementation - pyrepo-mcda git submodule
├── typescript/   # TS/JS implementation - MCDA.js Git submodule
├── .gitignore
├── .gitmodules
└── README.md
```

## Citing this software

If you use this software in your research, please cite the following paper:

[Version [1.4]- [pyrepo-mcda - reference objects based MCDA software package]](https://doi.org/10.1016/j.softx.2026.102896)

Or using Bitbtex:

DOI: [https://doi.org/10.1016/j.softx.2026.102896](https://doi.org/10.1016/j.softx.2026.102896)

```bibtex
@article{KARCZMARCZYK2026102896,
title = {Version [1.4]- [pyrepo-mcda - reference objects based MCDA software package]},
journal = {SoftwareX},
volume = {35},
pages = {102896},
year = {2026},
issn = {2352-7110},
doi = {https://doi.org/10.1016/j.softx.2026.102896},
url = {https://www.sciencedirect.com/science/article/pii/S2352711026003870},
author = {Artur Karczmarczyk and Aleksandra Bączkiewicz and Jarosław Wątróbski and Wojciech Sałabun},
keywords = {Multi-criteria decision analysis (MCDA), Strong sustainability paradigm (SSP), PROMETHEE II, Temporal decision analysis, Decision support systems (DSS), Python software}
}
```


## Getting started

### 1. Clone the repository

Clone this repository together with its submodules:

```bash
git clone --recurse-submodules https://github.com/mcdait/mcda-research.git
cd mcda-research
```

If you have already cloned the repository without its submodules, initialize them with:

```bash
git submodule update --init --recursive
```

The submodules are checked out at the revisions recorded by the main repository. To update them to the revisions referenced by the current main-repository configuration, run:

```bash
git submodule update --init --recursive
```

### 2. Choose an implementation

You can use either library independently. Installing both is not required.

## Python: pyrepo-mcda

### Installation

Python 3.10 or later is required. It is recommended to use a virtual environment.

Create and activate a virtual environment:

```bash
python -m venv .venv
```

On Windows:

```powershell
.venv\Scripts\Activate.ps1
```

On Linux or macOS:

```bash
source .venv/bin/activate
```

Install the published package:

```bash
python -m pip install pyrepo-mcda
```

### Quick start

The following example evaluates three alternatives using the TOPSIS method:

```python
import numpy as np

from pyrepo_mcda.mcda_methods import TOPSIS
from pyrepo_mcda import distance_metrics as dists
from pyrepo_mcda import normalizations as norms
from pyrepo_mcda.additions import rank_preferences

matrix = np.array([
    [1, 7, 3],
    [2, 5, 6],
    [4, 3, 8],
])

weights = np.array([1 / 3, 1 / 3, 1 / 3])
types = np.array([1, -1, 1])

method = TOPSIS(
    normalization_method=norms.vector_normalization,
    distance_metric=dists.euclidean,
)

scores = method(matrix, weights, types)
ranking = rank_preferences(scores, reverse=True)

print("Scores:", scores)
print("Ranking:", ranking)
```

In this example, `1` denotes a benefit criterion and `-1` denotes a cost criterion. Criterion weights should sum to 1. The ranking is obtained by sorting preference values in descending order.

### Python resources

- Source code: [pyrepo-mcda on GitHub](https://github.com/energyinpython/pyrepo-mcda)
- Full documentation: [pyrepo-mcda documentation](https://pyrepo-mcda.readthedocs.io/en/latest/)
- Installation package: [pyrepo-mcda on PyPI](https://pypi.org/project/pyrepo-mcda/)

## TypeScript/JavaScript: MCDA.js

### Installation

MCDA.js is distributed through npm as `mcdajs`. Install it in your existing Node.js project:

```bash
npm install mcdajs
```

Other supported package managers include Yarn, pnpm, and Bun.

### Quick start

The following TypeScript example defines a decision problem and retrieves its preference scores:

```typescript
import {
  TopsisDecisionProblem,
  CriterionType,
  rank,
} from "mcdajs";

const problem = new TopsisDecisionProblem();

problem.matrix = [
  [1, 7, 3],
  [2, 5, 6],
  [4, 3, 8],
];

problem.weights = [1 / 3, 1 / 3, 1 / 3];

problem.types = [
  CriterionType.BENEFIT,
  CriterionType.COST,
  CriterionType.BENEFIT,
];

problem.alternatives = ["A1", "A2", "A3"];
problem.criteria = ["C1", "C2", "C3"];

const scores = problem.scores;
const ranking = rank(scores);

console.log("Scores:", scores);
console.log("Ranking:", ranking);
```

The decision matrix contains alternatives in rows and criteria in columns. Criterion types indicate whether a criterion is to be maximized or minimized. The `scores` property provides the calculated preference values, while `rank()` converts them into a ranking.

### TypeScript/JavaScript resources

- Source code and examples: [MCDA.js on GitHub](https://github.com/mcdait/mcda.js)
- Installation package: [mcdajs on npm](https://www.npmjs.com/package/mcdajs)
- Usage examples and API details: see the [MCDA.js README](https://github.com/mcdait/mcda.js#readme)

## Research workflow and cross-language use

The ecosystem supports MCDA research in two complementary environments:

- **Python** can be used for data preparation, numerical experiments, statistical analysis, and sensitivity or robustness studies.
- **TypeScript/JavaScript** can be used to build interactive interfaces, explore decision scenarios, and integrate MCDA methods into web-based decision-support applications.
