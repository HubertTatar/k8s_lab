"You can toggle between the questions but make sure that that you click on END EXAM before the the timer runs out.
While this test environment is valid for 60 minutes, challenge yourself and try to complete all 5 questions within 30 minutes! To pass, correctly complete at least 4 out of 5 questions.Good Luck!!!"


1. Create a Persistent Volume called log-volume. It should make use of a storage class name manual. It should use RWX as the access mode and have a size of 1Gi. The volume should use the hostPath /opt/volume/nginx
Next, create a PVC called log-claim requesting a minimum of 200Mi of storage. This PVC should bind to log-volume.
Mount this in a pod called logger at the location /var/www/nginx. This pod should use the image nginx:alpine.





2. We have deployed a new pod called secure-pod and a service called secure-service. Incoming or Outgoing connections to this pod are not working.
Troubleshoot why this is happening.
Make sure that incoming connection from the pod webapp-color are successful.
Important: Don't delete any current objects deployed.



3. Create a pod called time-check in the dvl1987 namespace. This pod should run a container called time-check that uses the busybox image.
Create a config map called time-config with the data TIME_FREQ=10 in the same namespace.
The time-check container should run the command: while true; do date; sleep $TIME_FREQ;done and write the result to the location /opt/time/time-check.log.
The path /opt/time on the pod should mount a volume that lasts the lifetime of this pod.




4. Create a new deployment called nginx-deploy, with one single container called nginx, image nginx:1.16 and 4 replicas.
The deployment should use RollingUpdate strategy with maxSurge=1, and maxUnavailable=2.
Next upgrade the deployment to version 1.17.
Finally, once all pods are updated, undo the update and go back to the previous version.

Deployment created correctly?
Was the deployment created with nginx:1.16?
Was it upgraded to 1.17?
Deployment rolled back to 1.16?


5. Create a redis deployment with the following parameters:
Name of the deployment should be redis using the redis:alpine image. It should have exactly 1 replica.
The container should request for .2 CPU. It should use the label app=redis.
It should mount exactly 2 volumes.


a. An Empty directory volume called data at path /redis-master-data.
b. A configmap volume called redis-config at path /redis-master.
c. The container should expose the port 6379.


The configmap has already been created.
Deployment created correctly?

6. We have deployed a few pods in this cluster in various namespaces. Inspect them and identify the pod which is not in a Ready state. Troubleshoot and fix the issue.
Next, add a check to restart the container on the same pod if the command ls /var/www/html/file_check fails. This check should start after a delay of 10 seconds and run every 60 seconds.

You may delete and recreate the object. Ignore the warnings from the probe.

7. Create a cronjob called dice that runs every one minute. Use the Pod template located at /root/throw-a-dice. The image throw-dice randomly returns a value between 1 and 6. The result of 6 is considered success and all others are failure.
The job should be non-parallel and complete the task once. Use a backoffLimit of 25.
If the task is not completed within 20 seconds the job should fail and pods should be terminated.
You don't have to wait for the job completion. As long as the cronjob has been created as per the requirements.

8. Create a pod called my-busybox in the dev2406 namespace using the busybox image. The container should be called secret and should sleep for 3600 seconds.
The container should mount a read-only secret volume called secret-volume at the path /etc/secret-volume. The secret being mounted has already been created for you and is called dotfile-secret.
Make sure that the pod is scheduled on controlplane and no other node in the cluster.

9. Create a single ingress resource called ingress-vh-routing. The resource should route HTTP traffic to multiple hostnames as specified below:
The service video-service should be accessible on http://watch.ecom-store.com:30093/video
The service apparels-service should be accessible on http://apparels.ecom-store.com:30093/wear
To ensure that the path is correctly rewritten for the backend service, add the following annotation to the resource:
nginx.ingress.kubernetes.io/rewrite-target: /
Here 30093 is the port used by the Ingress Controller

10. A pod called dev-pod-dind-878516 has been deployed in the default namespace. Inspect the logs for the container called log-x and redirect the warnings to /opt/dind-878516_logs.txt on the controlplane node