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

## Containers

### Server
First, we will build the confd server image that our client will use, and tag it as `confd-alpine`. This is only necessary when your base Alpine image or version of confd need to be upgraded.
```
docker build ./server/ -t confd-alpine
```

The server is configured with an entrypoint script, but it will not run automatically since its template configuration is empty.

### Client
The client image will build on the server image, add your template configuration, map an output directory, and execute the entrypoint script. The image will stop once your configuration files are and saved to the output directory.

## Put it All Together
The `docker-compose.yaml` mounts the `output` directory where the templates will be generated. It also mounts up your `~/.aws` directory so it can use your AWS credentials.

The container is passing in the `AWS_PROFILE` variable which is then going to be used by `confd` to authenticate.

The default AWS region the examples are using is `us-east-1`, US East (N. Virgina).

### Generate your configuration files

Just run:
```
docker-compose up --build
```

The template files will be generated in the `output` directory.
