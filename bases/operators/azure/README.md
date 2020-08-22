# Setup Helm Secrets for Azure Operator

```bash
# Create a Service Principal
az ad sp create-for-rbac -n "cdw-azure-service-operator-20200821" --role contributor  --scopes /subscriptions/b9c770d1-cde9-4da3-ae40-95ce1a4fac0c

# Create the secrets
kubectl apply -f ./secrets.yaml
```