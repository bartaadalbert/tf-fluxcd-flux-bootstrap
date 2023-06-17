# Terraform Flux Bootstrap Module

This is a Terraform module that bootstraps Flux (the GitOps Kubernetes operator) in your Kuber

netes cluster.
# Requirements

    Terraform 0.14.x or newer
    A Kubernetes cluster
    Git repository (GitHub is used in the example)

# Provider

This module uses the flux provider.
Usage

Here's an example of how you can use this module:

```hcl

module "flux_bootstrap" {
  source            = "github.com/bartaadalbert/tf-fluxcd-flux-bootstrap?ref=kind"
  github_repository = "${var.GITHUB_OWNER}/${var.FLUX_GITHUB_REPO}"
  github_token      = var.GITHUB_TOKEN
  private_key       = module.tls_private_key.private_key_pem
  config_host       = module.kind_cluster.endpoint
  config_client_key = module.kind_cluster.client_key
  config_ca         = module.kind_cluster.ca
  config_crt        = module.kind_cluster.crt
}
```
Please replace ${var.GITHUB_OWNER}, ${var.FLUX_GITHUB_REPO}, var.GITHUB_TOKEN, module.tls_private_key.private_key_pem, module.kind_cluster.endpoint, module.kind_cluster.client_key, module.kind_cluster.ca and module.kind_cluster.crt with your own values.

# Variables

    github_repository: GitHub repository to store Flux manifests.
    flux_namespace: The namespace where Flux will be installed (default: "flux-system").
    target_path: Subdirectory to store Flux manifests in the Git repository (default: "clusters").
    github_token: The token used to authenticate with the Git repository.
    private_key: The private key used to authenticate with the Git repository.
    config_path: The path to the kubeconfig file (default: "~/.kube/config").
    config_host: The Kubernetes API server URL (default: "gke").
    config_client_key: The client key for the Kubernetes cluster (default: "client_key").
    config_crt: The client certificate for the Kubernetes cluster (default: "ca").
    config_ca: The certificate authority for the Kubernetes cluster (default: "ca").
    dummy_input: An input to force module to wait for kind-config.
# Outputs

    flux_namespace: The namespace where Flux is installed.

# License

This project is licensed under the terms of the MIT license.

Please adapt this to your needs and provide more context and examples if necessary. For instance, you might want to explain what each variable and output is used for in more detail, provide more examples of usage, or include instructions for how to get the necessary inputs if they aren't obvious.
