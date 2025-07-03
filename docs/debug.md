# Debugging

## Things to Check

* RAM utilization -- bitcoind is very hungry and typically needs in excess of 1GB.  A swap file might be necessary.
* Disk utilization -- The bitcoin blockchain will continue growing and growing and growing.  Then it will grow some more.  At the time of writing, 40GB+ is necessary.

## Viewing bitcoinknots Logs

    docker logs bitcoinknots-node


## Running Bash in Docker Container

*Note:* This container will be run in the same way as the bitcoin knots node, but will not connect to already running containers or processes.

    docker run -v bitcoinknots-data:/bitcoin --rm -it aphex3k/bitcoinknots bash -l

You can also attach bash into running container to debug running bitcoin knots

    docker exec -it bitcoinknots-node bash -l


