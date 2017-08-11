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

### Example Command-Line Docker Interaction

    docker start cucumber && docker attach cucumber

### Adding Ruby Gems to Containers
The expectation is that your project's source code is being mounted at
*/usr/local/src*, and that you will want to run the gems bundled into
your application's source code. However, some testers don't have the
luxury of having their testing harness included in the mainline. If
that's your case, you can pull down any Gemfile you like and then
`bundle install` them into the VM's environment.

If you don't have your own, consider using the author's
[Cucumber-centric Gemfile][7] as a base. For example, assuming your Git
repository is already mounted properly:

    cd /usr/local/src
    curl -sLo Gemfile https://goo.gl/iNsBjr
    bundle install

    # Tell Git to ignore your custom files.
    for file in Gemfile{,.lock} .bundle do
        echo "$file" >> .git/info/exclude
    done

Other solutions, such as installing the bundle in your home directory
and relying on rbenv shims to invoke the right gems without calling
`bundle exec` (which won't find a bundle in some other directory), are
certainly possible. This will install shims for your currently-select
Ruby, which you can use the installed gems almost anywhere that it isn't
being overriden simply by omitting `bundle`exec`.


[1]: http://www.gnu.org/graphics/gplv3-88x31.png
[2]: http://www.gnu.org/copyleft/gpl.html
[3]: http://i.creativecommons.org/l/by-nc-sa/3.0/us/88x31.png
[4]: https://creativecommons.org/licenses/by-nc-sa/4.0/
[5]: https://codenvy.io
[6]: https://hub.docker.com/r/codegnome/cucumber-centos7/
[7]: https://goo.gl/iNsBjr
