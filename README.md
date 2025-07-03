Bitcoin Knots for Docker
===================

[![Docker Stars](https://img.shields.io/docker/stars/aphex3k/bitcoinknots.svg)](https://hub.docker.com/r/aphex3k/bitcoinknots/)
[![Docker Pulls](https://img.shields.io/docker/pulls/aphex3k/bitcoinknots.svg)](https://hub.docker.com/r/aphex3k/bitcoinknots/)
[![Build Status](https://travis-ci.org/aphex3k/docker-bitcoinknots.svg?branch=master)](https://travis-ci.org/aphex3k/docker-bitcoinknots/)

Docker image that runs the Bitcoin knots node in a container for easy deployment.


Requirements
------------

* Physical machine, cloud instance, or VPS that supports Docker (i.e. [Vultr](http://bit.ly/1HngXg0), [Digital Ocean](http://bit.ly/18AykdD), KVM or XEN based VMs) running Ubuntu 14.04 or later (*not OpenVZ containers!*)
* At least 700 GB to store the block chain files (and always growing!)
* At least 1 GB RAM + 2 GB swap file

Recommended and tested on unadvertised (only shown within control panel) [Vultr SATA Storage 1024 MB RAM/250 GB disk instance @ $10/mo](http://bit.ly/vultrbitcoinknots).  Vultr also *accepts Bitcoin payments*!


Really Fast Quick Start
-----------------------

One liner for Ubuntu 14.04 LTS machines with JSON-RPC enabled on localhost and adds upstart init script:

    curl https://raw.githubusercontent.com/aphex3k/docker-bitcoinknots/master/bootstrap-host.sh | sh -s trusty


Quick Start
-----------

1. Create a `bitcoinknots-data` volume to persist the bitcoin knots blockchain data, should exit immediately.  The `bitcoinknots-data` container will store the blockchain when the node container is recreated (software upgrade, reboot, etc):

        docker volume create --name=bitcoinknots-data
        docker run -v bitcoinknots-data:/bitcoin/.bitcoin --name=bitcoinknots-node -d \
            -p 8333:8333 \
            -p 127.0.0.1:8332:8332 \
            aphex3k/bitcoinknots

2. Verify that the container is running and bitcoin knots node is downloading the blockchain

        $ docker ps
        CONTAINER ID        IMAGE                         COMMAND             CREATED             STATUS              PORTS                                              NAMES
        d0e1076b2dca        aphex3k/bitcoinknots:latest     "btc_oneshot"       2 seconds ago       Up 1 seconds        127.0.0.1:8332->8332/tcp, 0.0.0.0:8333->8333/tcp   bitcoinknots-node

3. You can then access the daemon's output thanks to the [docker logs command](https://docs.docker.com/reference/cli/docker/service/logs/)

        docker logs -f bitcoinknots-node

4. Install optional init scripts for upstart and systemd are in the `init` directory.


Documentation
-------------

* Additional documentation in the [docs folder](docs).
