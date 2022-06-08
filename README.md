# deploy-service

A composite action that you can use to deploy a service to Kubernetes.

## Usage

```yaml
on: [push]

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: dignio/deploy-service@v3
        with:
          # === Required
          app_name: prevent-demo
          instance: development
          service_type: webservice
          namespace: development
          docker_image: <org_id>.dkr.ecr.<aws_region>.amazonaws.com/<repo_name>:<docker_tag>
          aws_region: eu-north-1
          aws_role: <insert_aws_role>

          # === Optional
          replicas: 1
          port: 80
          container_port: 3000
          container_size: "medium"
          container_command: '["curl"]'
          container_args: '["-I", "https://www.dignio.com"]'
          secretsmanager: true
          cluster_name: demo-cluster
```
