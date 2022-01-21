# deploy-service

A reusable workflow that you can use to deploy a service to Kubernetes.

# to be injected

          app_name: prevent-ui
          namespace: development
          docker_image: 387308402250.dkr.ecr.eu-north-1.amazonaws.com/prevent-ui:9628f958eb4a69571cfee558624fa0a33fa49c4f

          # These are optional
          replicas: 1
          port: 80
          container_port: 80
          ingress: true
          ingress_host: prevent.dev.dignio.dev
          ingress_path: /

          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: eu-north-1

          KUBE_CONFIG: ${{ secrets.KUBE_CONFIG }}
      - name: Authenticate with Kubernetes
        uses: azure/k8s-set-context@v1
        with:
          method: kubeconfig
          kubeconfig: ${{ secrets.KUBE_CONFIG }}

      - name: Deploy to Kubernetes
        uses: Azure/k8s-deploy@v1
        with:
          manifests: |
              k8s.manifest.yaml
          kubectl-version: 'latest'
