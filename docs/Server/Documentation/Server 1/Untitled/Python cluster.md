# Python cluster

---

Python cluster is basically using computing power of server instead of your own, to run and compile programs.

### Setup
installed anaconda3 and set up desired kernel as needed
#### anaconda3 setup envs

Creates anaconda environement
```
conda create -n myenv python=3.9
```

activate environement
```
conda activate <env_name>
```

```
conda deactivate
```

install packages after activating env `(myenv)username@server$`
```
conda install <package>
```

Lists user envs
```
conda env list
```

Lists all envs - takes some tome there is a lot
```
conda list
```

after activating environement you can export it with
```
conda env export > environment.yml
```

creating from yaml file
```
conda env create -f environment.yml
```


### cluster setup
activate wanted environement
make directory where you want to the notebook to be,
enter
run notebook with specified IP and port
**port needs to be open**
```
jupyter notebook --no-browser --ip=127.0.0.1 --port=8890
```
open it in browser and use as regular notebook

### issues encountered
- you cant use external kernel to compile whole programs when using kernel in IDE as it comes to error in specifying PATH to the file. instead you can only send specific/selected lines and run them instaed one by one. tested it only on spyder, 
- jupyter notebook can run whole program as file is on cluster

---

## deploy on docker

### pre built images
container notebook with default python and no packages,
```
sudo docker run --rm -itd -p 9001:8888 -v /home/milos/jupyter_cluster:/home/jovyan --name jnotebook jupyter/minimal-notebook
```
see rest in build your image

### build your image
in https://jupyter-docker-stacks.readthedocs.io/en/latest/using/recipes.html#add-a-custom-conda-environment-and-jupyter-kernel
make Dockerfile and build image, run with new image.

better to add custom token in `command:` see issues
```
version: "3.9"

services:
  jupyter:
    image: #add image
    ports:
      - "9002:8888"
    volumes:
      - /home/milos/jupyter_cluster:/home/jovyan/ #add your path
#uncomment line below if you want to mount existing envs installed on host to your container,
#     - /home/milos/anaconda3/envs:/opt/conda/envs 
    environment:
      JUPYTER_ENABLE_LAB: "yes"
    command: "start-notebook.sh --NotebookApp.token='token' --NotebookApp.password='password'"
    tty: true
```

no env/kernel showing in notebook https://stackoverflow.com/questions/39604271/conda-environments-not-showing-up-in-jupyter-notebook
```
conda activate myenv
```
```
mamba install ipykernel
```
if already installed so just run from notebook terminal:
```
python -m ipykernel install --user --name myenv --display-name "<envnameyouwant>"
```
reboot container if needed, usualy just wait a bit. works as intended.

### issues encountered

- Generating token spam when running container if left empty, removing it generates random token possibly locking you out if you dont get link:
removed `--NotebookApp.token=''` from `command:` to prevent `Generating new user for token-authenticated request:` spam
better to add custom token https://stackoverflow.com/questions/75830256/jupyter-spam-with-generating-new-user-for-token-authenticated-request-in-logs

- Environements problem
in jupyter notebook documentation https://jupyter-docker-stacks.readthedocs.io/en/latest/using/common.html its stated that envs are saved in `/opt/conda` so we mount existing env with container as volume with
`-v /<your>/<path>/anaconda3/envs:/opt/conda/envs `
Note: dont try to copy whole env to the docker container, it will take more time and memory and might not work properly in the end, especially if you have to install ipykernel to the env. Rather build new image or mount to envs on host!

- Can not select/use environement/kernel from notebook. So open terminal in notebook and run following:
solution from: https://stackoverflow.com/questions/39604271/conda-environments-not-showing-up-in-jupyter-notebook
```
conda activate myenv
```
```
mamba install ipykernel
```
if already installed so just run from notebook terminal:
```
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```
reboot container if needed, usualy just wait a bit. works as intended.