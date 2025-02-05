- Get all pods with selector

`k get pod --selector env=dev`

- number of pods with selector env=dev:

`k get pod --selector env=dev | wc -l`
