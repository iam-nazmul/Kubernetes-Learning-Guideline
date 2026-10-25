# Kubernetes শেখার গাইডলাইন: Beginner → Professional → Advanced

---

## 🟢 ধাপ ০: শুরুর আগে যা জানা দরকার (Prerequisites)

Kubernetes সরাসরি শুরু করলে কঠিন লাগবে। আগে এগুলো মোটামুটি জেনে নিন:

- **Linux বেসিক:** ফাইল সিস্টেম, process, permission, `systemctl`, `journalctl`, `ps`, `top`, `grep`
- **Networking বেসিক:** IP, DNS, port, TCP/UDP, load balancer, HTTP/HTTPS
- **Container (Docker/Podman):** image, container, Dockerfile, volume, network, registry
- **YAML:** indentation, list, map (Kubernetes-এর সব কনফিগ YAML-এ লেখা)
- **Git:** basic commands

⏱️ সময়: ২–৪ সপ্তাহ (আগে জানা না থাকলে)

---

## 🔵 লেভেল ১: Beginner (১–২ মাস)

### লক্ষ্য
Kubernetes কী, কেন দরকার, এবং একটা অ্যাপ ক্লাস্টারে চালাতে পারা।

### যা শিখবেন
1. **আর্কিটেকচার:**
   - Control Plane: `kube-apiserver`, `etcd`, `kube-scheduler`, `kube-controller-manager`
   - Worker Node: `kubelet`, `kube-proxy`, container runtime (containerd)
2. **মূল অবজেক্ট:**
   - **Pod** – সবচেয়ে ছোট ইউনিট
   - **ReplicaSet** ও **Deployment** – অ্যাপ চালানো, scale, rolling update
   - **Service** – ClusterIP, NodePort, LoadBalancer
   - **Namespace** – রিসোর্স আলাদা রাখা
   - **ConfigMap** ও **Secret** – কনফিগারেশন ও গোপন তথ্য
   - **Labels ও Selectors**
3. **kubectl কমান্ড:**
   ```bash
   kubectl get pods -A
   kubectl describe pod <name>
   kubectl logs <pod> -f
   kubectl exec -it <pod> -- sh
   kubectl apply -f app.yaml
   kubectl scale deployment web --replicas=3
   kubectl rollout undo deployment web
   ```

### লোকাল ক্লাস্টার টুল
**Minikube**, **kind**, অথবা **k3d** — যেকোনো একটা দিয়ে নিজের ল্যাপটপে প্র্যাকটিস করুন।

### হ্যান্ডস-অন প্রজেক্ট
- একটি Nginx Deployment বানিয়ে Service দিয়ে expose করুন
- একটা ছোট web app (Node/Python) Docker image বানিয়ে Kubernetes-এ ডিপ্লয় করুন
- ConfigMap দিয়ে environment variable পাস করুন

### সার্টিফিকেশন (ঐচ্ছিক)
**KCNA** (Kubernetes and Cloud Native Associate) — বেসিক ধারণা যাচাইয়ের জন্য।

---

## 🟠 লেভেল ২: Professional (৩–৬ মাস)

### লক্ষ্য
প্রোডাকশনে অ্যাপ চালানো, ট্রাবলশুট করা, এবং ক্লাস্টার ম্যানেজ করতে পারা।

### যা শিখবেন
1. **Workload আরও গভীরে:**
   - StatefulSet (database-এর জন্য), DaemonSet, Job, CronJob
   - Init container, sidecar container
   - Liveness, Readiness, Startup probe
2. **Storage:**
   - Volume, PersistentVolume (PV), PersistentVolumeClaim (PVC), StorageClass
   - Dynamic provisioning
3. **Networking:**
   - CNI (Calico, Cilium, Flannel)
   - CoreDNS, Service discovery
   - Ingress ও **Gateway API** (নতুন প্রজেক্টে Gateway API শেখা ভালো — এটাই ভবিষ্যৎ স্ট্যান্ডার্ড)
   - NetworkPolicy
4. **রিসোর্স ম্যানেজমেন্ট:**
   - Requests ও Limits, ResourceQuota, LimitRange
   - HPA (Horizontal Pod Autoscaler), VPA
   - Taints, Tolerations, Node Affinity, Pod Affinity/Anti-affinity
5. **Security বেসিক:**
   - RBAC (Role, ClusterRole, RoleBinding), ServiceAccount
   - Pod Security Standards / SecurityContext
6. **প্যাকেজিং ও ডিপ্লয়মেন্ট:**
   - **Helm** (চার্ট লেখা ও ব্যবহার), **Kustomize**
7. **Observability:**
   - Prometheus + Grafana (মেট্রিক্স)
   - Loki বা EFK stack (লগ)
8. **ক্লাস্টার অপারেশন:**
   - `kubeadm` দিয়ে ক্লাস্টার বানানো
   - ক্লাস্টার আপগ্রেড, etcd backup ও restore
9. **ম্যানেজড Kubernetes:** EKS (AWS), GKE (Google), AKS (Azure) — অন্তত একটায় হাতেকলমে কাজ

### ট্রাবলশুটিং দক্ষতা (খুব গুরুত্বপূর্ণ)
`CrashLoopBackOff`, `ImagePullBackOff`, `Pending` pod, OOMKilled, DNS সমস্যা — এগুলো কীভাবে ধরবেন:
```bash
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl describe node <node>
kubectl top pods
```

