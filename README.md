# prometheusForTekton

## Overview

The run-prometheus task is designed to automate the setup and execution of Prometheus, a powerful monitoring and alerting toolkit. This task creates the necessary configuration for Prometheus, runs the server, and allows users to easily access the monitoring data.

### Parameters

1.prometheus_storage: PersistentVolumeClaim to be used for storing the Prometheus configuration and data.
2.prometheus_port: Port on which the Prometheus server will listen. Defaults to 9090.

## Workspaces

1.prometheus-storage: A PersistentVolumeClaim-type workspace for storing Prometheus configuration and data.

## Steps

### Write Configuration: This step creates the prometheus.yml configuration file in the specified workspace.

### Run Prometheus: This step executes the Prometheus server using the configuration provided in the previous step.

## Platforms

The Task can be run on linux/amd64 platform.


## Steps to Implement

1.Create the ConfigMap & PersistentVolumeClaim : Ensure you apply the PVC before running the Task:

kubectl create configmap prometheus-config --from-file=prometheus.yml

kubectl apply -f prometheus-pvc.yaml

2.Run the Task & Taskrun: Execute the TaskRun to start Prometheus:

kubectl apply -f run-prometheus.yaml
kubectl apply -f run-prometheus-run.yaml

3.Verify the TaskRun: Check the status of the TaskRun to see if it completed successfully:

tkn taskrun logs run-prometheus-run -f

4.Create the Service: After the TaskRun, create the service for Prometheus:

kubectl apply -f prometheus-service.yaml

5.Port-Forward to Access Prometheus: Finally, access Prometheus using:

kubectl port-forward svc/prometheus-service 9090:9090

Access Prometheus: Open your web browser and navigate to http://localhost:9090 to access the Prometheus UI.

Important Notes
Adjust the labels in the Service definition to match your Prometheus pod's labels.
Ensure that the PVC is correctly provisioned before the TaskRun is executed.
The write-config step creates the Prometheus configuration file inside the PVC. Make sure this part works before starting Prometheus.
