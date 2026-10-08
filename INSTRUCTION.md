# Instructions for Deploying and Testing DaemonSet and CronJob

## 1. How to Apply Manifests
Run the following commands from the root directory to deploy the monitoring infrastructure:

```bash
kubectl apply -f .infrastructure/namespace.yml
kubectl apply -f .infrastructure/daemonset.yml
kubectl apply -f .infrastructure/cronjob.yml
```

---

## 2. How to Validate the Solution

### Validating DaemonSet Logs
To check if the DaemonSet is continuously sending HTTP requests to the ToDo app cluster service every 5 seconds, fetch its logs:

```bash
# Find the active DaemonSet pod name
kubectl get pods -n mateapp -l name=todoapp-pinger

# View the logs (you should see HTML/JSON output from the ToDo app)
kubectl logs -l name=todoapp-pinger -n mateapp --tail=20
```

### Validating CronJob Logs
The CronJob automatically executes a curl request every 4 minutes. To verify its successful execution and view the history:

```bash
# List executed jobs and pods triggered by the scheduler
kubectl get jobs,pods -n mateapp

# View logs of the latest completed cron job pod
kubectl logs pod/<CRONJOB_POD_NAME> -n mateapp
```