### হ্যান্ডস-অন প্রজেক্ট
- ৩-টিয়ার অ্যাপ (Frontend + Backend + PostgreSQL StatefulSet) ডিপ্লয়
- Helm চার্ট বানিয়ে dev/staging/prod আলাদা values দিয়ে ডিপ্লয়
- Prometheus + Grafana দিয়ে ড্যাশবোর্ড ও অ্যালার্ট
- `kubeadm` দিয়ে ৩-নোড ক্লাস্টার (VM-এ) বানানো

### সার্টিফিকেশন
- **CKAD** – ডেভেলপারদের জন্য
- **CKA** – অ্যাডমিন/DevOps-এর জন্য (সবচেয়ে বেশি চাহিদা)

---

## 🔴 লেভেল ৩: Professional থেকে Advanced (৬–১২+ মাস)

### লক্ষ্য
বড় স্কেলের প্ল্যাটফর্ম ডিজাইন, সিকিউরিটি, অটোমেশন এবং Kubernetes এক্সটেন্ড করা।

### যা শিখবেন
1. **GitOps:**
   - **Argo CD** বা **Flux** দিয়ে Git-কে single source of truth বানানো
   - Progressive delivery: Argo Rollouts / Flagger (Canary, Blue-Green)
2. **Advanced Security:**
   - Policy engine: **Kyverno** বা **OPA Gatekeeper**
   - Runtime security: **Falco**
   - Image scanning ও signing: Trivy, Cosign (Sigstore)
   - Secrets management: External Secrets Operator, HashiCorp Vault
   - Supply chain security, audit logging
3. **Service Mesh:**
   - **Istio**, **Linkerd** বা **Cilium Service Mesh** — mTLS, traffic splitting, observability
4. **Kubernetes এক্সটেন্ড করা:**
   - CRD (Custom Resource Definition)
   - **Operator** লেখা (Go + Kubebuilder / Operator SDK)
   - Admission Webhook
5. **স্কেলিং ও কস্ট অপটিমাইজেশন:**
   - Cluster Autoscaler, **Karpenter**
   - **KEDA** (event-driven autoscaling)
   - FinOps টুল: Kubecost / OpenCost
6. **Multi-cluster ও Platform Engineering:**
   - Multi-cluster management, disaster recovery (**Velero**)
   - Infrastructure as Code: Terraform / Crossplane / Cluster API
   - Internal Developer Platform (Backstage)
7. **Advanced Observability:**
   - **OpenTelemetry**, distributed tracing (Jaeger/Tempo)
   - SLO/SLI ভিত্তিক অ্যালার্টিং
8. **ইন্টারনাল জ্ঞান:**
   - Scheduler কীভাবে সিদ্ধান্ত নেয়, etcd performance, API server tuning
   - eBPF ভিত্তিক networking (Cilium)
9. **AI/ML ওয়ার্কলোড (ট্রেন্ডিং):**
   - GPU scheduling, Kubeflow, KServe

### হ্যান্ডস-অন প্রজেক্ট
- Argo CD দিয়ে পুরো GitOps পাইপলাইন (CI → image build → scan → sign → deploy)
- একটা নিজস্ব Operator লিখুন (যেমন: CRD দিয়ে auto database backup)
- Kyverno দিয়ে পলিসি: "privileged container নিষেধ", "শুধু signed image চলবে"
- Velero দিয়ে এক ক্লাস্টার থেকে আরেক ক্লাস্টারে restore প্র্যাকটিস

### সার্টিফিকেশন
- **CKS** (Certified Kubernetes Security Specialist)
- **Kubestronaut** — KCNA, KCSA, CKA, CKAD, CKS সবগুলো পাস করলে এই টাইটেল পাওয়া যায়

---

## 📚 শেখার রিসোর্স

- **অফিসিয়াল ডকুমেন্টেশন:** kubernetes.io/docs (সবচেয়ে নির্ভরযোগ্য, পরীক্ষাতেও ব্যবহার করা যায়)
- **প্র্যাকটিস:** Killercoda (ফ্রি ব্রাউজার ল্যাব), killer.sh (CKA/CKAD/CKS মক টেস্ট)
- **বই:** *Kubernetes Up & Running*, *Kubernetes Patterns*, *Production Kubernetes*
- **হার্ড মোড শেখা:** Kelsey Hightower-এর *Kubernetes The Hard Way* (GitHub) — ভেতরের সবকিছু বুঝতে
- **কমিউনিটি:** CNCF Slack, Kubernetes Slack, KubeCon টক (YouTube-এ ফ্রি)

---

## 💡 কিছু পরামর্শ

1. **পড়ার চেয়ে হাতেকলমে বেশি করুন** — প্রতিটি টপিকের পর নিজে YAML লিখে চালান।
2. **জিনিস ভাঙুন, তারপর ঠিক করুন** — ইচ্ছা করে pod crash করান, node বন্ধ করুন, তারপর ট্রাবলশুট করুন।
3. **একসাথে সব টুল শিখতে যাবেন না** — CNCF ল্যান্ডস্কেপ বিশাল; আগে core Kubernetes মজবুত করুন।
4. **GitHub-এ প্রজেক্ট রাখুন** — চাকরির ইন্টারভিউতে এটা সার্টিফিকেটের মতোই কাজে দেয়।
5. **Kubernetes রিলিজ নোট ফলো করুন** — প্রতি বছর প্রায় ৩টা নতুন ভার্সন আসে, অনেক কিছু deprecated হয়।

---

## Optional: [Kubernetes শেখার গাইড ও সাপ্তাহিক স্টাডি প্ল্যান.pdf](<Kubernetes শেখার গাইড ও সাপ্তাহিক স্টাডি প্ল্যান.pdf>)