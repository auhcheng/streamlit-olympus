# Phoenics

[![Build Status](https://travis-ci.com/FlorianHase/phoenics.svg?token=rULvnKYmWdFF3JqQBVVW&branch=master)](https://travis-ci.com/FlorianHase/phoenics)

Phoenics is an open source optimization algorithm combining ideas from Bayesian optimization with Bayesian Kernel Density estimation [1]. It performs global optimization on expensive to evaluate objectives, such as physical experiments or demanding computations.

Check out the `examples` folder for detailed descriptions and code examples for:

| Example | Link |
|:--------|:-----|
| Sequential optimization           |  [examples/optimization_sequential](https://github.com/chemos-inc/phoenics/tree/master/examples/optimization_sequential)  |


# Installation

## Environment (Optional)

We suggest to create a new environment for the installation of Phoenics to avoid any compatibility issues with pre-existing python packages. This is optional, but recommended.

This can be done with Venv or Anaconda.

### Venv
Create the virtual environment:
```bash
python -m venv venv
```
Activate (Unix):
```bash
source venv/bin/activate
```
Activate (Windows):
```bash
.\venv\Scripts\activate
```

A `venv` folder will be created in the current directory and the virtual enviroment will be activated.

Note: Edward backend requires Python 3.6 in order to install all needed dependencies. Python version can be specified as follow:

```bash
python3.6 -m venv venv
```


### Anaconda

```bash
conda create --name venv
conda activate venv
```

Note: Edward backend requires Python 3.6 in order to install all needed dependencies. Python version can be specified as follow:

```bash
conda create --name venv python=3.6
```

## Phoenics as pip module

Phoenics can be installed directly with pip:

```bash
apt-get install python-pip
python -m pip install phoenics
```

## Phoenics from source

Phoenics can also be installed from source. This way allows anyone to make and test changes on the code.
```bash
git clone https://github.com/chemos-inc/phoenics.git
cd phoenics
python -m pip install -U pip
python -m pip install -r requirements.txt
python -m pip install -e .
```

# Dependencies and requirements

This code has been tested with Python 3.6 and 3.7 on Unix platforms and on Windows 10.

## PIP
 It requires the following `pip` packages:
* numpy
* pyyaml >= 5.1
* sqlalchemy >= 1.3
* watchdog >= 0.9
* wheel >= 0.33

These will be automatically installed by running the `setup.py` or by installing Phoenics as a pip module.

## Windows
Requirements for Windows:
*  `Microsoft C++ Build Tools` ([Download Link](https://visualstudio.microsoft.com/visual-cpp-build-tools/))
*  64-bit version of Python ([Python 3.6.8 64 bit installer](https://www.python.org/ftp/python/3.6.8/python-3.6.8-amd64.exe))

## Backend
Phoenics requires additional modules for the backend of its Bayesian Neural Network. Two options are currently supported: `tensorflow-probability` and `edward`.
### Tensorflow probability
To use this backend, specify it in the configuration file:
```json
"backend": "tfprob"
```
Install it with:
```bash
python -m pip install tensorflow==1.15
python -m pip install tensorflow-probability==0.8.0
```
Note: A warning will be generated if a version lower than 41.0.0 of `setuptools` is installed. To fix the warning run:
```bash
python -m pip install setuptools==41.0.0
```
### Edward
To use this backend, specify it in the configuration file:
```json
"backend": "edward"
```
Install it with:
```bash
python -m pip install edward==1.3.5
python -m pip install tensorflow==1.4.1
```

Note: `tensorflow==1.4.1` can not be installed with Python 3.7+.

# Run the example

```bash
git clone git@github.com:chemos-inc/phoenics.git
cd phoenics
python -m venv venv
source venv/bin/activate # on Windows: .\venv\Scripts\activate
python -m pip install -U pip
python -m pip install setuptools==41.0.0
python -m pip install -r requirements.txt
python -m pip install tensorflow==1.15
python -m pip install tensorflow-probability==0.8.0
python -m pip install -e .
cd examples/optimization_sequential/
python ./optimize_branin.py
```

# Using Phoenics

Phoenics is designed to suggest new parameter points based on prior observations. The suggested parameters can then be passed on to objective evaluations (experiments or involved computation). As soon as the objective values have been determined for a set of parameters, these new observations can again be passed on to Phoenics to request new, more informative parameters.

```python
from phoenics import Phoenics

# create an instance from a configuration file
config_file = 'config.json'
phoenics    = Phoenics(config_file)

# request new parameters from a set of observations
params      = phoenics.recommend(observations = observations)
```
Detailed examples for specific applications are presented in the `examples` folder.

### Disclaimer

Note: This repository is under construction! We hope to add further details on the method, instructions and more examples in the near future.

### Experiencing problems?

Please create a [new issue](https://github.com/chemos-inc/phoenics/issues/new/choose) and describe your problem in detail so we can fix it.

### References

[1] H??se, F., Roch, L. M., Kreisbeck, C., & Aspuru-Guzik, A. [Phoenics: A Bayesian Optimizer for Chemistry.](https://pubs.acs.org/doi/abs/10.1021/acscentsci.8b00307) ACS central science 4.6 (2018): 1134-1145.
