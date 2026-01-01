# Day XX: [Scenario Title]

**Category:** [Category Name]
**Difficulty:** [Beginner/Intermediate/Advanced]

---

## 🎯 Challenge Description

[Brief description of the scenario. What are we trying to achieve?]

**Objectives:**
1. [Objective 1]
2. [Objective 2]
3. [Objective 3]

---

## 🛠️ Prerequisites

- Kubernetes Cluster (Minikube, Kind, or Cloud)
- `kubectl` configured
- [Any specific tools like Helm, etc.]

---

## 💻 Solution

### Step 1: [Step Name]

[Explanation of the step]

```bash
# Command to execute
kubectl run ...
```

### Step 2: [Step Name]

[Explanation]

```yaml
# YAML manifest if needed
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: nginx
    image: nginx
```

### Verification

How to verify the solution works?

```bash
kubectl get pods
kubectl exec ...
```

---

## 🎥 Video Walkthrough

[![Video Title](https://img.youtube.com/vi/VIDEO_ID/0.jpg)](https://www.youtube.com/watch?v=VIDEO_ID)

*(Click the image to watch the video)*

---

## 📚 References

- [Kubernetes Documentation](https://kubernetes.io/docs/home/)
- [Relevant Link 1]
