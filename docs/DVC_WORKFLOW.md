# DVC Workflow Documentation

## Overview

This document describes the DVC workflow used for dataset tracking and versioning in the MLOps Iris Classifier project.

## DVC Remote Configuration

A local folder was configured as the default DVC remote:

`~/dvc-remote-storage`

The remote was configured using:

```bash
dvc remote add -d myremote ~/dvc-remote-storage
```

## Dataset Versioning Workflow

For every dataset change, the following workflow was followed:

1. Modify or generate the dataset.
2. Track the dataset using DVC:

```bash
dvc add data/raw/iris_v1.csv
```

3. Add the DVC metadata file to Git:

```bash
git add data/raw/iris_v1.csv.dvc
```

4. Commit the dataset metadata:

```bash
git commit -m "data: dataset version update"
```

5. Upload the actual dataset to the DVC remote:

```bash
dvc push
```

## Dataset Version Comparison

Dataset versions were compared using:

```bash
dvc diff <commit-hash>
```

Git history was used to identify dataset versions:

```bash
git log --oneline -- data/raw/iris_v1.csv.dvc
```

## Restoring Dataset Versions

An older DVC metadata file was restored using:

```bash
git checkout <commit-hash> -- data/raw/iris_v1.csv.dvc
```

The actual dataset was then restored using:

```bash
dvc checkout data/raw/iris_v1.csv.dvc
```

The latest dataset version can be restored by returning to the latest DVC metadata file and running `dvc checkout` again.

## Conclusion

DVC allows large datasets to be versioned efficiently while Git tracks lightweight metadata files. This provides reproducibility by connecting specific code versions with specific dataset versions.
