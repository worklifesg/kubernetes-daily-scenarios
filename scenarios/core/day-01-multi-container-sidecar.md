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

> *The solution for this scenario has not been added yet. Try to solve it yourself first!*

### Step 1: Define the Pod Manifest

```yaml
# TODO: Write your YAML here
```

### Step 2: Apply and Verify

```bash
# TODO: Add commands to apply and verify
```

---

## 🎥 Video Walkthrough

*Coming Soon*

---

## 📚 References

- [Kubernetes Docs: Multi-Container Pods](https://kubernetes.io/docs/concepts/workloads/pods/#how-pods-manage-multiple-containers)
- [Kubernetes Docs: Communicate Between Containers in the Same Pod Using a Shared Volume](https://kubernetes.io/docs/tasks/access-application-cluster/communicate-containers-same-pod-shared-volume/)
