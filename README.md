Trino Coordinator Exposure via Kubernetes Gateway API (Istio)
This repository provides the Kubernetes Gateway API resource definitions (Gateway, HTTPRoute) to expose the internal Trino Coordinator Service externally using the Istio Gateway Controller.


Provide a public endpoint for the Trino Coordinator Service running in the trino-ftr namespace, leveraging Istio's advanced traffic management capabilities.

Prerequisites
Istio Gateway Controller installed and running.

Application namespace (trino-ftr) and Gateway namespace (gateway-system) created.

Trino Coordinator Service running in the trino-ftr namespace.

Deployment
Apply the provided Gateway API definitions to your cluster:

Bash

kubectl apply -f trino-gateway-api.yaml