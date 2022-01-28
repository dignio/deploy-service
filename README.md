# deploy-service

A composite action that you can use to deploy a service to Kubernetes.

## Usage

```yaml
on: [push]

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: dignio/deploy-service@v1
        with:
          # === Required
          app_name: prevent-ui
          service_type: webservice
          namespace: development
          docker_image: <org_id>.dkr.ecr.<aws_region>.amazonaws.com/<repo_name>:<docker_tag>
          aws_region: eu-north-1

          # === Optional
          replicas: 1
          port: 80
          container_port: 3000
          ingress: true
          ingress_host: prevent.dev.dignio.dev
          ingress_path: /

          # === Required secrets
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          # This has to be a base64 encoded kube config file
          KUBE_CONFIG: ${{ secrets.KUBE_CONFIG }}
```
