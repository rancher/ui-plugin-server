# Plugin Server Base Chart
This chart serves as a base for developing plugins for the Rancher UI. It contains all the templates for deploying a fileserver to server plugin related files and is designed to be integrated with the Rancher Plugin controller. To use this base chart for your plugin a few edits need to be made.

## Building the Plugin Server Image
First start by copying the files you wish to serve into the `/plugin` directory. Any file in this directory will be packaged on to the docker image being used for the plugin server. Once the files are there, you can build the image using `package/Dockerfile` as your dockerfile and then make sure to push the image to a Docker Repository and tag it. This repository will be used in the chart's `values.yaml`.

## Updating the Chart
You will want to change certain values in `charts/values.yaml` and `charts/Chart.yaml` in order to deploy this to a cluster. In `charts/values.yaml`, make sure to update the repository and tag values. In `charts/Chart.yaml`, make sure to update the chart's name and description to match your plugin. 

## Deployment
After these edits all that's left is to deploy the chart through the method of your choice.
Example install command:
`helm upgrade --install test-plugin ./charts --namespace cattle-ui-plugin-system --create-namespace`
