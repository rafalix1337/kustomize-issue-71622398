Not working example.

```
kustomize-issue-71622398/not_working_example# kustomize build . | yq -Y -r '. | select (.kind == "Deployment")|.'
Error: accumulating resources: accumulation err='accumulating resources from 'backend': '/mnt/c/repos/kustomize-issue-71622398/not_working_example/backend' must resolve to a file': recursed accumulation of path '/mnt/c/repos/kustomize-issue-71622398/not_working_example/backend': add operation does not apply: doc is missing path: "/spec/template/spec/containers/0/envFrom/-": missing value

```