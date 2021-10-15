# SET UP SYSTEM TO ACCESS STORE REMOTELY

Before you proceed, make sure you have login rights as an NBP student and access to /net/store

### STEPS TO CONNECT TO `/net/store/` remotely

Open terminal on macOS or Linux
```
ssh <rzlogin>@gate.ikw.uos.de
```
enter your password when prompted.


### STEPS TO INSTALL PYTHON3 without sudo access
Only `python 2.7` is installed on the remote computer and you do not have sudo access to install `python3`

In the next steps, you will install `python 3` from source. Type the following to install python for your remote computer:

```
cd ~
wget https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-pypy3-Linux-x86_64.sh -O ~/mambaforge/mambaforge.sh
bash ~/mambaforge/mambaforge.sh
```
(I used mambaforge, but you can try this with miniconda3 as well)

RESTART TERMINAL and use ssh to login to `gate.ikw.uos.de`

Check python version and path
```bash
python -V
echo $PATH
```
make sure the path looks something like this:

```bash
/net/home/student/***/mambaforge-pypy3/bin:/net/home/student/***/mambaforge-pypy3/condabin:
```
if not set path by:

```bash
export PATH="/net/home/student/***/mambaforge-pypy3/condabin:$PATH"
export PATH="/net/home/student/***/mambaforge-pypy3/bin/:$PATH"
```
then check PATH again

Your terminal would also look something like this:
```bash
(base)<rzlogin>@gate:~$
```

### CREATE CONDA VIRTUAL ENVIRONMENT

To create a new virtual environment, type:
```bash
conda create --name my_env
```
Activate your virtual environment:
```bash
conda activate my_env
```
Your terminal would now look like this:
```bash
(my_env)<rzlogin>@gate:~$
```
For more info on how to customize your virtual environment use the cheatsheet [**here**](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf)

Once, you have set up your virtual environment, activate it and install your desired python packages. You can find a sample yml to create a virtual environment here:

`/net/store/nbp/projects/sample_virtual_env/sample_env.yml`

### SETUP A REMOTE JUPYTER NOTEBOOK SERVER

You can setup a Jupyter server and work on it remotely.

```bash
ssh rzlogin@gate.ikw.uos.de
cd /net/store/nbp/projects/<project_folder>
conda activate my_env
jupyter notebook --no-browser --port=8889
```
Open another terminal and type the following command:

```bash
ssh -N -f -L localhost:8888:localhost:8889 rzlogin@gate.ikw.uos.de
```
The above command creates a local listener port at 8888 that connects with the remote jupyter server at 8889

Open a web browser and type

```html
https://localhost:8888
```
Voila! You can now access your data and write code in jupyter notebook
