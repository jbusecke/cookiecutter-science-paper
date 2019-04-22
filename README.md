# Cookiecutter Science Paper

_A cookiecutter template for reproducible science papers._

This template is an addition to [cookiecutter-science-project](https://github.com/jbusecke/cookiecutter-science-project). It lets you easily publish a code repository with your paper, when it is accepted (or in the revision stage).

Following the [cookiecutter-science-project](https://github.com/jbusecke/cookiecutter-science-project) workflow, upload the data needed to reproduce to a citeable [zenodo](https://zenodo.org/) archive.
Note the id of your dataset (the number at the end of the url like this https://zenodo.org/record/xxxxxx), for the setup process later.


### Requirements to use the cookiecutter template:
-----------
 - Python 2.7 or 3.5
 - [Cookiecutter Python package](http://cookiecutter.readthedocs.org/en/latest/installation.html) >= 1.4.0: This can be installed with pip by or conda depending on how you manage your Python packages:

``` bash
$ pip install cookiecutter
```

or

``` bash
$ conda - c conda-forge install cookiecutter
```


### To start a new paper, run:
------------
``` bash
$ cookiecutter https://github.com/jbusecke/cookiecutter-science-paper
```

If you have previously created a package with this template confirm the prompt to redownload the newest version.
The installation dialog will ask for a few inputs:
- `author_list`: List of authors or typical citation format like `author_etal`
- `journal`: Journal in which the article will be published, like `nature`.
- `year`: Year of publication.
- `author_name`: Your name.
- `short_title`: Optional. If you want your repository to have some short description in the title (e.g. `author_etal_nature_2018_stratosphere`) enter `stratosphere` here. Otherwise just press enter.
- `repo_name`: This will be the name of the resulting github repository. Normally just press enter to confirm.
- `github_username`: Your username for [github](https://github.com).
- `open_source_license`: Chose a license for your package. Currently available licenses are: "MIT" and "BSD-3-Clause", details can be found [here]().
- `zenodo_data_id`: The Zenodo id for your uploaded datasets (see above)
- `python_interpreter`: Chose your python version. In most cases just press enter to chose python 3.

### The resulting directory structure
------------

This will set up a project folder with the following structure in the current directory:

```
├── setup.py
├── README.md             <- Readme for this paper
├── LICENSE
├── environment.yml       <- Conda environment file. Create environment with
│                           `conda env create -f environment.yml`
├── .travis.yml           <- Conda environment file. Create environment with
│                           `conda env create -f environment.yml`
├── .stickler.yml         <- Conda environment file. Create environment with
│                           `conda env create -f environment.yml`
├── scripts              
│   ├── setup.sh          <- Shell script to initialize new project.
│   └── download_zenodo_files <- Shell script to automatically download zenodo files.
│
├── notebooks             <- Jupyter notebooks that reproduce all figures, tables etc in your study
│                              from the data in the zenodo archive.
│
├── data                  <- data directory containing downloaded zenodo file
│
├── ci                    <- Files for continous integration; see travis-ci.com
│
└──  repo_name         <- Source code for use in this project.
    ├── __init__.py       <- Makes `repo_name` a Python module
    │
    ├── dummy.py          <- Example python module file. These contain your installable functions
    |
    └── tests
        └── test_dummy.py
```




The directory includes a simple setup script, which will create a github repository and commit the current state as initial commit.

In the directory created by cookiecutter do

```bash
$ ./scripts/setup.sh
```

Then download the data from zenodo with

```bash
$ ./scripts/download_zenodo_files.sh
```
> It is important to execute these scripts from the root directory

Now you can move notebooks from your [science project](https://github.com/jbusecke/cookiecutter-science-project)
over to this folder and make sure they work correctly with the archived data. Migrate any functions/test needed for the notebooks over to the paper module. All steps should work on a completely independent system.

Once everything works, [add your github repository to zenodo](https://guides.github.com/activities/citable-code/).
Then commit and tag your git repository and push to github, zenodo will automatically create a citeable DOI, that you can put into the paper.


### Optional features

#### CI with travis-ci
Head over to [travis](https://travis-ci.org/), ...
For each service log in with your github account and follow the instructions for activating your github repo. It can take a while until new repos show up in travis. Just get a cup of coffee or have a nice chat with your office mate.

<!-- #### Binder deployment
Not implemented yet -->
