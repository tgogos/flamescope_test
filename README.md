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


## run `iperf` server with Docker

    # use the host network stack:
    sudo docker run  -it --rm --name=iperf3-server --net=host networkstatic/iperf3 -s
    
    # use the default bridge (slower)
     sudo docker run  -it --rm --name=iperf3-server -p 5201:5201 networkstatic/iperf3 -s
 
 
 ## run `iperf` server with Kubernetes
 
     kubectl apply -f iperf_k8s_deployment.yaml
     kubectl apply -f iperf_k8s_service.yaml
