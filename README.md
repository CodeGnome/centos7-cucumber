# centos7-cucumber

Home of the [com.codegnome.centos7-cucumber][6] Docker image.

## Copyright and Licensing

### Copyright Notice

The copyright for the software, documentation, and associated files are
held by the author.

    Copyright © 2015, 2016, 2017 Todd A. Jacobs
    All rights reserved.

The AUTHORS file is also included in the source tree.

### Software License

![GPLv3 Logo][1]

The software is licensed under the [GPLv3][2]. The LICENSE file is
included in the source tree.

### README License

![Creative Commons BY-NC-SA Logo][3]

This README is licensed under the [Creative Commons
Attribution-NonCommercial-ShareAlike 4.0 International License][4].

## Purpose

This is a CentOS 7 image with the latest stable Ruby interpreter, and a
system install of rbenv for managing Ruby and the gems needed to provide
a portable Cucumber testing environment. It generates CentOS 7
containers for Cucumber testing.

More generally, it can be (ab)used to provide a Docker-based VM (of
sorts) for running your Cucumber tests locally, or share your QA
platforms during pairing on Docker-enabled platforms like [CodeEnvy][5].
You replace a full-featured VM or CI server with this Docker image at
your own risk.

## Installation and Setup

    docker pull codegnome/centos7-cucumber

    cd /path/to/source/code

    docker run \
        --init \
        --interactive \
        --tty \
        --name cucumber \
        --volume "$PWD":/usr/local/src \
        codegnome/cucumber-centos7

## Usage

    docker start cucumber && docker attach cucumber


[1]: http://www.gnu.org/graphics/gplv3-88x31.png
[2]: http://www.gnu.org/copyleft/gpl.html
[3]: http://i.creativecommons.org/l/by-nc-sa/3.0/us/88x31.png
[4]: https://creativecommons.org/licenses/by-nc-sa/4.0/
[5]: https://codenvy.io
[6]: https://hub.docker.com/r/codegnome/cucumber-centos7/
