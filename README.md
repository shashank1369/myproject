# ============================================================
# 🚀 KUBERNETES (MINIKUBE) COMPLETE COMMAND SET WITH DETAILS
# ============================================================

# -------------------------------------------
# 1) START MINIKUBE
# -------------------------------------------

# Start Minikube using Docker as the driver
minikube start --driver=docker

# Check whether Minikube and Kubernetes components are running
minikube status
# Expected: host=Running, kubelet=Running, apiserver=Running


# -------------------------------------------
# 2) BASIC KUBECTL COMMANDS
# -------------------------------------------

kubectl version
# Shows client & server version

kubectl get nodes
# Shows Kubernetes node (minikube node)

kubectl get pods
# Shows running pods in default namespace

kubectl get pods -A
# Shows ALL pods in ALL namespaces

kubectl get deployments
# Shows all deployments

kubectl get svc
# Shows all services running in the cluster


# -------------------------------------------
# 3) CREATE DEPLOYMENT
# -------------------------------------------

# Create an nginx deployment
kubectl create deployment mynginx --image=nginx

# Check pod created by this deployment
kubectl get pods

# Detailed information about pod (Events, IP, Node)
kubectl describe pods


# -------------------------------------------
# 4) EXPOSE DEPLOYMENT AS SERVICE
# -------------------------------------------

# Expose the deployment on port 80 as a NodePort service
kubectl expose deployment mynginx --type=NodePort --port=80

# Check service details including assigned NodePort
kubectl get svc

# Example output:
# mynginx  NodePort  80:32XXX/TCP
# 32XXX is the port Minikube assigned


# -------------------------------------------
# 5) SCALE DEPLOYMENT
# -------------------------------------------

# Scale number of pods to 4
kubectl scale deployment mynginx --replicas=4

# Verify that 4 pods are created
kubectl get pods -o wide


# -------------------------------------------
# 6) ACCESS APPLICATION
# -------------------------------------------

# OPTION A — PORT FORWARDING
# Forward localhost:8080 to nginx service port 80
kubectl port-forward service/mynginx 8080:80

# Now open browser:
# http://localhost:8080/
# You should see the default nginx welcome page.


# OPTION B — MINIKUBE SERVICE URL
minikube service mynginx --url

# This prints a URL, example:
# http://192.168.49.2:32241
#
# Open this URL in browser to view nginx page.


# -------------------------------------------
# 7) UPDATE DEPLOYMENT IMAGE
# -------------------------------------------

kubectl set image deployment/mynginx nginx=nginx:latest
# Updates container image inside all pods


# -------------------------------------------
# 8) DELETE RESOURCES (CLEANUP)
# -------------------------------------------

kubectl delete deployment mynginx
kubectl delete service mynginx


# -------------------------------------------
# 9) OPEN KUBERNETES DASHBOARD
# -------------------------------------------

# Opens graphical UI in browser
minikube dashboard


# -------------------------------------------
# 10) STOP / DELETE CLUSTER
# -------------------------------------------

minikube stop
# Stops cluster (does NOT delete it)

minikube delete
# Deletes full cluster




# ============================================================
# 🖥️ NAGIOS MONITORING (DOCKER) — FULL COMMAND SET WITH DETAILS
# ============================================================

# -------------------------------------------
# 1) PULL NAGIOS IMAGE
# -------------------------------------------

docker pull jasonrivers/nagios
# Downloads the official Nagios Docker image from Docker Hub


# -------------------------------------------
# 2) RUN NAGIOS CONTAINER
# -------------------------------------------

docker run -d -p 9090:80 --name nagios jasonrivers/nagios
# -d = run in background
# -p 9090:80 = access UI via browser on port 9090
# --name nagios = container name


# -------------------------------------------
# 3) VERIFY CONTAINER IS RUNNING
# -------------------------------------------

docker ps
# Should show container named "nagios" running on port 9090


# -------------------------------------------
# 4) OPEN THE NAGIOS WEB UI
# -------------------------------------------

# Open browser and enter:
# http://localhost:9090

# LOGIN:
# username: nagiosadmin
# password: nagios

# Inside UI you can check:
# ✔ Host Status
# ✔ Service Status
# ✔ CPU / RAM / Disk checks
# ✔ Alerts and Notifications


# -------------------------------------------
# 5) VIEW NAGIOS LOGS
# -------------------------------------------

docker logs nagios
# Shows logs of container

docker logs -f nagios
# Follow logs live (real-time)


# -------------------------------------------
# 6) RESTART NAGIOS
# -------------------------------------------

docker restart nagios
# Restarts container (useful if settings updated)


# -------------------------------------------
# 7) STOP & REMOVE NAGIOS
# -------------------------------------------

docker stop nagios
# Stops container

docker rm nagios
# Removes container


# -------------------------------------------
# 8) REMOVE NAGIOS IMAGE (OPTIONAL)
# -------------------------------------------

docker images
# Show all images

docker rmi jasonrivers/nagios
# Delete Nagios image from system
