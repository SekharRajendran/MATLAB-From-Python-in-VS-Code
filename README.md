# MATLAB Engine for Python Setup in VS Code

This guide explains how to set up Python 3.12 in VS Code and connect it to MATLAB using MATLAB Engine for Python.

## Goal

After setup, you should be able to run a Python script from VS Code that starts MATLAB and calls MATLAB functions.

Example:

```python
import matlab.engine

eng = matlab.engine.start_matlab()
print(eng.sqrt(25.0))
eng.quit()
```

Expected output:

```text
5.0
```

## 1. Install Python from VS Code Terminal

Open VS Code.

Go to:

```text
Terminal > New Terminal
```

Run this in the VS Code terminal:

```powershell
winget install Python.Python.3.12
```

After installation, close the VS Code terminal and open a new one.

Check Python:

```powershell
py -3.12 --version
```

Check pip:

```powershell
py -3.12 -m pip --version
```

Check that Python is 64-bit:

```powershell
py -3.12 -c "import sys; print(sys.maxsize > 2**32)"
```

Expected output:

```text
True
```

## 2. Check MATLAB Version

Open MATLAB.

Run this in the MATLAB Command Window:

```matlab
version
```

Also run:

```matlab
matlabroot
```

This shows where MATLAB is installed.

Python 3.12 works with newer MATLAB releases such as R2024b or newer. If your MATLAB release is older, you may need Python 3.11 instead.

## 3. Install MATLAB Engine for Python

This step is done inside MATLAB, not inside the VS Code terminal.

In the MATLAB Command Window, run:

```matlab
cd(fullfile(matlabroot,"extern","engines","python"))
system("py -3.12 -m pip install .")
```

This installs MATLAB Engine into your Python 3.12 environment.

## 4. Test MATLAB Engine from VS Code Terminal

Go back to VS Code.

Open a new terminal.

Run:

```powershell
py -3.12 -c "import matlab.engine; eng = matlab.engine.start_matlab(); print(eng.sqrt(25.0)); eng.quit()"
```

Expected output:

```text
5.0
```

If this works, MATLAB Engine is installed correctly.

## 5. Create a Python Test Script

Create a new file in VS Code called:

```text
test_matlab_engine.py
```

Put this code inside:

```python
import matlab.engine

eng = matlab.engine.start_matlab()

print("MATLAB started successfully")
print("MATLAB version:", eng.version())
print("sqrt(25) =", eng.sqrt(25.0))

eng.quit()
```

Save the file.

Run it from the VS Code terminal:

```powershell
py -3.12 test_matlab_engine.py
```

Expected output should look similar to:

```text
MATLAB started successfully
MATLAB version: 24.x or 25.x
sqrt(25) = 5.0
```

## 6. Install Other Python Packages

Use this format in the VS Code terminal:

```powershell
py -3.12 -m pip install package_name
```

Example:

```powershell
py -3.12 -m pip install numpy scipy pandas matplotlib
```

To see installed packages:

```powershell
py -3.12 -m pip list
```

## 7. Optional: Let MATLAB Use This Same Python

This step is needed only if you want MATLAB to call Python.

First, get the Python path from the VS Code terminal:

```powershell
py -3.12 -c "import sys; print(sys.executable)"
```

Copy the printed path.

Then open MATLAB and run this in the MATLAB Command Window:

```matlab
pyenv("Version","PASTE_YOUR_PYTHON_PATH_HERE")
pyenv
```

Example:

```matlab
pyenv("Version","C:\Users\YourName\AppData\Local\Programs\Python\Python312\python.exe")
pyenv
```

## 8. Add Python Interpreter in VS Code

At the end, tell VS Code which Python to use.

Open VS Code.

Press:

```text
Ctrl + Shift + P
```

Search for:

```text
Python: Select Interpreter
```

Select the Python 3.12 interpreter.

It will usually look like one of these:

```text
Python 3.12.x
```

or:

```text
C:\Users\YourName\AppData\Local\Programs\Python\Python312\python.exe
```

After selecting it, open a new VS Code terminal and check:

```powershell
python --version
```

or:

```powershell
py -3.12 --version
```

## 9. Common Problems

### Problem: No module named matlab.engine

Run this again in the MATLAB Command Window:

```matlab
cd(fullfile(matlabroot,"extern","engines","python"))
system("py -3.12 -m pip install .")
```

Then test again from VS Code terminal:

```powershell
py -3.12 -c "import matlab.engine; print('MATLAB Engine found')"
```

### Problem: Python version not supported

Check your MATLAB release.

If your MATLAB release does not support Python 3.12, install Python 3.11:

```powershell
winget install Python.Python.3.11
```

Then install MATLAB Engine using:

```matlab
cd(fullfile(matlabroot,"extern","engines","python"))
system("py -3.11 -m pip install .")
```

### Problem: VS Code is using the wrong Python

In VS Code:

```text
Ctrl + Shift + P
Python: Select Interpreter
```

Choose Python 3.12.

Then run:

```powershell
py -3.12 test_matlab_engine.py
```

Using `py -3.12` makes sure the script runs with Python 3.12.
# MATLAB-From-Python-in-VS-Code
Setting up MATLAB Engine in python with VS Code
