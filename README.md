# (Netflix) Flamescope Test

Tests with `iperf`, `docker`, `kubernetes`

## prerequisites

    sudo apt install linux-tools-4.15.0-42-generic

## how to take system-wide profiles

    sudo perf record -F 99 -a -g -- sleep 30
    sudo perf script > a-filename-here.perf

## how to install & run flamescope

    # clone repo
    git clone https://github.com/Netflix/flamescope
    
    # build docker image
    cd flamescope/
    docker build -t flamescope .
    sudo docker build -t flamescope .
    
    # run and use a volume with your .perf files inside
    sudo docker run --rm -it -v /path/to/.perf/files/:/profiles:ro -p 5000:5000 flamescope
