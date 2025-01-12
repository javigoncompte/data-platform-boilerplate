# Boilerplate Monorepo for Data Platforms

## Requirements
- uv 
- ruff
- hatch

## Layout
.
├── LICENSE
├── README.md
├── libraries
│   ├── client
│   │   ├── README.md
│   │   ├── pyproject.toml
│   │   └── src
│   │       └── client
│   │           ├── __init__.py
│   │           └── py.typed
│   ├── connection
│   │   ├── README.md
│   │   ├── pyproject.toml
│   │   └── src
│   │       └── connection
│   │           ├── __init__.py
│   │           └── py.typed
│   ├── ingestion
│   │   ├── README.md
│   │   ├── pyproject.toml
│   │   └── src
│   │       └── ingestion
│   │           ├── __init__.py
│   │           └── py.typed
│   ├── interfaces
│   │   ├── README.md
│   │   ├── pyproject.toml
│   │   └── src
│   │       └── interfaces
│   │           ├── __init__.py
│   │           └── py.typed
│   └── transformations
│       ├── README.md
│       ├── pyproject.toml
│       └── src
│           └── transformations
│               ├── __init__.py
│               └── py.typed
├── projects_data_engineering
│   └── x_domain
│       └── albatross
│           ├── README.md
│           ├── pyproject.toml
│           └── src
│               └── albatross
│                   └── __init__.py
├── projects_llm_ai
├── projects_machine_learning
├── pyproject.toml
└── uv.lock

## Understanding Layout

### Libraries

* libraries setting up libs that are going to be used by other projects or packages these are initialized using uv
    - uv init --lib

### Projects_*

* These are projects in different aspects of a data platform with data engineering, machine learning and llm/ai

#### Creating a package in a project

* If using domains such as product/sales
    1. Go to project create a folder of the domain name ex: x_domain
    2. Create the package folder name ex: albatross
    3. uv init --package

* If not using a domain and instead directly just package names
    1. Go to a project
    2. create folder name of package name
    3. uv init --package