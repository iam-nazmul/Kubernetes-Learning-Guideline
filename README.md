# Kubernetes শেখার গাইডলাইন: Beginner → Professional → Advanced

---

## 🟢 ধাপ ০: শুরুর আগে যা জানা দরকার (Prerequisites)

Kubernetes সরাসরি শুরু করলে কঠিন লাগবে। আগে এগুলো মোটামুটি জেনে নিন:

- **[Linux বেসিক:](#linux-বেসিক-একটি-সংক্ষিপ্ত-গাইড)** ফাইল সিস্টেম, process, permission, `systemctl`, `journalctl`, `ps`, `top`, `grep`
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

---

# Linux বেসিক: একটি সংক্ষিপ্ত গাইড

## ১. ফাইল সিস্টেম

Linux-এ সবকিছু একটা গাছের মতো কাঠামোতে সাজানো, যার শুরু `/` (root) থেকে। Windows-এর মতো `C:`, `D:` ড্রাইভ নেই।

| ডিরেক্টরি | কী থাকে |
|---|---|
| `/` | সবকিছুর মূল |
| `/home` | সাধারণ ইউজারদের ফোল্ডার (`/home/rahim`) |
| `/root` | root ইউজারের হোম |
| `/etc` | কনফিগারেশন ফাইল (`/etc/nginx/`, `/etc/passwd`) |
| `/var` | পরিবর্তনশীল ডেটা: লগ (`/var/log`), ক্যাশ, ডাটাবেস |
| `/bin`, `/usr/bin` | সাধারণ কমান্ড (`ls`, `cp`) |
| `/sbin`, `/usr/sbin` | সিস্টেম অ্যাডমিন কমান্ড |
| `/tmp` | অস্থায়ী ফাইল (রিবুটে মুছে যেতে পারে) |
| `/dev` | ডিভাইস ফাইল (`/dev/sda`) |
| `/proc` | চলমান প্রসেস ও কার্নেলের ভার্চুয়াল তথ্য |
| `/opt` | থার্ড-পার্টি সফটওয়্যার |

**দরকারি কমান্ড:**
```bash
pwd                 # এখন কোথায় আছি
ls -lah             # বিস্তারিত তালিকা (লুকানো ফাইলসহ)
cd /var/log         # ডিরেক্টরি বদলানো
cd ~                # হোমে ফেরা
mkdir -p a/b/c      # নেস্টেড ফোল্ডার তৈরি
cp -r src dst       # কপি
mv old new          # সরানো / নাম বদলানো
rm -rf folder       # মুছে ফেলা (সাবধান! ফেরত আনা যায় না)
cat file.txt        # ফাইল দেখা
less big.log        # বড় ফাইল পেজ করে দেখা
tail -f app.log     # লাইভ লগ দেখা
df -h               # ডিস্কের জায়গা
du -sh *            # কোন ফোল্ডার কত জায়গা নিচ্ছে
```

## ২. Permission (অনুমতি)

`ls -l` চালালে এমন দেখায়:
```
-rwxr-xr-- 1 rahim devs 1024 Oct 25 10:00 script.sh
```

প্রথম অংশ ভেঙে দেখি:
```
-    rwx    r-x    r--
│    │      │      └── others (বাকি সবাই): শুধু পড়তে পারে
│    │      └── group (devs): পড়া + চালানো
│    └── owner (rahim): পড়া + লেখা + চালানো
└── ধরন: - = ফাইল, d = ডিরেক্টরি, l = লিংক
```

- **r** = read (4), **w** = write (2), **x** = execute (1)
- সংখ্যায়: `rwx`=7, `r-x`=5, `r--`=4 → মোট **754**

```bash
chmod 755 script.sh      # owner সব, বাকিরা পড়া+চালানো
chmod +x script.sh       # চালানোর অনুমতি যোগ
chmod u+w,o-r file       # owner-কে write দাও, others থেকে read সরাও
chown rahim:devs file    # মালিক ও গ্রুপ বদলানো
sudo command             # root অধিকারে চালানো
```

সাধারণ মান: ফাইল `644`, স্ক্রিপ্ট/ডিরেক্টরি `755`, গোপন ফাইল (SSH key) `600`। `777` প্রায় কখনোই ব্যবহার করবেন না।

## ৩. Process (প্রসেস)

চলমান প্রতিটি প্রোগ্রাম একটি প্রসেস, যার একটি অনন্য **PID** (Process ID) আছে। প্রতিটি প্রসেসের একটি parent থাকে (PPID)।

### `ps` — প্রসেসের স্ন্যাপশট
```bash
ps aux                   # সব প্রসেস
ps aux | grep nginx      # নির্দিষ্ট প্রসেস খোঁজা
ps -ef --forest          # parent-child গাছ আকারে
```
`ps aux`-এর কলাম: `USER`, `PID`, `%CPU`, `%MEM`, `STAT` (R=চলছে, S=ঘুমন্ত, Z=zombie), `COMMAND`।

### `top` — লাইভ মনিটর
```bash
top
```
ভেতরে কী-বোর্ড শর্টকাট: `P` = CPU অনুযায়ী সাজাও, `M` = মেমরি অনুযায়ী, `k` = প্রসেস kill, `1` = প্রতিটি CPU কোর আলাদা, `q` = বের হও। উপরের **load average** তিনটি সংখ্যা ১, ৫ ও ১৫ মিনিটের গড় লোড দেখায়। আরো সুন্দর ইন্টারফেসের জন্য `htop` ইনস্টল করে নিতে পারেন।

### প্রসেস নিয়ন্ত্রণ
```bash
kill 1234          # ভদ্রভাবে বন্ধ করতে বলা (SIGTERM)
kill -9 1234       # জোর করে বন্ধ (SIGKILL), শেষ উপায়
pkill nginx        # নাম দিয়ে kill
command &          # ব্যাকগ্রাউন্ডে চালানো
jobs; fg; bg       # ব্যাকগ্রাউন্ড জব পরিচালনা
```

## ৪. `systemctl` — সার্ভিস পরিচালনা

আধুনিক Linux-এ **systemd** সার্ভিস (nginx, ssh, docker ইত্যাদি) চালায়, আর `systemctl` দিয়ে তাকে নিয়ন্ত্রণ করা হয়।

```bash
systemctl status nginx         # অবস্থা দেখা (চলছে কিনা, সাম্প্রতিক লগ)
sudo systemctl start nginx     # চালু
sudo systemctl stop nginx      # বন্ধ
sudo systemctl restart nginx   # রিস্টার্ট
sudo systemctl reload nginx    # কনফিগ রিলোড (সার্ভিস না থামিয়ে)
sudo systemctl enable nginx    # বুটের সময় স্বয়ংক্রিয়ভাবে চালু
sudo systemctl disable nginx   # বুটে চালু হবে না
systemctl list-units --type=service --state=failed   # ব্যর্থ সার্ভিসগুলো
sudo systemctl daemon-reload   # unit ফাইল বদলানোর পর
```

মনে রাখুন: `start` মানে এখনই চালু, `enable` মানে পরের বুটে চালু। দুটো একসাথে: `systemctl enable --now nginx`।

## ৫. `journalctl` — systemd-এর লগ

```bash
journalctl -u nginx            # নির্দিষ্ট সার্ভিসের লগ
journalctl -u nginx -f         # লাইভ (tail -f এর মতো)
journalctl -u nginx -n 50      # শেষ ৫০ লাইন
journalctl --since "1 hour ago"
journalctl --since today -p err   # আজকের শুধু error
journalctl -b                  # বর্তমান বুটের লগ
journalctl -b -1               # আগের বুটের লগ (ক্র্যাশ খুঁজতে কাজে লাগে)
journalctl --disk-usage        # লগ কত জায়গা নিচ্ছে
```

সাধারণ ডিবাগিং ধারা: `systemctl status X` দিয়ে দেখুন কী হচ্ছে, তারপর `journalctl -u X -n 100` দিয়ে বিস্তারিত কারণ খুঁজুন।

## ৬. `grep` — টেক্সট খোঁজা

```bash
grep "error" app.log            # লাইনে "error" আছে এমন
grep -i "error" app.log         # বড়/ছোট হাতের অক্ষর উপেক্ষা
grep -r "TODO" ./src            # ফোল্ডারে রিকার্সিভলি
grep -n "error" app.log         # লাইন নম্বরসহ
grep -v "debug" app.log         # যেগুলোতে "debug" নেই
grep -c "error" app.log         # কতগুলো ম্যাচ
grep -C 3 "Exception" app.log   # ম্যাচের আগে-পরে ৩ লাইন
grep -E "error|warn" app.log    # একাধিক প্যাটার্ন (regex)
grep -l "password" *.conf       # শুধু ফাইলের নাম
```

## সব একসাথে: Pipe (`|`)

Linux-এর আসল শক্তি হলো ছোট কমান্ড জোড়া লাগানো, যেখানে একটির আউটপুট পরেরটির ইনপুট হয়:

```bash
ps aux | grep python | grep -v grep          # python প্রসেসগুলো
journalctl -u nginx --since today | grep -i error | wc -l   # আজ কতবার error
ps aux --sort=-%mem | head -5                # সবচেয়ে বেশি মেমরি নেওয়া ৫টি
du -sh /var/log/* | sort -h | tail -5        # সবচেয়ে বড় ৫টি লগ
```

## একটা বাস্তব দৃশ্য

"ওয়েবসাইট কাজ করছে না" — কীভাবে খুঁজবেন:
```bash
systemctl status nginx                  # ১. সার্ভিস চলছে?
journalctl -u nginx -n 50 -p err        # ২. কী error দিচ্ছে?
sudo nginx -t                           # ৩. কনফিগে ভুল আছে?
df -h                                   # ৪. ডিস্ক ভরে গেছে?
top                                     # ৫. CPU/মেমরি শেষ?
sudo systemctl restart nginx            # ৬. ঠিক করে রিস্টার্ট
```

যেকোনো কমান্ড সম্পর্কে আরো জানতে `man grep` বা `grep --help` চালান। 

