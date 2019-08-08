# certboto-docker 📜🤖☁️🐳 #

[![Build Status](https://travis-ci.com/cisagov/certboto-docker.svg?branch=develop)](https://travis-ci.com/cisagov/certboto-docker)
[![Total alerts](https://img.shields.io/lgtm/alerts/g/cisagov/certboto-docker.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/cisagov/certboto-docker/alerts/)
[![Language grade: Python](https://img.shields.io/lgtm/grade/python/g/cisagov/certboto-docker.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/cisagov/certboto-docker/context:python)

## Docker Image ##

![MicroBadger Layers](https://img.shields.io/microbadger/layers/dhsncats/certboto.svg)
![MicroBadger Size](https://img.shields.io/microbadger/image-size/dhsncats/certboto.svg)

This is a docker skeleton project that can be used to quickly get a
new [cisagov](https://github.com/cisagov) GitHub docker project
started.  This skeleton project contains [licensing
information](LICENSE), as well as [pre-commit
hooks](https://pre-commit.com) and a [Travis
CI](https://travis-ci.com) configuration appropriate for docker
containers and the major languages that we use.

## Usage ##

### Install ###

Pull `dhsncats/certboto` from the Docker repository:

    docker pull dhsncats/certboto

Or build `dhsncats/certboto` from source:

    git clone https://github.com/cisagov/certboto-docker.git
    cd certboto-docker
    docker-compose build --build-arg VERSION=0.0.1

### Run ###

    docker-compose run --rm example

## Ports ##

This container exposes the following ports:

| Port  | Protocol | Service  |
|-------|----------|----------|
| 8080  | TCP      | http     |

## Environment Variables ##

| Variable      | Default Value                 | Purpose      |
|---------------|-------------------------------|--------------|
| ECHO_MESSAGE  | `Hello World from Dockerfile` | Text to echo |

## Secrets ##

| Filename      | Purpose              |
|---------------|----------------------|
| quote.txt     | Secret text to echo  |

## Volumes ##

| Mount point | Purpose        |
|-------------|----------------|
| /var/log    | logging output |

## Contributing ##

We welcome contributions!  Please see [here](CONTRIBUTING.md) for
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
