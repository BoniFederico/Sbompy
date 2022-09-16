# `Sbompy` - Create Sbom with Python

## Description

Sbompy is a Python tool that allow you to generate a json Software Bill of Materials (SBOM) in accord to the [CycloneDX v1.4 SBOM standard](https://cyclonedx.org/docs/1.4/json/).
You can generate the SBOM both from a local folder or from a GitHub repository. Dependencies are collected from <i>requirements.txt</i> file inside the folder, but the tool is also capable of collecting other dependencies by parsing each file `.py` in the folder. Sbompy can also collect indirect dependencies (dependencies of dependencies) by installing all the dependencies in a <i>Python virtual environment</i> inside the target folder.

## Installation

You can install [Sbompy from pip](https://test.pypi.org/project/sbompy/); currently Sbompy is available only in <i>test.pypi</i> index, so you have to run the following command:

```posh
pip install --index-url 'https://test.pypi.org/simple/' --extra-index-url 'https://pypi.org/simple' sbompy
```

## Requirements

If you install Sbompy from pip (as per the section above) all the requirements will be automatically installed in your system. Otherwise, if you want to download the repository from GitHub, in order to use Sbompy you will need to install all the dependencies defined int <i>requirements.txt</i>. You can either installing them manually using a packet manager (e.g. pip) or you can install them with the following pip command on the <i>requirements.txt</i> file of the project:

```posh
pip install -r 'requirements.txt'
```

## Usage

```posh
usage: sbompy.py [-h] [-s [S]] [-p] [-k K] [-d] [-m] [-l [L]] [-v [V]]

Sbompy is a tool for creating sbom in json format from a Python project.

options:
  -h, --help            -Show this help message and quit.
  -s [S], -source [S]   -Project location. Can be both a local path or a Github url.In
                        case of Github url, repository will be downloaded inside the
                        current folder and you must provide the -k argument.If no path
                        is specified, then path will be current path \.
  -p, -parse            -If present, dependencies will be also searched inside the code
                        by parsing each python file and searching 'import' statements.
  -k K, -key K          -If the source is a GitHub directory, you must provide a
                        GitHub API key. GitHub API key starts with 'ghp_'.
  -d, -deep             -If present, direct dependencies will be installed inside a virt.
                        environment inside the project folder and indirect dependencies
                        will be captured.
  -m, -migrate          -If present, sbompy will migrate your Python 2 code to Python 3.
                        This could be usefull since -deep feature will raise errors with
                        Python 2 syntax.
  -l [L], -location [L]
                        -Where the sbom file will be stored. When no path is specified,
                        then path will be current path \.
  -v [V], -verbose [V]  -Logging level. Can be 0 (NotSet), 1 (Debug), 2 (Info), 3
                        (Warning), 4 (Error), 5 (Critical).
```

## Examples

The following command build a sbom from the ‘spid-sp-test’ GitHub repository provided the GitHub key and store the sbom in the ‘example’ folder. Dependencies are collected only from the requirements.txt file if present. There will not be indirect dependencies (unless they are specified in the requirements.txt).

```posh
python sbompy.sbompy -s 'https://github.com/italia/spid-sp-test' -k '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' -l 'example'
```

The following command build a sbom from the ‘spid-sp-test’ GitHub repository provided the GitHub key and store the sbom in the current folder. Dependencies are collected both from requirements.txt and from parsing the code (-p flag). Indirect dependencies are collected by installing in a virtual environment the direct dependencies (-d flag).

```posh
python sbompy.sbompy -s 'https://github.com/italia/spid-sp-test' -k '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' -d -p
```

The following command build a sbom from the local folder ‘project’ and store the sbom in the current folder.Dependencies are collected only from the requirements.txt file if present. There will not be indirect dependencies (unless they are specified in the requirements.txt).

```posh
python sbompy.sbompy -s 'C:\Users\12345\Desktop\project
```
