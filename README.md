# Sbompy

## Description

Sbompy is a Python tool that allow you to generate a json Software Bill of Materials (SBOM) in accord to the CycloneDX v1.4 SBOM standard.
You can generate the SBOM both from a local folder or from a GitHub repository. Dependencies are collected from requirements.txt file inside the folder, but the tool is also capable of collecting other dependencies by parsing each file .py in the folder. Sbompy can also collect indirect dependencies (dependencies of dependencies) by installing all the dependencies in a Python venv inside the target folder.

## Requirements

In order to use Sbompy you will need to make sure that all the dependencies defined in the requirements.txt are installed in your system. You can both installing them manually using a packet manager (e.g. pip) or you can install all of them with the following pip command on the requirements.txt file of the project:

''
pip install -r requirements.txt

## Installation

You can either download Sbompy from the repository or install it with pip:

pip install sbompy

## Usage

usage: sbompy.py [-h] [-s [S]] [-p] [-k K] [-d] [-l [L]]

Sbompy is a tool for creating sbom in json format from a Python project.

options:
-h, --help show this help message and exit
-s [S], -source [S] Project location. Can be both a local path or a Github
url. In case of Github url, repository will be
downloaded inside the current folder and you must
provide the -k argument. If no path is specified, then
path will be current path \.
-p, -parse If present, dependencies will be also searched inside
the code by parsing each python file searching for
'import' statements.
-k K, -key K In case the source is a GitHub directory, you must
provide a GitHub API key. GitHub API key starts with
'ghp\_'.
-d, -deep If present, direct dependencies will be installed in a
virtual environment inside the project folder and
indirect dependencies will be also captured.
-l [L], -location [L]
Location where to store the sbom file. If no path is
specified, then path will be current path \.

## Examples

The following command build a sbom from the ‘spid-sp-test’ GitHub repository provided the GitHub key and store the sbom in the ‘example’ folder. Dependencies are collected only from the requirements.txt file if present. There will not be indirect dependencies (unless they are specified in the requirements.txt).

python sbompy.py -s 'https://github.com/italia/spid-sp-test' -k 'ghp_Tdsafdsafdsvgbfdgfdbredfasdf' -l 'example'

The following command build a sbom from the ‘spid-sp-test’ GitHub repository provided the GitHub key and store the sbom in the current folder. Dependencies are collected both from requirements.txt and from parsing the code (-p flag). Indirect dependencies are collected by installing in a virtual environment the direct dependencies (-d flag).

python sbompy.py -s 'https://github.com/italia/spid-sp-test' -k 'ghp_ThzjnQNGxY3dsfathtrh4543qrf4tegrsadUsKf' -d -p

The following command build a sbom from the local folder ‘project’ and store the sbom in the current folder.Dependencies are collected only from the requirements.txt file if present. There will not be indirect dependencies (unless they are specified in the requirements.txt).

python sbompy.py -s 'C:\Users\12345\Desktop\project
