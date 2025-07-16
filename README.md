1. Get the Node Token from the Master Node:
SSH into the K3s master node:


ssh -i raghav-terraform.pem ubuntu@<k3s-master-ip>
Get the node token:
sudo cat /var/lib/rancher/k3s/server/node-token
2. Install K3s on the Worker Nodes:
SSH into the worker node:

ssh -i raghav-terraform.pem ubuntu@<worker-node-ip>
Run the following to install K3s and join the worker node to the master:
curl -sfL https://get.k3s.io | K3S_URL=https://<k3s-master-ip>:6443 K3S_TOKEN=<node-token> sh -
Replace <k3s-master-ip> with the public IP of the K3s master node (from Terraform output).

Replace <node-token> with the token you retrieved from the master node.

3. Verify the Nodes:
Once the worker nodes have joined, you can verify by running:


kubectl get nodes
You should see the master node and worker nodes listed as Ready.
