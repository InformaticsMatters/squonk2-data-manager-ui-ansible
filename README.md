# Ansible playbook to deploy the Squonk2 Data Manager UI

![lint](https://github.com/InformaticsMatters/squonk2-data-manager-ui-ansible/workflows/lint/badge.svg)

![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/informaticsmatters/squonk2-data-manager-ui-ansible)

[![CodeFactor](https://www.codefactor.io/repository/github/informaticsmatters/squonk2-data-manager-ui-ansible/badge)](https://www.codefactor.io/repository/github/informaticsmatters/squonk2-data-manager-ui-ansible)

An Ansible playbook and role normally launched form an AWX server instance
that deploys our Squonk2 [Data Manager UI] as a Kubernetes **StatefulSet**
with **Service** and **Ingress**.

## Deploying for development (Docker Desktop)
You can deploy the UI to a local (Minikube or Docker Desktop) cluster using a
suitable set of parameters. An example file is present in the project root
(`parameters.yaml`).

You will need: -

-   A local cluster ([Minikube] or [Docker Desktop])
-   `kubectl` (known to work with `v1.22.4`)
-   Python 3

>   Refer to the Data Manger documentation for details on Minikube or
    Docker Desktop configuration

Use a suitable environment: -

    python -m venv ~/.venv/mini-apps-data-tier-ui-ansible

    source ~/.venv/mini-apps-data-tier-ui-ansible/bin/activate
    pip install --upgrade pip
    pip install -r requirements.txt

And a local cluster config, here we keep our files in the home directory
`k8s-config` and have a config file for our cluster called `config-local`: -

    export KUBECONFIG=~/k8s-config/config-local

Check the cluster connection with kubectl: -

    kubectl get no

Review the parameter template and copy it to `parameters.yaml`, changing
variables as required.

With the config and parameters prepared you can now run the playbook
to install the UI: -

    ansible-playbook site.yaml -e @parameters.yaml

---

[data manager ui]: https://github.com/InformaticsMatters/squonk2-data-manager-ui
[docker desktop]: https://www.docker.com/products/docker-desktop
[minikube]: https://minikube.sigs.k8s.io/docs/start/
