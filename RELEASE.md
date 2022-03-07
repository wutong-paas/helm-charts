> Just use wutong-console for example.

Check your chart lint

```bash
helm lint wutong-console/
```

Pakcage charts & refresh the repo index:

```bash
helm package wutong-console
helm repo index --url https://wutong-paas.github.io/helm-charts/ .
```

If you need to add a new chart to the Helm char repository, it's mandatory for you to regenerate the `index.yaml` file. The `$ helm repo index` command will completely rebuild the `index.yaml` file from scratch, including only the charts that it finds locally, which very likely is our case. Howerver, it worth notice that you can use the `--merge` flag to incrementally add new charts to an existing index.yaml:

```bash
helm repo index --url https://wutong-paas.github.io/helm-charts/ --merge index.yaml .
```