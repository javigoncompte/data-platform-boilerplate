# Boilerplate Monorepo for Data Platforms

## Requirements
- uv 
- ruff
- hatch

## Layout
``` bash
➜ tree .
.
├── LICENSE
├── README.md
├── dist
├── libs
│   ├── client
│   │   ├── README.md
│   │   ├── data_platform
│   │   │   └── client
│   │   │       ├── __init__.py
│   │   │       └── py.typed
│   │   └── pyproject.toml
│   ├── connection
│   │   ├── README.md
│   │   ├── data_platform
│   │   │   └── connection
│   │   │       ├── __init__.py
│   │   │       └── py.typed
│   │   └── pyproject.toml
│   ├── ingestion
│   │   ├── README.md
│   │   ├── data_platform
│   │   │   └── ingestion
│   │   │       ├── __init__.py
│   │   │       └── py.typed
│   │   └── pyproject.toml
│   ├── interfaces
│   │   ├── README.md
│   │   ├── data_platform
│   │   │   └── interfaces
│   │   │       ├── __init__.py
│   │   │       └── py.typed
│   │   └── pyproject.toml
│   └── transformations
│       ├── README.md
│       ├── data_platform
│       │   └── transformations
│       │       ├── __init__.py
│       │       └── py.typed
│       └── pyproject.toml
├── projects_data_engineering
│   └── x_domain
│       └── albatros
│           ├── data_platform
│           │   ├── albatros
│           │   │   ├── __init__.py
│           │   │   └── py.typed
│           │   └── py.typed
│           ├── dist
│           │   ├── albatros-0.1.0-py3-none-any.whl
│           │   └── albatros-0.1.0.tar.gz
│           ├── pyproject.toml
│           └── tests
│               └── test_albatros_import.py
├── pyproject.toml
└── uv.lock
```
## Understanding Layout

### Libraries

* libraries setting up libs that are going to be used by other projects or packages these are initialized using uv
    - uv run una create package client libs/
    - or copy paste client

### Projects_*

* These are projects in different aspects of a data platform with data engineering, machine learning and llm/ai

#### Creating a package in a project

* If using domains such as product/sales
    1. Go to project create a folder of the domain name ex: x_domain
    2. Create the package folder name ex: albatross
    3. uv run una create package albatros projects_data_engineering/x_domain/

* If not using a domain and instead directly just package names
    1. Go to a project
    2. create folder name of package name
    3. uv run una create package albatros projects_data_engineering/

* We are using uv una to handle the wheel building using external libs since uv worskpaces doesn't support for the moment
https://una.rdrn.me/quickstart/
