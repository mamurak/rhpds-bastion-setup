# Playbook to provision all needed resources

This playbook is used to provision all required resources (configurations, operators, OCP resources) that are needed for the ML/CI-CD pipelines and scenario.
It uses a custom Execution Environment with preloaded collections and roles needed for setting up the environment.

## Preliminary steps

### Environment setup

Install *ansible navigator* for your setup following [instructions](https://ansible-navigator.readthedocs.io/en/latest/installation/)

### Fill the inventory

The inventory needs to be populated with the **bastion** host information:

    [rhods_bastion]
    your_bastion_hostname_here ansible_user=your_bastion_username_here ansible_ssh_pass=your_bastion_password_here ansible_ssh_common_args='-o StrictHostKeyChecking=no'

### Fill the user_vars.yml file

    git_repo: ## The URL of the fork in your user profile
    git_branch: ## The branch you are going to work on

    quay_auth_token: ## Your Quay authentication token (base64 encoded) used to pull/push the images
    github_access_token: ## The access token for your Github account - [guide for retrieving it](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
    github_account: ## your Github account name
    s3_secret: nothing ## this field is not used at this time

    ocp_username: ## The OCP of the admin user in your cluster
    ocp_password: ## The Password of the admin unser in your cluster
    ocp_api_url: ## The API URL of your OCP Cluster

## Run the playbook

Once your variables and inventory will be filled up, you can proceed running the playbook:

    ansible-navigator run -i inventory -m stdout bastion-provisioner.yml

At the end of the execution, the relevant URLs for the different ArgoCD Instances will be provided, as well as the resource deployment, pipeline execution and operator setup will be initiated on the cluster.


