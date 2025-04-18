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

In order to configure the volumes for the configuration and the data use the following properties:

```yaml
storage:
  config: # Where the configuration file, database, etc is stored
    size: 5Gi
  segments: # Where the recordings (video segments) are stored
    size: 15Gi
  snapshots: # Where the snapshots from object detection, motion detection, etc are stored
    size: 15Gi
  thumbnails: # Where the thumbnails for recordings triggered by trigger_event_recording are stored
    size: 5Gi
  eventclips: # Where the event clips created by create_event_clip are stored
    size: 5Gi
```

If you want to use [VAAPI](https://viseron.netlify.app/docs/documentation/installation#running-viseron), your `values.yaml` will need to define the `dri` mount point and allow viseron to run with privileges to access the DRI device.

```yaml
securityContext:
  privileged: true

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

For more details please visit the [viseron documentation](https://viseron.netlify.app/docs/documentation)
