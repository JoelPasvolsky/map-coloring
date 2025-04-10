[![Open in GitHub Codespaces](
  https://img.shields.io/badge/Open%20in%20GitHub%20Codespaces-333?logo=github)](
  https://codespaces.new/dwave-examples/map-coloring?quickstart=1)
[![Linux/Mac/Windows build status](
  https://circleci.com/gh/dwave-examples/map-coloring.svg?style=shield)](
  https://circleci.com/gh/dwave-examples/map-coloring)

# Map Coloring

A demo on using the D-Wave Ocean SDK to solve the map coloring problem. Namely,
given a map, color the regions of the map such that no two regions sharing a
border would share the same color.

![Graph](graph.png)

A graph representation of the provinces of Canada. Provinces connected by edges
share a border together. This is a sample output produced by this demo.

## Installation

You can run this example without installation in cloud-based IDEs that support
the [Development Containers specification](https://containers.dev/supporting)
(aka "devcontainers") such as GitHub Codespaces.

For development environments that do not support `devcontainers`, install
requirements:

```bash
pip install -r requirements.txt
```

If you are cloning the repo to your local system, working in a
[virtual environment](https://docs.python.org/3/library/venv.html) is
recommended.

## Usage

Your development environment should be configured to access the
[Leap&trade; Quantum Cloud Service](https://docs.dwavequantum.com/en/latest/ocean/sapi_access_basic.html).
You can see information about supported IDEs and authorizing access to your Leap
account [here](https://docs.dwavequantum.com/en/latest/leap_sapi/dev_env.html).

Simply run the code with

```bash
python map_coloring.py
```

## Code Overview

The idea is to describe the map coloring problem in terms of constraints.
Once this is done, we can use tools from the Ocean SDK to convert these
constraints into a binary quadratic model (BQM), a type of equation that can be
ingested by the quantum computer. Afterwards, we will hopefully have a solution
to our map coloring problem.

Constraints to describe the map coloring problem:

* Each region can only select one color
* No regions sharing a border can share a color

## Code Specifics

### Why only four colors?

* In the code, we let each of the regions choose one among four colors. Why
  are we limiting ourselves to only four colors? According to the [Four Colour
  Theorem](https://en.wikipedia.org/wiki/Four_color_theorem), we need no more
  than four colors to color any planar map such that no two adjacent regions
  share the same color

### Alternative implementation

* To solve the map coloring problem, in this demo, we are forming constraints,
  converting said constraints into a BQM, and then feeding said BQM to a solver.
  Please note, however, that the D-Wave Ocean stack also has a function called
  [min_vertex_color_qubo(..)][1] that will directly form the map coloring BQM
  for you.

## License

Released under the Apache License 2.0. See [LICENSE](./LICENSE) file.

[1]: https://docs.dwavequantum.com/en/latest/ocean/api_ref_dnx/generated/dwave_networkx.algorithms.coloring.min_vertex_color_qubo.html