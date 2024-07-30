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
        .github/workflows/deploy-k8s-docker.yml
        .github/workflows/deploy-k8s-docker-2.yml


WARNING: 

Point to account not works if is not organization account

githubConfigUrl: "https://github.com/diegargon/"    

Point to repo works with all accounts:

githubConfigUrl: "https://github.com/diegargon/k8stest"    

