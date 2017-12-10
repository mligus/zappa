# Docker image for Zappa

Docker container to run Zappa based on the [Lambda Docker Image](https://hub.docker.com/r/lambci/lambda/)

Based on Daniel Whatmuff [danielwhatmuff/zappa](https://github.com/danielwhatmuff/zappa) container.


## Requirements

1. [Docker](https://www.docker.com) installed and running

2. AWS access credentials and/or custom AWS profile configured


## Features

* LambCI [Docker image](https://github.com/lambci/docker-lambda) that is as close as possible to AWS Lambda environment

* Ensure that you application (with requirements) can run on AWS Lambda

* Supports Python 2.7 and Python 3.6


## Usage


### With Shell alias (option 1)

Example alias with AWS profile used:

```
alias zappa-shell='docker run -ti -e AWS_PROFILE=${AWS_PROFILE:-default} -v ~/.aws:/root/.aws -v $(pwd):/var/task  --rm mligus/zappa bash'
```

or with key, secret and region passed directly from local environment: 

```
alias zappa-shell='docker run -ti -e AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID -e AWS_DEFAULT_REGION=$AWS_DEFAULT_REGION -v $(pwd):/var/task  --rm mligus/zappa bash
```

Enter Zappa _shell_:

```
zappa-shell
```


### With Makefile (option 2)

Example of `Makefile`:

```
.PHONY: zappa-shell
AWS_PROFILE ?= default

zappa-shell:
    docker run -ti -e AWS_PROFILE=$(AWS_PROFILE) -v $(CURDIR):/var/task -v ~/.aws/:/root/.aws  --rm mligus/zappa:python3.6 bash
```

To enter Zappa _shell_ run:

```
make zappa-shell
```


# Example workflow

1. Run Zappa _shell_ with `zappa-shell` or `make zappa-shell`

2. `zappa> ` shell prompt should appear

3. Source built-in virtual Python environment `source /var/venv/bin/activate` or create your own `python -m venv docker_venv`

4. Install requirements for your Lambda application `pip install -r requirements_deploy.txt`

5. Run Zappa commands:

```
zappa deploy <env>
zappa update <env>
zappa undeploy <env>
```

For more commands please refer to [Zappa](https://github.com/Miserlou/zappa)
