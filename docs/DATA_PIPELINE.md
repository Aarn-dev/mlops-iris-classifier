
# Data Pipeline Documentation

## Pipeline Stages

| Stage | Purpose | Input | Output |
|---|---|---|---|
| Collect | Obtain raw Iris data | sklearn Iris dataset | iris_raw.csv |
| Preprocess | Clean data | iris_raw.csv | iris_preprocessed.csv |
| Feature Engineering | Create useful features | iris_preprocessed.csv | iris_features.csv |
| Validate | Check schema, nulls and ranges | iris_features.csv | Validation result |

## Pipeline Flow

```text
Collect
   |
   v
Preprocess
   |
   v
Feature Engineering
   |
   v
Validate
```

## Validation Rules

1. All expected columns must be present.
2. No unexpected null values are allowed.
3. Species must be setosa, versicolor, or virginica.
4. Numeric features must be within expected ranges.

## DVC Automation

The pipeline is defined in dvc.yaml.

DVC tracks dependencies and outputs and generates dvc.lock
after a successful pipeline execution.

The dvc repro command reruns stages when their dependencies
change and skips unchanged stages when possible.