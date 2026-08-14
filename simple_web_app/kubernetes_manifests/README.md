# Deploy workloads to Kubernetes

## Steps:

1. Clone the repository

2. Build the docker image from `simple_web_app_*` folder

3. Tag the image:

   ```bash
   docker tag docker.io/library/simple-web-server localhost:5001/simple_web_app
   ```

3. Create kind cluster with registry using:

   ```bash
   ./kind-with-registry.sh
   ```

4. Deploy manifests to Kubernetes

## Troubleshooting variant

`kubernetes-manifests-variant.yaml` is an alternative deployment used for the
troubleshooting exercise. It is the same application, but the manifests contain
several deliberate misconfigurations for the candidate to find and fix.

One of the problems involves a `NetworkPolicy`. The default kind CNI (kindnet)
does **not** enforce NetworkPolicy, so that problem is invisible on a standard
cluster. Use the provided script to create a cluster with a policy-enforcing CNI
(Calico) instead of `kind-with-registry.sh`:

```bash
./kind-with-calico.sh
```

Then build/load the image and deploy `kubernetes-manifests-variant.yaml`.
