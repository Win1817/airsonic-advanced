# Airsonic-Advanced Deployment on Kubernetes
This guide describes the process of deploying Airsonic-Advanced in a Kubernetes cluster using Persistent Volume Claims (PVC) for storage and a NodePort service for external access.

# Prerequisites
A Kubernetes cluster (e.g., K3s) up and running.
Persistent storage available with a configured StorageClass (e.g., Longhorn).
kubectl command-line tool configured to access the cluster.
Namespace airsonic-advanced already created.

# Deployment Overview
Components:
PersistentVolumeClaims (PVCs) for configuration, music, playlists, and podcasts storage.
Deployment to run the Airsonic-Advanced application.
Service to expose the application on a NodePort.

# Steps to Deploy Airsonic-Advanced
1. Clone the Repository
Start by cloning the repository where your Kubernetes YAML files are stored. If you haven't created a repository, create one, or store the following files locally in a directory of your choice.

```bash
git clone https://github.com/Win1817/airsonic-advanced.git
cd airsonic-advanced
````

2. Apply the Persistent Volume Claims (PVCs)
Airsonic-Advanced requires four PVCs for storing configuration, music, playlists, and podcasts. These PVCs will use your preferred storage class (e.g., Longhorn).

The PVC YAMLs should be present in your cloned repository (e.g., pvc.yaml):

```bash
kubectl apply -f airsonic-pvc.yaml
````

3. Deploy Airsonic-Advanced
Next, deploy the Airsonic-Advanced application in your Kubernetes cluster using the deployment.yaml file in the cloned repository:

```bash
kubectl apply -f airsonic-deployment.yaml
````

4. Expose the Service
Finally, expose Airsonic-Advanced using a NodePort service. This will allow you to access the application externally.

```bash
kubectl apply -f airsonic-service.yaml
````

5. Access Airsonic-Advanced
Once the service is deployed, you can access Airsonic-Advanced via a web browser using the following URL:

```bash
http://<NODE_IP>:32015
````
Replace <NODE_IP> with the IP address of any node in your Kubernetes cluster.

# Conclusion
You have now deployed Airsonic-Advanced in the airsonic-advanced namespace, using persistent storage for configuration, music, playlists, and podcasts. The service is exposed on NodePort 32015 for external access.

# Adjustments
Change storageClassName in the PVCs to match your storage provider.
Modify the environment variables (PUID, PGID, TZ) to suit your needs.

# Troubleshooting
PVC Binding Issues: Ensure the storage class is correctly configured and available.
Service Access: Check that your firewall and Kubernetes network policies allow traffic to the NodePort (32015).
