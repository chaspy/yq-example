# yq-example

image tag を linux に変更したい

```
yq -i '(.spec.template.spec.containers[0].image = "hello-world:linux")' base/deployment.yaml
```

kustomization.yaml で deployment.yaml を patchesStrategicMerge から resources に変更する

```
yq -i 'del(.patchesStrategicMerge[] | select(. == "deployment.ymal"))' "overlays/prd/kustomization.yaml"
yq -i '(.resources += "deployment.yaml")' "overlays/prd/kustomization.yaml"
```

containers.env のキーを追加する

```
yq -i '.spec.template.spec.containers[0].env[1].name = "APP_ENV"' base/deployment.yaml
```

containers.env[1] (APP_ENV) の value を環境変数から追加する

```
APP_ENV_VALUE="example"
APP_ENV_VALUE=$APP_ENV_VALUE yq e -i '.spec.template.spec.containers[0].env[1].value = strenv(APP_ENV_VALUE)' base/deployment.yaml
```

