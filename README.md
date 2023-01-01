# yq-example

## Version

```
yq --version
yq (https://github.com/mikefarah/yq/) version 4.27.2
```

## Example

To change the image tag to `linux` ,

```
yq -i '(.spec.template.spec.containers[0].image = "hello-world:linux")' base/deployment.yaml
```

To remove `deployment.yaml` from `patchesStrategicMerge` in `kustomization.yaml` and add it to `resources` ,

```
yq -i 'del(.patchesStrategicMerge[] | select(. == "deployment.ymal"))' "overlays/prd/kustomization.yaml"
yq -i '(.resources += "deployment.yaml")' "overlays/prd/kustomization.yaml"
```

To add `APP_ENV` key to `containers[0].env[1]` ,

```
yq -i '.spec.template.spec.containers[0].env[1].name = "APP_ENV"' base/deployment.yaml
```

To add a value of `containers.env[1]` (`APP_ENV`) via environment variable,

```
APP_ENV_VALUE="example"
APP_ENV_VALUE=$APP_ENV_VALUE yq e -i '.spec.template.spec.containers[0].env[1].value = strenv(APP_ENV_VALUE)' base/deployment.yaml
```

To add a new key via environment variable,

```
APP_ENV_KEY="newkey"
APP_ENV_KEY=$APP_ENV_KEY yq -i '.spec.template.metadata.labels[env(APP_ENV_KEY)] = "newvalue"' base/deployment.yaml
```
