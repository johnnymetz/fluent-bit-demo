# fluent-bit-demo

Fluent Bit Demo

Based on [GitHub - fluent/fluent-bit-kubernetes-logging: Fluent Bit Kubernetes Daemonset](https://github.com/fluent/fluent-bit-kubernetes-logging#getting-started)

## Getting Started

Create app with logs in default namespace:

```
kubectl apply -f ./counter.yaml
kubectl logs pod/counter
```

Next, replace the host path in `fluent-bit-daemonset.yaml` with the absolute path to the `logs/` in this repo, e.g. /path/to/logs

Create fluent bit daemonset:

```
kubectl create ns logging

kubectl apply -f https://raw.githubusercontent.com/fluent/fluent-bit-kubernetes-logging/master/fluent-bit-service-account.yaml
kubectl apply -f https://raw.githubusercontent.com/fluent/fluent-bit-kubernetes-logging/master/fluent-bit-role-1.22.yaml
kubectl apply -f https://raw.githubusercontent.com/fluent/fluent-bit-kubernetes-logging/master/fluent-bit-role-binding-1.22.yaml

kubectl apply -f fluent-bit-configmap.yaml
kubectl apply -f fluent-bit-daemonset.yaml
```

Notice the `logs/` folder is populated with several files, including one for the `counter` pod.

## Development

```
kubectl delete -f fluent-bit-daemonset.yaml
kubectl apply -f fluent-bit-configmap.yaml
kubectl apply -f fluent-bit-daemonset.yaml
```

## Cleanup

```
kubectl delete -n default pod/counter
kubectl delete ns logging
```

## Resources

- [Kubernetes - Fluent Bit: Official Manual](https://docs.fluentbit.io/manual/installation/kubernetes)
- [GitHub - fluent/fluent-bit-kubernetes-logging: Fluent Bit Kubernetes Daemonset](https://github.com/fluent/fluent-bit-kubernetes-logging)
