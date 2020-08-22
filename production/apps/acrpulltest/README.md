# Notes

Make sure the Service Principal or Managed Idenity of the AKS cluster has **AcrPull** permissions on the Azure Container Registry.

Also, make sure Helm sets the `registry.acr.enabled` value to `true` to ensure that Flux can use the ACR permissions to look for new tags in the container registry.
