# Notes

For some reason, Flux isn't creating the CRD instance from the redis.yaml file here.

To fix that, deploy the redis.yaml file manually.

```bash
k apply -f redis.yaml
```

Then, delete the apps pods and let them recreate. It should then work.
