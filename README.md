## Usage

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

```sh
helm repo add viseron https://carlosrodfern.github.io/viseron-helm-chart
```

If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the package.  You can then run `helm search repo
viseron -l` to see the different versions of the chart.

To install the viseron chart:

```sh
helm install my-viseron viseron/viseron
```

To uninstall the chart:

```sh
helm delete my-viseron
```

## Configurations

There are key parts in your `values.yaml` file that you will want to define.

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

Another important one is storage with the `storage` tag. For example, setting `50Mi` for the config storage, and `200Gi` for the recordings:

```yaml
storage:
  config:
    size: 50Mi
  data:
    size: 200Gi
```
