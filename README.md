# prometheusForTekton
Steps to Implement
1.Create the PersistentVolumeClaim: Ensure you apply the PVC before running the Task:

kubectl apply -f prometheus-pvc.yaml

2.Run the Task: Execute the TaskRun to start Prometheus:

kubectl apply -f run-prometheus.yaml

3.Verify the TaskRun: Check the status of the TaskRun to see if it completed successfully:

tkn taskrun logs run-prometheus-run -f

4.Create the Service: After the TaskRun, create the service for Prometheus:

kubectl apply -f prometheus-service.yaml

5.Port-Forward to Access Prometheus: Finally, access Prometheus using:

kubectl port-forward svc/prometheus-service 9090:9090

Access Prometheus: Open your web browser and navigate to http://localhost:9090 to access the Prometheus UI.