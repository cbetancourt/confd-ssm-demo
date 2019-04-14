# AWS SSM, confd demo

A demo project that uses confd to generate config files for applications. It uses the AWS SSM Parameter Store as backend.

## Requirements

 - docker
 - docker-compose

### Parameters in SSM

You can generate the example parameters in SSM with the following commands, just make sure you have set the `AWS_PROFILE` environment variable before you run them.

```
aws ssm put-parameter --name /dev/client-api/database/user --value client --type String
aws ssm put-parameter --name /dev/client-api/database/password --value p@ssw0rd --type SecureString
```

## The containers

Check the `docker-compose.yaml`, it mounts up the `config-output` directory, where the templates will be generated, it also mounts up your `~/.aws` folder so it can use the credentials. The container is passing in the `AWS_PROFILE` variable which is then going to be used by `confd` to authenticate.

The default AWS region the examples are using is `us-east-1`, US East (N. Virgina).

## Start the project

Just run
```
docker-comopse up --build
```

The template files will be generated in the `config-output` folder.
