# NWB Explorer

NWB Explorer is a web application that can be used by scientists to read, visualize and explore
the content of NWB files. 

Learn more about the [Neurodata Without Borders](https://www.nwb.org/).



## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites 
Below you will find the software you need to install to use nwb explorer (and the versions we used):
* Git (2.17.0).
* Node (9.11.1) and npm (6.0.0).
* Python 3 (3.6+), pip (10.0.1)



#### Python Dependencies
=======
* Django (1.11.7). `pip install django`
* Pygeppeto_server. ```git clone https://github.com/MetaCell/pygeppetto-django.git && cd pygeppetto-django && git checkout development && pip install -e . ```
* Pygeppeto_model.```git clone https://github.com/openworm/pygeppetto.git && cd pygeppetto && git checkout manager && pip install -e . ```
* Pyecore (0.8.1). `pip install pyecore`
* Pynwb. ```git clone https://github.com/NeurodataWithoutBorders/pynwb.git && cd pynwb && git checkout dev && pip install -e . ```
* Seaborn (0.8.1). `pip install seaborn`
 

We recommend the use of a new python 3 virtual environment: 

```
python3 -m venv new_venv_folder
source new_venv_folder/bin/activate
```

Or, with conda

```bash
conda create -n nwb python=3.7
source activate nwb
```
### Local installation

Step by step instructions to get a development environment running.


First, clone nwb explorer
```bash
git clone -b development https://github.com/MetaCell/nwb-explorer [PROJECT_ROOT]
```
Then run install script
```bash
cd PROJECT_ROOT
cd utilities
python install.py [branch MYBRANCH]
```

## How to run

After the installation is complete, run the script:
```bash
cd [PROJECT_ROOT]
./NWBE
```

If everything worked, the default browser will open on `http://localhost:8888/geppetto`

### Run with docker
Under the folder k8s we can find the container definitions to setup a kubernetes deployment with jupyter hub spawner.
We can run with docker with the following commands:
```bash
cd [PROJECT_ROOT]/k8s
docker build -t nwb-explorer --build-arg BRANCH=nwbdev .
docker run -it -p8888:8888 nwb-explorer
```

## How to use

When the application is started, no file will be loaded.

1. Use the interface to load the file from a public url or just load a sample
1. Specify the parameter nwbfile in your browser. Example: `http://localhost:8000/geppetto?nwbfile=https://github.com/OpenSourceBrain/NWBShowcase/raw/master/NWB/time_series_data.nwb`

After the file is loaded, a Jupyter notebook will be available.
From the notebook the current loaded file can be accessed through the variable `nwbfile`.
For further information about the Python API, see the [PyNWB docs](https://pynwb.readthedocs.io/en/stable/)


## How to develop
The application is built as a Jupyter notebook extension by means of the [jupyter-geppetto extension](https://github.com/openworm/org.geppetto.frontend.jupyter).
The Jupyter notebook web application is hence used as a backend, the application pages, the web resources and apis are served by Tornado handlers.

### Python code
In order to have all the python files redeployed, the application and the dependencies must be installed in development mode, i.e. with the command
```
pip install -e .
```
### Javascript code
To check if a dependency is installed in development mode, run pip list.

JS/HTML code can be found inside `static/org.geppetto.frontend/src/main/webapp/`. The code needs to be rebuilt with webpack everytime there is a change. The recommended way is to run in `/static/org.geppetto.frontend/src/main/webapp/` this command:
```
npm run build-dev-noTest:watch
```

## Built With

* [PyNWB](https://github.com/NeurodataWithoutBorders/pynwb) - Used to read and manipulate NWB files
* [Jupyter notebook](https://jupyter.org/) - The Jupyter notebook web application is used as a backend.
* [Geppetto](http://www.geppetto.org/) - Used to build a web-based application to visualize and simulate the NWB 2.0 files.

## Background
The NWB Explorer was initially created by MetaCell to showcase the features of the Geppetto platform to share 
neurophysiological data in Neurodata Without Borders format. It was further developed as part of a 
Google Summer of Code project with the OpenWorm project. It is currently being extended as part of the Open Source Brain
project to provide both a standalone and online application for visualising and analysing the contents of NWB files. 
This work is currently funded by the Wellcome Trust.

## Authors

* Matteo Cantarelli ([MetaCell](http://metacell.us))
* Giovanni Idili ([MetaCell](http://metacell.us))
* Afonso Pinto 

See also the list of [contributors](https://github.com/Metacell/nwb-explorer/contributors) who participated in this project.



