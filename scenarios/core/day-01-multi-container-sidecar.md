# Day 01: Multi-Container Pod (Sidecar Pattern)

**Category:** Core Concepts
**Difficulty:** Intermediate

---

## 🎯 Challenge Description

In Kubernetes, a **Pod** is the smallest deployable unit, but it doesn't have to be limited to a single container. The **Sidecar Pattern** is a fundamental architectural pattern where a secondary container (the sidecar) sits alongside the main application container to enhance or extend its functionality without changing the application code.

**Your Task:**
You need to implement a multi-container Pod that demonstrates data sharing between two containers running on the same node and lifecycle.

You will create a Pod named `web-content-generator` that contains:
1.  **Main Container:** An `nginx` web server that serves HTML files.
2.  **Sidecar Container:** A `debian` container that acts as a content generator. It should write the current date and time to an `index.html` file every 5 seconds.
3.  **Shared Storage:** A shared Volume that both containers can access, allowing the sidecar to write data that the main container serves.

**Objectives:**
1.  Define a Pod manifest named `web-content-generator`.
2.  Create a shared volume of type `emptyDir`.
3.  Configure the **main container** (`nginx`) to mount the shared volume at `/usr/share/nginx/html`.
4.  Configure the **sidecar container** (`debian`) to mount the shared volume at `/app/data` (or any path you choose, as long as the script writes to the correct file).
5.  The sidecar must run a command that infinitely loops, writing a customized message with the timestamp to `index.html` in the shared volume every 5 seconds.
6.  Verify that you can access the generated page through the Nginx server.

---

## 🛠️ Prerequisites

- A running Kubernetes cluster (Minikube, Kind, or Cloud Provider).
- `kubectl` command-line tool configured to communicate with the cluster.
- Basic understanding of YAML syntax and Pod specifications.

---

## 💻 Solution

The primary walkthrough for this scenario is available in the video below. If you prefer a text-based guide or need to copy-paste commands, expand the section below.

<details>
<summary>Click to reveal the Step-by-Step Solution</summary>

### Step 1: Create the Manifest File
Open a terminal and create a file named `web-content-generator.yaml`. You can use nano, vi, or cat.

```bash
vi web-content-generator.yaml
```

### Step 2: Define the Pod Configuration
Paste the following YAML into the file. Pay close attention to how the `volumes` and `volumeMounts` use the same name (`shared-data`).

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-content-generator
  labels:
    app: web-gen
spec:
  # 1. Define the shared storage
  volumes:
    - name: shared-data
      emptyDir: {}

  containers:
    # 2. The Main Web Server
    - name: main-container
      image: nginx:latest
      volumeMounts:
        - name: shared-data
          mountPath: /usr/share/nginx/html # Nginx default web root

    # 3. The Sidecar Content Generator
    - name: sidecar-container
      image: debian:latest
      volumeMounts:
        - name: shared-data
          mountPath: /app/data
      command: ["/bin/sh", "-c"]
      args:
        - |
          while true; do
            echo "<html><body style='background:#f4f4f4;font-family:sans-serif;'><h1>Lab Success!</h1><p>Content updated at: $(date)</p></body></html>" > /app/data/index.html
            sleep 5
          done
```

### Step 3: Apply the Manifest
Use `kubectl` to send the configuration to the cluster:

```bash
kubectl apply -f web-content-generator.yaml
```

### Step 4: Verify Container Initialization
Since the Pod has two containers, it may take a few seconds to pull both the nginx and debian images. Check the status:

```bash
kubectl get pod web-content-generator
```

> **Note:** You should see `2/2` in the READY column.

### Step 5: Test the Internal Connection
You can verify that the Sidecar is successfully writing to the volume by "executing" into the Main container and reading the file:

```bash
kubectl exec web-content-generator -c main-container -- cat /usr/share/nginx/html/index.html
```

### Step 6: Access the Web Server

#### Option 1: Localhost (Port Forwarding)
To see the results in your browser or via curl from your host machine, use port forwarding:

```bash
kubectl port-forward web-content-generator 8080:80
```

Then, in a new terminal or browser, run:

```bash
curl http://localhost:8080
```

#### Option 2: Viewport App (NodePort)
If you are using a cloud environment with a "View Port" feature, expose the pod as a Service:

```bash
# 1. Expose the pod
kubectl expose pod web-content-generator --type=NodePort --port=80 --name=web-service-exposed

# 2. Get the NodePort
kubectl get svc web-service-exposed -o jsonpath='{.spec.ports[0].nodePort}'
```

Use the output port in your Viewport tool.

</details>

---

## 🎥 Video Walkthrough

*Coming Soon*

---

## 📚 References

- [Kubernetes Docs: Multi-Container Pods](https://kubernetes.io/docs/concepts/workloads/pods/#how-pods-manage-multiple-containers)
- [Kubernetes Docs: Communicate Between Containers in the Same Pod Using a Shared Volume](https://kubernetes.io/docs/tasks/access-application-cluster/communicate-containers-same-pod-shared-volume/)
