# Add admission control

## Add the admission controller

Validating webhook admission control should be enabled by default in 1.13.
Run webhook-certs.sh to generate the secret containing the certificates that the webhook server uses.
Run the admission controller.

```bash
kubectl apply -f https://raw.githubusercontent.com/lizrice/kubecon-seattle/master/admission/admission.yaml
```

## Try applying this-is-fine again

```bash
kubectl apply -f https://raw.githubusercontent.com/lizrice/kubecon-seattle/master/this-is-fine.yaml
```

The service account creation isn't permitted.

## Opting out of service account tokens

Opt out of automounting API credentials for a service account:

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: my-sa
automountServiceAccountToken: false
```

Opt out of automounting API credentials for a particular pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  serviceAccountName: my-sa
  automountServiceAccountToken: false
```

## Delete this-is-fine again

```bash
kubectl delete -f https://raw.githubusercontent.com/lizrice/kubecon-seattle/master/this-is-fine.yaml
```

[Next](./PAGE-4.md)