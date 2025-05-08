# fun-with-jenkins

[![Build status](https://badge.buildkite.com/41540f18af5fa6a63abe00a854bfe22f7a1a0131210f7c08a4.svg)](https://buildkite.com/cnunciato/fun-with-jenkins)

This is just me getting familiar with Jenkins.

## Infrastructure

The `infra` folder contains a Pulumi program that deploys Jenkins as a Fargate service. It's just the one container for now, so nothing fancy. The initial `admin` password is set with Pulumi as a secret. To get that, run:

```bash
pulumi -C infra config get jenkinsAdminPassword
```

## Converting a Jenkinsfile to a Buildkite pipeline

The `.buildkite` folder contains a Node.js script that reads the `Jenkinsfile` in the root of this repo, passes it to the Jenkins server (specifically to the `pipeline-model-converter` endpoint), and transforms the JSON returned by Jenkins into a Buildkite pipeline definition. For example, given the following `Jenkinsfile`:

```groovy
pipeline {
    agent any
    stages {
        stage(':jenkins: Hello from the Jenkinsfile!') {
            steps {
                echo 'Hi, world! :wave:'
            }
        }
    }
}
```

You'd get:

```
$ npm -C .buildkite --silent run build 
{
    "steps": [
        {
            "label": ":jenkins: Hello from the Jenkinsfile!",
            "commands": [
                "echo 'Hi, world! :wave:'"
            ]
        }
    ]
}
```

Commits to the `main` branch run this program and extend the Buildkite pipeline at runtime accordingly:

![A Buildkite pipeline generated from a Jenkinsfile](https://github.com/user-attachments/assets/758e44c0-e506-44d7-9afb-224efcfa5745)\

:kite:

## Running the Jenkins server locally

To spin up a quick Jenkins install locally with Docker Compose, first make sure Docker Desktop is running, then run:

```bash
docker-compose up
```

... and browse to the server at http://localhost:8080.

More to come.