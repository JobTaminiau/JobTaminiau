---
title: "Use NREL SAM on Google Colab"
date: 2021-09-24T13:53:30-04:00
categories:
  - Scripts
tags:
  - python_code
  - Google Colab
  - NREL SAM
---
As part of my research projects, I often rely on NREL's PV SAM to model solar energy performance. This post describes the use of the software on Google Colab.

```python
# install PV SAM
!pip install nrel-pysam

# load PVSAM
import PySAM.Pvwattsv7 as pv

# Create new model
new_model = pv.new()
print(type(new_model))
new_model.export()

# list model configurations
help(pv.default)
```
