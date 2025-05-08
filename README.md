# fun-with-jenkins

[![Build status](https://badge.buildkite.com/b11986402806b48d2cce49893def5d0e75ed8cb1ca5f147a47.svg)](https://buildkite.com/cnunciato/fun-with-jenkins)

This is just me getting familiar with Jenkins.

* The `infra` folder contains a Pulumi program that deploys Jenkins as a Fargate service. It's just the one container for now, so nothing fancy. The initial `admin` password is set with Pulumi as a secret. To get that, run:

    ```bash
    pulumi -C infra config get jenkinsAdminPassword
    ```

* The `.buildkite` folder contains a Node.js program that parses the `Jenkinsfile` in the root of this repo and converts it into a Buildkite pipeline definition. Commits to the `main` branch run this program and extend the Buildkite pipeline at runtime accordingly:

    ![Image](https://github.com/user-attachments/assets/57114e6f-862b-4992-a12e-9c03faa82342)

## Running Jenkins locally

To spin up a quick Jenkins install locally, first make sure Docker Desktop is running, then:

```bash
docker-compose up
```

... and browse to http://localhost:8080.

