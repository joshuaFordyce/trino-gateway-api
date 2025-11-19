

This guide covers the necessaray steps to deploy and test the Gateway API resources to expose the Trino Coordinator Service externally

1. Prerequisites and Deployment Setup
    - Istio Gateway Controller installed
        - The underlying controller must be running on the cluster. T
    - The application namespace and the Gateway namespace must be created
    - Make sure that the trino Coordinator Service is running in the trino-ftr namespace  

2. Deployment Steps
    1. Apply the Gateway API Definitions
    ```
    Kubectl apply -f trino-gateway-api.yaml
    ```

    2. Verify GatewayClass Acceptance
    ```
    kubectl get gatewayclass istio-trino-class
    # should show 'Accepted: True'
    ```

    3. Verify Gateway Listener Status
    ```
    kubectl get gateway trino-external-gateway -n gateway-system
    ```

    4. Verify HTTPRoute Attachement
    ```
    kubectl describe httproute trino-api-route -n trino-ftr
    # Check the ParentRefs status section and make sure it says 'Condition: Programmed: True'
    ```

3. Validation and testing(use the trino /v1/info endpoint to confirm that traffic hitting th external Gateway IP/Hostname is successfully routed to the internal Trino Coordinator)

    1. Identify the Gatway Address

        ```
        # Replace <GATEWAY_IP_OR_HOSTNAME> with the actual value from Step 2.3
        GATEWAY_ADDRESS=$(kubectl get gateway trino-external-gateway -n gateway-system -o jsonpath='{.status.addresses[0].value}')
        echo "Gateway Address: $GATEWAY_ADDRESS"
        ```
    2. Execute the Test Command (Direct HTTP on Port 80):

        ```
        curl -s -I http://$GATEWAY_ADDRESS/v1/info
        ```
