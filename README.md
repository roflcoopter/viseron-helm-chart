## Introduction

This is a helm chart for the [viseron](https://viseron.netlify.app) application.

## Usage

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

```sh
helm repo add viseron https://roflcoopter.github.io/viseron-helm-chart
```

If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the package.  You can then run `helm search repo
viseron -l` to see the different versions of the chart.

To install/upgrade the viseron chart:

```sh
helm -n my-viseron-namespace upgrade --create-namespace --install --values "my-viseron-values.yaml" my-viseron  viseron/viseron
```

To uninstall the chart:

```sh
helm -n my-viseron-namespace delete my-viseron
```

## Configuration

There are key sections in your `values.yaml` file that you will want to define.

For example, if you want to use [VAAPI](https://viseron.netlify.app/docs/documentation/installation#running-viseron), your `values.yaml` will need to define the `dri` mount point.

```yaml
volumes:
  - name: dev-dri
    hostPath:
      path: /dev/dri

volumeMounts:
  - name: dev-dri
    mountPath: /dev/dri
```

If you want to use [Google Edge TPU](https://coral.ai/products/), your `values.yaml` will need to have this instead:

```yaml
securityContext:
  privileged: true

volumes:
  - name: dev-usb
    hostPath:
      path: /dev/bus/usb

volumeMounts:
  - name: dev-usb
    mountPath: /dev/bus/usb
```

Another important configuration is the volumes to store the configuration and the recordings. For example, setting `50Mi` for the config storage, and `200Gi` for the recordings:

```yaml
storage:
  config:
    size: 50Mi
  data:
    size: 200Gi
```

For more details please visit the [viseron documentation](https://viseron.netlify.app/docs/documentation)
