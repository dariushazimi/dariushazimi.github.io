# Create a distribution file for python script
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Create a distribution file for python script](#create-a-distribution-file-for-python-script)
    - [Install setuptools](#install-setuptools)

<!-- /code_chunk_output -->

This shows you how to create a distribution file so that users can install the script on their machines.

We will do that using the setup tools
## Install setuptools
` pipenv install -d setuptools`


**Note**

We use -d since we only need the setuptool for development

Create a [setup.py](https://setuptools.readthedocs.io/en/latest/setuptools.html#basic-use) file, it contains many tools. Here I list some of the common ones.
```
from setuptools import setup,
setup(
    name="HelloWorld", # Name of your package
    version="0.1",
    author="Dariush Azimi", # your name in this case
    author_email="your email addr",
    licese="GPLv3+",
    packages=['packagename'],
    url="to your project repo at github", # an example
    install_requires =[ #tell setup tools what packages are required
        'click', # or what ever the packages your script needs
        'boto3'
    ],
    entry_points='''
    [console_scripts] # here we say we have a console script
    awsarmy=awsarmy.awsarmy:cli # here it is called awsarmy, will look inside the directory called awsarmy,and next will look for the module called .awsrmy and then will look for a function called
    cli
    ''',
)
```

- Next do the following
``` pipenv run python setup.py bdist_wheel```
this will create an output file in the dist folder that you can use to install with pip3 command

- to install it 
    `pip3 install https://github.com/dariushazimi/aws-snapshot-analyzer/blob/master/awsbutler/awsbutler_2018-2018_11_01_0.1-py3-none-any.whl`

You can use the url to point to the location of the wheel file to install it.
