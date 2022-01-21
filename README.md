# deploy-service

A reusable workflow that you can use to deploy a service to Kubernetes.

## Usage

```yaml
jobs:
  call-deploy-workflow:
    uses: dignio/deploy-service/.github/workflows/deploy-workflow.yaml@main
    with:
      # Required
      app_name: prevent-ui
      namespace: development
      docker_image:
      aws_region: eu-north-1

      # Optional
      replicas: 1
      port: 80
      container_port: 3000
      ingress: true
      ingress_host: prevent.dev.dignio.dev
      ingress_path: /

    # Required secrets
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      # This has to be a base64 encoded kube config file
      KUBE_CONFIG: ${{ secrets.KUBE_CONFIG }}
```
