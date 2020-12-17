# API Gateway via Flux

## Secrets for APIM Gateway

When you create the self-hosted gateway for the API Management service, you
will be provided with instructions for deployment. You will need to translate
these steps into a config.yaml file, which will then need to be applied to the
cluster manually.

> NOTE: Use the [config-sample.yaml](config-sample.yaml) file as a template.

## Apply the Config

Now that we have a full set of config and secrets, apply the config.yaml file.

```bash
kubectl apply -f config.yaml
```

## Add a Flux Config for API Gateway

> NOTE: The `operator-namespace` must match the value provided in [kustomization.yaml](kustomization.yaml).

```bash
