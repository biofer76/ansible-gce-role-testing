# ansible-gce-role-testing
A set of Ansible Playbooks to run and test the Ansible GCE Role

## Requirements 

* Ansible 2.7+
* Ansible Google Cloud collection
* Python 3.6+
* google-auth Python package

This repo includes the Ansible GCE Role project: https://github.com/devxops/ansible-role-gce  
More information regarding GCE VM configuration available here: https://github.com/devxops/ansible-role-gce/blob/main/README.md

## GCP Project config

GCP Project configuration must be set as environment variables:

* `GCP_PROJECT_ID`
  The ID of your Google Project
* `GCP_SERVICE_ACCOUNT_FILE`
  Path of your service account files

**Suggestion:** Add a `.env` file in project root and load through `source .env`command. 

```
GCP_PROJECT_ID=project-id
GCP_SERVICE_ACCOUNT_FILE=/path/to/my-secret-service-account.json
```

## Manage VM instances on GCP

How to create and remove a VM instance on Google Cloud through GCE Ansible role, Playbooks are executed in localhost.

### Create

It creates a new Google Cloud VM instance based on default configuration (`roles/gce/defaults/main.yml`)

Before launching the Playbook you must set a real service account for VM instance, usually is the default Compute Engine default service account.
You can find it in GCP > IAM with the pattern `000000000000-compute@developer.gserviceaccount.com`

In Playbook files I used a new environment variable to configure the instance service account value, you could also add it to the `.env` file.

```
GCP_INSTANCE_SERVICE_ACCOUNT=000000000000-compute@developer.gserviceaccount.com
```

Required roles for Ansible service account:
* Compute Admin
* DNS Administrator
* Service Account User

**Run the Ansible Playbook with default values**

```bash
ansible-playbook create.yml
```

