[![Deploy Application Docker K8s 2](https://github.com/diegargon/k8stest/actions/workflows/deploy-k8s-docker-2.yml/badge.svg)](https://github.com/diegargon/k8stest/actions/workflows/deploy-k8s-docker-2.yml)
[![CI for PHP App](https://github.com/diegargon/k8stest/actions/workflows/runson-php.yaml/badge.svg)](https://github.com/diegargon/k8stest/actions/workflows/runson-php.yaml)
[![Deploy Application Docker K8s](https://github.com/diegargon/k8stest/actions/workflows/deploy-k8s-docker.yml/badge.svg)](https://github.com/diegargon/k8stest/actions/workflows/deploy-k8s-docker.yml)

# k8stest

Testing github actions with self k8s cluster

k8s controller and runner set
Assumptions:
    1º working k8s cluster
    2º Helm
    3º github app secret
            kubectl create secret generic pre-defined-secret    --namespace=arc-runners    --from-literal=github_app_id=945429    --from-literal=github_app_installation_id=52825076    --from-literal=github_app_private_key='-----BEGIN RSA PRIVATE KEY----- ..... '


Basic configurations

Controller: (Works with all  self workflows)
    k8s-helms/gha-runner-scale-set-controller.yaml


Workflows 1:
    This runner set runs the project on k8s default image

    .github/workflows/runons-test
    .github/workflows/runons-php

    Runners Set

    k8s-helms/gha-runner-scale-set-nodocker.yaml


Workflows 2:

    This runner set runs the project in docker

    k8s-helms/gha-runner-scale-set-dockernodocker.yaml
        
        Simple php Test
        
        .github/workflows/deploy-k8s-docker.yml
            
        Build image/Dockerfile

        .github/workflows/deploy-k8s-docker-2.yml
        docker/Dockerfile

WARNING: 

Point to account not works if is not organization account

githubConfigUrl: "https://github.com/diegargon/"    

Point to repo works with all accounts:

githubConfigUrl: "https://github.com/diegargon/k8stest"    

