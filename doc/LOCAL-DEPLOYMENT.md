# Local deployment
Notes for deployment to a local cluster, like [minikube] or [Docker Desktop].

> It is assumed that you have a local Kubernetes cluster, built using
  minikube or Docker Desktop.

You will now need: -

- This repository (but you'll have that already)
- Python 3
- [lens]

## Create an environment for the Ansible playbooks
You will need a Python virtual environment for ansible playbook execution.
You may be running playbooks from several repositories, so you can re-use
this one.

You must use Python 3: -

    python -m venv  ~/.venv/ansible

    source ~/.venv/ansible/bin/activate
    pip install wheel
    pip install -r requirements.txt

## Deploy the UI
From the root of your clone of the `mini-apps-data-tier-ui-ansible` repository,
and within the Ansible environment you created in the previous step,
create a suitable Ansible parameter file called `parameters.yaml` using the
`parameters-template.yaml` file as a guide, replacing the `SetMe` lines.

>   You will need a KUBECONFIG file, and refer to it using the `dt_kubeconfig`
    variable and make sure `kubectl get no` returns nodes you expect.

>   You will need to provide the hostname of a Keycloak server to use
    for API authentication. A `/auth` endpoint will be expected at the
    hostname you provide. The keycloak server will need a `squonk` realm,
    and a suitable Data Manager client that allows _access from anywhere_.

Now deploy the UI: -

    ansible-playbook site.yaml -e @parameters.yaml

>   You can check the deployment progress using [Lens].

Using the above as an example, you should be able to connect to the
Account Server Swagger page at: -

    https://192.168.99.137.nip.io/account-server-ui

Or, if using Docker Desktop, at: -

    https://kubernetes.docker.internal/account-server-ui

---

[docker desktop]: https://www.docker.com/products/docker-desktop
[lens]: https://k8slens.dev
[minikube]: https://minikube.sigs.k8s.io/docs/start/
