# talltechdude.argocd
=========

Ansible role for deploying ArgoCD and App of Apps to Kubernetes Cluster

Requirements
------------

 - Existing Kubernetes Cluster

Role Variables
--------------

See defaults/main.yml
```
argocd_namespace: argocd

argocd_admin_password: "supersecretpassword"

argocd_hostname: argocd.localhost
argocd_tls_cert: argocd-certificate
argocd_ingress_annotations: ~


kubeconfig_file: "~/.kube/config"
kube_api_url: "https://{{ ansible_host }}:443"

argocd_apps:
  name: application
  version: 1.0.0
  path: apps
  repoURL: https://github.com/argoproj/argocd-example-apps
  repositories: |
    - url: {{ argocd_apps.repoURL }}
  repository_credentials: ~
```

Dependencies
------------

None

Example Playbook
----------------

```
- name: ArgoCD Install
  hosts: k8s
  gather_facts: false
  vars:
    kubeconfig_file: "{{ inventory_dir }}/kubeconfigs/{{ inventory_hostname }}.kubeconfig.yaml"
  roles:
    - talltechdude.argocd
```

License
-------

MIT
