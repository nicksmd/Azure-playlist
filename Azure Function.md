##### How to install external Python package to Azure function?

- Create an virtual environment:
  - Open a Kudu console, choose Powershell
  - Go to the folder your your script (should be D:/home/site/wwwroot/NameOfMyFunction)
  - **python -m virtualenv myvenv** to create virtual env
  - **cd myenv/Scripts** and call activate.bat by **.\activate.ps1** to active the virtual env  
  
  After this step, the shell should become: **PS>** instead of **PS**
- Install packages:
  - update pip: **python -m pip install -U pip** or **python -m pip install pip==<version>**
  - install desired package: for example: **python -m pip install numpy**
  - add the following lines to your function:
  
  ```Python
  import sys, os.path
  sys.path.append(os.path.abspath(os.path.join(os.path.dirname( __file__ ), 'myvenv/Lib/site-packages')))
  ```
