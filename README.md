# ![alt text](https://raw.githubusercontent.com/OnToology/OnToology/master/media/icons/logoprop1_readme.png "OnToology")
[![Build Status](https://semaphoreci.com/api/v1/ahmad88me/ontoology/branches/master/badge.svg)](https://semaphoreci.com/ahmad88me/ontoology)
[![codecov](https://codecov.io/gh/OnToology/OnToology/branch/master/graph/badge.svg)](https://codecov.io/gh/OnToology/OnToology)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.1317786.svg)](https://doi.org/10.5281/zenodo.1317786)

A system for collaborative ontology development process. Given a repository with an owl file, **OnToology** will survey it and produce diagrams, a complete documentation and validation based on common pitfalls.

You can find a live version of OnToology online: http://ontoology.linkeddata.es.

Team: Ahmad Alobaid, Daniel Garijo, Maria Poveda, Idafen Santa, Oscar Corcho, Alba Fernandez Izquierdo

License: Apache License v2 (http://www.apache.org/licenses/LICENSE-2.0)


# To run automated tests
1. You should have [docker](https://docs.docker.com/) and [docker-compose](https://docs.docker.com/compose/) installed
2. You need to have a GitHub user to act as "OnToologyUser" (you can choose any username you like).
3. Add the details as in the *secret setup* section below.
4. Run the automated tests script `sh scripts/run_tests.sh` 



## Secret setup
This file should be added in `scripts/secret_setup.sh`
```
#!/bin/sh
export github_password=""
export client_id_login=""
export client_id_public=""
export client_id_private=""
export client_secret_login=""
export client_secret_public=""
export client_secret_private=""
export test_user_token=""
export test_user_email=""

```

<!--

## Tests (under refactoring)
ID | Test Case | Expected Result  | Status
:--|:---------:|:---------------: | :----:
1  | Adding non-existing repo | shouldn't add the non-existing repo and should add an error page | :heavy_check_mark:
2  | Very large ontology | To show error message | :warning: (takes literally days to perform the test, we are going to ignore this)
3  | Ontology with syntax error | To show error message | :heavy_minus_sign:
4  | If a tool is not able to generate an output | should not stop, should proceed with the other tools | :heavy_minus_sign:  
5  | Add a new repo | should be added | :heavy_minus_sign:
6  | Adding a repo that already added | should be accepted | :heavy_minus_sign:
7  | Add a new repo, then delete this repo from github and try to do some actions e.g. generate previsualization | should run the action without problems | :heavy_minus_sign:
8  | Generate previsualization | should be regenerated | :heavy_minus_sign: 


Sign | Meaning
:---:| :-----:
:heavy_minus_sign: | Test automation is not implemented
:heavy_check_mark: | Test automation is completed
:warning:          | Warning




## Auto deployment script

1. Before you run the script check the below variables that most probably you need to change to adapt to your

Things that you might want to change the username and email of git
```
git config --global user.name
git config --global user.email
```

And maybe you want to use the https url instead of git url
```
git clone https://github.com/OnToology/OnToology.git
```

and in the case of git keys, make sure to generate one and add it to OnToologyUser

2. Install git if not installed
```
sudo apt-get install git
```

3. Using the deployment script
```
sudo sh OnToology/deploy.sh
```

4. You may need to fix the permission for www-data (or another user).
This one is kinda trick and there are different ways to do it.
    * Ubuntu and www-data to have the same group number and user number (e.g. /etc/passwd and you can set it there)
    but this might not be the best, but the easiest.
    * Configure a separate user for the application and provide it with the permission of all necessary directories
    things like logs folder, temp folder, ssh key for GitHub.


5. Append environment variables (Below) to virtual environment venv/bin/activate (note: this won't work with apache)

#### Environment variables that you need to set

```
export github_username=OnToologyUser
export github_password=
export github_repos_dir=/home/ubuntu/temp/
export ar2dtool_dir=/home/ubuntu/ar2dtool/bin/
export ar2dtool_config=/home/ubuntu/config/
export widoco_dir=/home/ubuntu/widoco/
export owl2jsonld_dir=/home/ubuntu/owl2jsonld
export SECRET_KEY=
export tools_config_dir=/home/ubuntu/config
export previsual_dir=/home/ubuntu/vocabLite/jar
export wget_dir /home/ubuntu/wget_dir
export client_id_login=
export client_secret_login=
export client_id_public=
export client_secret_public=
export client_id_private=
export client_secret_private=
export publish_dir=/home/ubuntu/publish/

export db_username=
export db_password=
export db_host=
export db_port=

export email_server=""
export email_from=""
export email_username=""
export email_password=""
```

or in the local WSGI file `localwsgi.py`
```
import os
environ = os.environ
environ['github_username']="OnToologyUser"
environ['github_password']=""
environ['github_repos_dir']="/home/ubuntu/temp/"
environ['ar2dtool_dir']="/home/ubuntu/ar2dtool/bin/"
environ['ar2dtool_config']="/home/ubuntu/config/"
environ['widoco_dir']="/home/ubuntu/widoco/"
environ['owl2jsonld_dir']="/home/ubuntu/owl2jsonld"
environ['SECRET_KEY']=""
environ['tools_config_dir']="/home/ubuntu/config"
environ['previsual_dir']="/home/ubuntu/vocabLite/jar"
environ['wget_dir']="/home/ubuntu/temp/wget_dir"
environ['client_id_login']=""
environ['client_secret_login']=""
environ['client_id_public']=""
environ['client_secret_public']=""
environ['client_id_private']=""
environ['client_secret_private']=""
environ['publish_dir']="/home/ubuntu/publish/"

environ['db_username']=""
environ['db_password']=""
environ['db_host']=""
environ['db_port']=""

environ['email_server'] = ""
environ['email_from'] = ""
environ['email_username'] = ""
environ['email_password'] = ""
```

-->

## How to contribute
There are two workflows:

#### Case 1: If you are a contributor:
1. Create a new branch from the current live one (now it is `master`). Make sure to give it a presentive name. In case it is for a specific issue, include the issue number in the branch name, e.g. change-spinner-123.
2. Once you push your changes on the new branch, **create a pull request** and one of the admins will check your code base and will merge if it is ok.

#### Case 2: If you are not added as a contributor yet (or you are a contributor who prefers this workflow):
1. Fork from the current live branch (now it is `master`).
2. Create a pull request, we will review it and merge if it is ok.


