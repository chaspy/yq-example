# yq-example

image tag を linux に変更したい

```
yq -i '(.spec.template.spec.containers[0].image = "hello-world:linux")' deployment.yaml
```

kustomization.yaml で deployment.yaml を patchesStrategicMerge から resources に変更する

```

```


