- Get all pods with selector

`k get pod --selector env=dev`

- number of pods with selector env=dev:

`k get pod --selector env=dev | wc -l` but this will also count the header, so subtract 1, otherwise:

`k get pod --selector env=dev --no-headers | wc -l`

To install Metrics server add this in args : `--kubelet-insecure-tls`
