## Day01 - Create a Python Virtual Environment for ML 

The xFusionCorp Industries data science team needs a standardised Python environment for their new ML project. Set up a virtual environment with the
required ML libraries on the `controlplane` host.


1) Create a Python virtual environment named `ml-env` under `/root/code/` using `python3 -m venv`.

2) Activate the environment and install the following packages: `numpy`, `pandas`, `scikit-learn`, and `matplotlib`.

3) Generate a `requirements.txt` file using `pip freeze` and save it at `/root/code/requirements.txt`.

## Answer: 

Step01: Create python virtual environment named 'ml-env' under '/root/code' directory
```
python3 -m venv /root/code/ml-env 
````  

Step02: Activate the python environment and install numpy, pandas, scikit-learn and matplotlib 
```
source /root/code/ml-env/bin/activate

pip install numpy pandas scikit-learn matplotlib
```

Step03: Create a requirment.txt file under the root/code directory
```
pip freeze > /root/code/requirement.txt
```

### Task is Completed!
