# certboto-docker 📜🤖☁️🐳 #

[![GitHub Build Status](https://github.com/cisagov/certboto-docker/workflows/build/badge.svg)](https://github.com/cisagov/certboto-docker/actions/workflows/build.yml)
[![CodeQL](https://github.com/cisagov/certboto-docker/workflows/CodeQL/badge.svg)](https://github.com/cisagov/certboto-docker/actions/workflows/codeql-analysis.yml)
[![Known Vulnerabilities](https://snyk.io/test/github/cisagov/certboto-docker/badge.svg)](https://snyk.io/test/github/cisagov/certboto-docker)

## Docker Image ##

[![Docker Pulls](https://img.shields.io/docker/pulls/cisagov/certboto)](https://hub.docker.com/r/cisagov/certboto)
[![Docker Image Size (latest by date)](https://img.shields.io/docker/image-size/cisagov/certboto)](https://hub.docker.com/r/cisagov/certboto)
[![Platforms](https://img.shields.io/badge/platforms-amd64%20%7C%20arm%2Fv6%20%7C%20arm%2Fv7%20%7C%20arm64%20%7C%20ppc64le%20%7C%20s390x-blue)](https://hub.docker.com/r/cisagov/certboto/tags)

Certboto combines all the convenience of [Certbot](https://certbot.eff.org)
with the cloudiness of [AWS S3 buckets](https://aws.amazon.com/s3/)
and [AWS Route53](https://aws.amazon.com/route53/)
all wrapped up in a tasty [Docker](https://www.docker.com) container.

## Running ##

<<<<<<< HEAD
Consider using a `docker-compose.yml` file to run Certboto.
=======
### Running with Docker ###

To run the `cisagov/example` image via Docker:

```console
docker run cisagov/example:0.2.0
```
>>>>>>> 0d48ebd47a28a887868ea3093e675e95f3843561

### Running with Docker Compose ###

1. Create a `docker-compose.yml` file similar to the one below to use [Docker Compose](https://docs.docker.com/compose/).

    ```yaml
    ---
    version: "3.7"

    secrets:
      credentials:
        file: /home/username/.aws/credentials

    services:
<<<<<<< HEAD
      certboto:
        image: cisagov/certboto
        init: true
        restart: "no"
=======
      example:
        image: cisagov/example:0.2.0
        volumes:
          - type: bind
            source: <your_log_dir>
            target: /var/log
>>>>>>> 0d48ebd47a28a887868ea3093e675e95f3843561
        environment:
          - AWS_DEFAULT_REGION=us-east-1
          - BUCKET_NAME=my-certificates
          - BUCKET_PROFILE=certsync-role
          - DNS_PROFILE=dns-role
        secrets:
          - source: credentials
            target: credentials
    ```

#### Issue a new certificate ####

```console
docker compose run certboto certonly -d lemmy.imotorhead.com
```

#### Renew an existing certificate ####

```console
docker compose run certboto
```

#### Additional `certbot` commands ####

The `certbot` help can be displayed without synchronizing with a bucket.

```console
docker compose run certboto --help
```

More complicated `certbot` commands may be impossible to escape correctly. The
`--shell` flag can be used to drop into a shell within the container after the
bucket is synchronized to the container.  This allows users to issue commands
directly to `certbot`.  Once the shell exits cleanly, the container will be
synchronized back to the bucket.

```console
docker compose run certboto --shell
```

#### Disabling Route53 challenges ####

To disable usage of the Route53 DNS plugin pass `--no-dns-route53` as the first
argument.  This is useful if you need to use other types of challenges.

```console
docker compose run certboto --no-dns-route53 --manual certonly -d lemmy.imotorhead.com
```

## Using secrets with your container ##

This container also supports passing sensitive values via [Docker
secrets](https://docs.docker.com/engine/swarm/secrets/).  Passing sensitive
values like your credentials can be more secure using secrets than using
environment variables.  See the
[secrets](#secrets) section below for a table of all supported secret files.

1. To use secrets, create a `certboto_credentials` file containing the values you
want set:

    ```ini
    [default]
    aws_access_key_id = XXXXXXXXXXXXXXXXXXXX
    aws_secret_access_key = xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

    [dns-role]
    role_arn = arn:aws:iam::1234567890ab:role/ModifyPublicDNS
    source_profile = default

    [bucket-role]
    role_arn = arn:aws:iam::1234567890ab:role/CertbotBucket
    source_profile = default

    # If running on EC2 with an instance profile that allows sts:AssumeRole
    # you can assume delegated roles using the metadata as the credential source
    # See: https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-role.html

    [dns-role-ec2]
    role_arn = arn:aws:iam::1234567890ab:role/ModifyPublicDNS
    credential_source = Ec2InstanceMetadata

    [bucket-role-ec2]
    role_arn = arn:aws:iam::1234567890ab:role/CertbotBucket
    credential_source = Ec2InstanceMetadata
    ```

1. Then add the secret to your `docker-compose.yml` file:

    ```yaml
    ---
    version: "3.7"

    secrets:
      credentials:
        file: certboto_credentials

    services:
<<<<<<< HEAD
      certboto:
        image: cisagov/certboto
        init: true
        restart: "no"
=======
      example:
        image: cisagov/example:0.2.0
        volumes:
          - type: bind
            source: <your_log_dir>
            target: /var/log
>>>>>>> 0d48ebd47a28a887868ea3093e675e95f3843561
        environment:
          - AWS_DEFAULT_REGION=us-east-1
          - BUCKET_NAME=my-certificates
          - BUCKET_PROFILE=certsync-role
          - DNS_PROFILE=dns-role
        secrets:
          - source: credentials
            target: credentials
    ```

## Updating your container ##

### Docker Compose ###

1. Pull the new image from Docker Hub:

    ```console
    docker compose pull
    ```

1. Recreate the running container by following the
[previous instructions](#running-with-docker-compose):

    ```console
    docker compose run certboto
    ```

<<<<<<< HEAD
## Image tags ##

The images of this container are tagged with
[semantic versions](https://semver.org).  It is recommended that most users use
a version tag (e.g. `:0.1.4`).

| Image:tag | Description |
|-----------|-------------|
|`cisagov/certboto:0.1.4`| An exact release version. |
|`cisagov/certboto:0.1`| The most recent release matching the major and minor version numbers. |
|`cisagov/certboto:0`| The most recent release matching the major version number. |
|`cisagov/certboto:edge` | The most recent image built from a merge into the `develop` branch of this repository. |
|`cisagov/certboto:nightly` | A nightly build of the `develop` branch of this repository. |
|`cisagov/certboto:latest`| The most recent release image pushed to a container registry.  Pulling an image using the `:latest` tag [should be avoided.](https://vsupalov.com/docker-latest-tag/) |
=======
### Docker ###

1. Stop the running container:

    ```console
    docker stop <container_id>
    ```

1. Pull the new image:

    ```console
    docker pull cisagov/example:0.2.0
    ```

1. Recreate and run the container by following the [previous instructions](#running-with-docker).

## Updating Python dependencies ##

This image uses [Pipenv] to manage Python dependencies using a [Pipfile](https://github.com/pypa/pipfile).
Both updating dependencies and changing the [Pipenv] configuration in `src/Pipfile`
will result in a modified `src/Pipfile.lock` file that should be committed to the
repository.

> [!WARNING]
> The `src/Pipfile.lock` as generated will fail `pre-commit` checks due to JSON formatting.

### Updating dependencies ###

If you want to update existing dependencies you would run the following command
in the `src/` subdirectory:

```console
pipenv lock
```

### Modifying dependencies ###

If you want to add or remove dependencies you would update the `src/Pipfile` file
and then update dependencies as you would above.

> [!NOTE]
> You should only specify packages that are explicitly needed for your Docker
> configuration. Allow [Pipenv] to manage the dependencies of the specified
> packages.

## Image tags ##

The images of this container are tagged with [semantic
versions](https://semver.org) of the underlying example project that they
containerize.  It is recommended that most users use a version tag (e.g.
`:0.2.0`).

| Image:tag | Description |
|-----------|-------------|
|`cisagov/example:0.2.0`| An exact release version. |
|`cisagov/example:0.2`| The most recent release matching the major and minor version numbers. |
|`cisagov/example:0`| The most recent release matching the major version number. |
|`cisagov/example:edge` | The most recent image built from a merge into the `develop` branch of this repository. |
|`cisagov/example:nightly` | A nightly build of the `develop` branch of this repository. |
|`cisagov/example:latest`| The most recent release image pushed to a container registry.  Pulling an image using the `:latest` tag [should be avoided.](https://vsupalov.com/docker-latest-tag/) |
>>>>>>> 0d48ebd47a28a887868ea3093e675e95f3843561

See the [tags tab](https://hub.docker.com/r/cisagov/certboto/tags) on Docker
Hub for a list of all the supported tags.

## Volumes ##

There are no volumes.

<!--
| Mount point | Purpose        |
|-------------|----------------|
| `/path/to/volume` | Describe its purpose. |
-->

## Ports ##

There are no exposed ports.

<!--
| Port | Purpose        |
|------|----------------|
| PORT_NUMBER | Describe its purpose. |
-->

## Environment variables ##

### Required ###

| Name | Purpose |
|------|---------|
| AWS_DEFAULT_REGION | Default AWS region. |
| BUCKET_NAME | The bucket to store the Certbot configuration. |
| BUCKET_PROFILE | The profile of your `credentials` to use for bucket access. |
| DNS_PROFILE | The profile of your `credentials` to use for route53 access. |

### Optional ###

There are no optional environment variables.

<!--
| Name  | Purpose | Default |
|-------|---------|---------|
| `OPTIONAL_VARIABLE` | Describe its purpose.  | `null` |
-->

## Secrets ##

| Filename | Purpose |
|----------|---------|
| `credentials` | The [AWS credentials](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html) file. |

## Building from source ##

Build the image locally using this git repository as the [build context](https://docs.docker.com/engine/reference/commandline/build/#git-repositories):

```console
docker build \
<<<<<<< HEAD
  --build-arg VERSION=0.1.4 \
  --tag cisagov/certboto:0.1.4 \
  https://github.com/cisagov/certboto-docker.git#develop
=======
  --tag cisagov/example:0.2.0 \
  https://github.com/cisagov/example.git#develop
>>>>>>> 0d48ebd47a28a887868ea3093e675e95f3843561
```

## Cross-platform builds ##

To create images that are compatible with other platforms, you can use the
[`buildx`](https://docs.docker.com/buildx/working-with-buildx/) feature of
Docker:

1. Copy the project to your machine using the `Code` button above
   or the command line:

    ```console
    git clone https://github.com/cisagov/certboto-docker.git
    cd certboto-docker
    ```

1. Create the `Dockerfile-x` file with `buildx` platform support:

    ```console
    ./buildx-dockerfile.sh
    ```

1. Build the image using `buildx`:

    ```console
    docker buildx build \
      --file Dockerfile-x \
      --platform linux/amd64 \
<<<<<<< HEAD
      --build-arg VERSION=0.1.4 \
      --output type=docker \
      --tag cisagov/certboto:0.1.4 .
=======
      --output type=docker \
      --tag cisagov/example:0.2.0 .
>>>>>>> 0d48ebd47a28a887868ea3093e675e95f3843561
    ```

## AWS policies ##

### Certboto roles ###

The `BUCKET_PROFILE` should assume a role with the following policy:

```javascript
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:ListBucket",
                "s3:DeleteObject"
            ],
            "Resource": [
                "arn:aws:s3:::cert-bucket-name",
                "arn:aws:s3:::cert-bucket-name/*"
            ]
        }
    ]
}
```

The `DNS_PROFILE` should assume a role with the following policy:

```javascript
{
    "Version": "2012-10-17",
    "Id": "certbot-dns-route53 sample policy",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "route53:ListHostedZones",
                "route53:GetChange"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect" : "Allow",
            "Action" : [
                "route53:ChangeResourceRecordSets"
            ],
            "Resource" : [
                "arn:aws:route53:::hostedzone/YOURHOSTEDZONEID"
            ]
        }
    ]
}
```

### Certificate access role ###

To access a specific certificate, a role with the following profile should be
assumed:

```javascript
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "allow-cert-read",
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::cert-bucket-name/live/lemmy.imotorhead.com/*"
        }
    ]
}
```

### Accessing and installing certificates at instance boot time ###

The certificates created by Certboto can be installed on a booting instance
using [cloud-init](https://cloudinit.readthedocs.io/en/latest/).  An implementation
of this can be found in the
[openvpn-server-tf-module](https://github.com/cisagov/openvpn-server-tf-module)
project.  Specifically
[`install-certificates.py`](https://github.com/cisagov/openvpn-server-tf-module/blob/develop/cloudinit/install-certificates.py)

## Contributing ##

We welcome contributions!  Please see [`CONTRIBUTING.md`](CONTRIBUTING.md) for
details.

## License ##

This project is in the worldwide [public domain](LICENSE).

This project is in the public domain within the United States, and
copyright and related rights in the work worldwide are waived through
the [CC0 1.0 Universal public domain
dedication](https://creativecommons.org/publicdomain/zero/1.0/).

All contributions to this project will be released under the CC0
dedication. By submitting a pull request, you are agreeing to comply
with this waiver of copyright interest.

[Pipenv]: https://pypi.org/project/pipenv/
