![GithubTest](https://img.shields.io/badge/Github-Test-blue)
[![Deploy Application Docker K8s 2](https://github.com/diegargon/k8stest/actions/workflows/deploy-k8s-docker-2.yml/badge.svg)](https://github.com/diegargon/k8stest/actions/workflows/deploy-k8s-docker-2.yml)
[![CI for PHP App](https://github.com/diegargon/k8stest/actions/workflows/runson-php.yaml/badge.svg)](https://github.com/diegargon/k8stest/actions/workflows/runson-php.yaml)
[![Deploy Application Docker K8s](https://github.com/diegargon/k8stest/actions/workflows/deploy-k8s-docker.yml/badge.svg)](https://github.com/diegargon/k8stest/actions/workflows/deploy-k8s-docker.yml)
[![CodeSniffer](https://github.com/diegargon/k8stest/actions/workflows/code-sniffer.yml/badge.svg)](https://github.com/diegargon/k8stest/actions/workflows/code-sniffer.yml)
[![PhpStan](https://github.com/diegargon/k8stest/actions/workflows/phpstan.yml/badge.svg)](https://github.com/diegargon/k8stest/actions/workflows/phpstan.yml)
![License](https://img.shields.io/github/license/diegargon/k8stest)

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
    
    Files:

    k8s-helms/gha-runner-scale-set-controller.yaml

    Install/Upgrade:

    helm upgrade --install -n arc-systems --create-namespace arc oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set-controller -f gha-runner-scale-set-controller.yaml


Runner Set

    Install
    
    helm upgrade --install -n arc-runners  --create-namespace arc-runner-set  oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set -f gha-runner-scale-set.yaml


Workflows 1:

    This runner set runs the project on k8s with the default github action image

    k8s-helms/gha-runner-scale-set-nodocker.yaml

    Files: 

        .github/workflows/runons-test

        .github/workflows/runons-php


Workflows 2:

    This runner set runs the project in docker (Works too for no docker)

    k8s-helms/gha-runner-scale-set-docker.yaml
        
        ## Simple php Test
        
        Files: 

            .github/workflows/deploy-k8s-docker.yml
            
        ## Build image/Dockerfile and run phpunit

        Files: 

            .github/workflows/deploy-k8s-docker-phpunit.yml
        
            docker/Dockerfile



WARNING: 

Point to account not works if is not organization account

githubConfigUrl: "https://github.com/diegargon/"    

Point to repo works with all type accounts:

githubConfigUrl: "https://github.com/diegargon/k8stest"    

