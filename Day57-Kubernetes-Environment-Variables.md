# ☸️ Day 57 – Kubernetes Environment Variables

## 📌 Scenario

The Nautilus DevOps team needed to create a Kubernetes Pod that uses environment variables to generate a greeting message.

The Pod was configured with three environment variables and a shell command that reads those variables and prints the final message.

---

## 🎯 Objectives

- Create a Pod named `print-envars-greeting`
- Use the `bash:latest` image
- Configure the container as `print-env-container`
- Create three environment variables
- Execute the required shell command
- Set `restartPolicy` to `Never`
- Verify the output using `kubectl logs`

---

## 🛠️ Tasks Performed

### ✅ 1. Create the Pod YAML

Created:

```bash
vi print-envars-greeting.yaml
```

Configuration:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: print-envars-greeting

spec:
  restartPolicy: Never

  containers:
    - name: print-env-container
      image: bash:latest

      env:
        - name: GREETING
          value: "Welcome to"

        - name: COMPANY
          value: "DevOps"

        - name: GROUP
          value: "Group"

      command: ["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']
```

---

## 🌱 Environment Variables

The following environment variables were configured:

| Variable | Value |
|---|---|
| `GREETING` | `Welcome to` |
| `COMPANY` | `DevOps` |
| `GROUP` | `Group` |

The command reads these variables:

```bash
echo "$(GREETING) $(COMPANY) $(GROUP)"
```

---

## 🚀 Create the Pod

```bash
kubectl apply -f print-envars-greeting.yaml
```

Expected output:

```text
pod/print-envars-greeting created
```

---

## 🔍 Verify Pod

```bash
kubectl get pod print-envars-greeting
```

Because the command executes once and finishes, the Pod should reach:

```text
Completed
```

This is expected because:

```text
restartPolicy: Never
```

prevents Kubernetes from restarting the completed container.

---

## 📋 Check Application Output

Used:

```bash
kubectl logs -f print-envars-greeting
```

Output:

```text
Welcome to DevOps Group
```

---

## 🧠 Key Learnings

- Kubernetes Pods can receive environment variables using the `env` field.
- Environment variables can be accessed by shell commands inside containers.
- `command` overrides the default container command.
- `restartPolicy: Never` is useful for one-time jobs or commands that should execute only once.
- A Pod with `restartPolicy: Never` can successfully reach `Completed`.
- `kubectl logs` can be used to inspect container output.

---

## 🎤 Interview Questions

### Q1. How do you define environment variables in Kubernetes?

Using the `env` field inside a container specification:

```yaml
env:
  - name: GREETING
    value: "Welcome to"
```

### Q2. Why was `restartPolicy: Never` used?

The command only needs to execute once. After printing the message, the container exits successfully, so Kubernetes should not restart it.

### Q3. How can you view the output of a completed Pod?

Use:

```bash
kubectl logs print-envars-greeting
```

### Q4. What happens when the command finishes?

The container exits, and because `restartPolicy` is `Never`, Kubernetes does not restart it. The Pod reaches the `Completed` state.

### Q5. How are environment variables accessed in the shell?

They can be referenced using:

```bash
$(VARIABLE_NAME)
```

For example:

```bash
$(GREETING)
```

---

## 📌 Final Configuration

```text
Pod
│
└── print-envars-greeting
       │
       └── print-env-container
              │
              ├── Image: bash:latest
              │
              ├── GREETING=Welcome to
              ├── COMPANY=DevOps
              ├── GROUP=Group
              │
              └── Command:
                  echo "$(GREETING) $(COMPANY) $(GROUP)"
```

### Expected Output

```text
Welcome to DevOps Group
```

---

## 🚀 Final Result

✅ Pod `print-envars-greeting` created

✅ Container `print-env-container` configured

✅ `bash:latest` image used

✅ Three environment variables configured

✅ Exact required command used

✅ `restartPolicy: Never` configured

✅ Output verified successfully

# 🎉 Day 57 Completed Successfully! 🚀
