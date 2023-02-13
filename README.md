# terraform-kubernetes-deployment-api

This Terraform module creates a Deployment for Kubernetes along with a Horizontal Pod Autoscaler and a Service. The deployment includes a container with various configurations such as environment variables, volumes, resources, liveness and startup probes, etc.

## How to use

```hcl
module "deployment" {
  source  = "graphnode-technologies/deployment-api/kubernetes"
  version = "1.4.0"

  name                = "example"
  namespace           = "default"
  replicas            = 1
  image               = "nginx:latest"
  args                = ["nginx", "-g", "daemon off;"]
  service_account_name = "example-service-account"
  environment_vars    = {
    EXAMPLE_VAR = "example_value"
  }
}
```

## Resources created

- Kubernetes Deployment
- Kubernetes Horizontal Pod Autoscaler (optional)
- Kubernetes Service (optional)
- Kubernetes Ingress (optional)


## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
| args | The arguments passed to the image | list(string) | `[]` | no |
| create_service | If a service should be created for this deployment | bool | `false` | no |
| environment | The environment that the deployment is deployed to | string | `"development"` | no |
| environment_vars | The environment variables passed to the deployment | map(string) | `{}` | no |
| extra_annotations | Additional annotations to add to the deployment | map(string) | `{}` | no |
| extra_volume_mounts | Additional volume mounts for the deployment | map(string) | `{}` | no |
| extra_volume_secrets | Additional secrets to mount for the deployment | map(string) | `{}` | no |
| extra_ingress_annotations | Additional annotations for the ingress resources | map(string) | `{}` | no |
| health_check | The health check configuration for the deployment | object | `{ port = 3000, path = "/health" }` | no |
| image | The image for the deployment | string | - | yes |
| limits | The resource limits for the deployment | object | `{ cpu = "100m", memory = "128Mi" }` | no |
| liveness_delay | The delay for liveness probes | object | `{ initial_delay_seconds = 60, period_seconds = 30 }` | no |
| max_replicas | The maximum number of replicas for the deployment | number | `1` | no |
| name | The name of the deployment | string | `"main"` | no |
| domain_name | The domain for the ingress | string | `""` | no |
| namespace | The namespace that the deployment is deployed to | string | `"default"` | no |
| requests | The resource requests for the deployment | object | `{ cpu = "50m", memory = "64Mi" }` | no |
| replicas | The number of replicas for the deployment | number | `1` | no |
| secret_environment_vars | The secret environment variables passed to the deployment | list(object) | `[]` | no |
| service_account_name | The name of the service account to run the deployment as | string | `"default"` | no |
| startup_failure_threshold | The number of consecutive failures to tolerate during startup before giving up | number | `3` | no |

## Outputs

| Name | Description |
|------|-------------|
| name | The name of the deployment |