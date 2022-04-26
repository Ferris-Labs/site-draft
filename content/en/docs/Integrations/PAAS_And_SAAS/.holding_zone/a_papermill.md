---
title: "papermill"
linkTitle: "papermill"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     papermill Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.papermill"></a>

# operators.papermill

<a id="operators.papermill.NoteBook"></a>

## NoteBook Objects

```python
@attr.s(auto_attribs=True)
class NoteBook(File)
```

Jupyter notebook

<a id="operators.papermill.PapermillOperator"></a>

## PapermillOperator Objects

```python
class PapermillOperator(BaseOperator)
```

Executes a jupyter notebook through papermill that is annotated with parameters

**Arguments**:

- `input_nb`: input notebook (can also be a NoteBook or a File inlet)
- `output_nb`: output notebook (can also be a NoteBook or File outlet)
- `parameters`: the notebook parameters to set
- `kernel_name`: (optional) name of kernel to execute the notebook against
(ignores kernel name in the notebook document metadata)

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_papermill"></a>

# example\_dags.example\_papermill

This DAG will use Papermill to run the notebook "hello_world", based on the execution date
it will create an output notebook "out-<date>". All fields, including the keys in the parameters, are
templated.

<a id="example_dags.example_papermill.check_notebook"></a>

#### check\_notebook

```python
@task
def check_notebook(inlets, execution_date)
```

Verify the message in the notebook

