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

---

# নেটওয়ার্কিং বেসিক

পুরো ব্যাপারটা একটা **চিঠি পাঠানোর** মতো ভাবা যায়। কাকে পাঠাবেন (IP), তার ঠিকানা খুঁজে বের করা (DNS), বাড়ির কোন রুমে দেবেন (Port), কীভাবে পাঠাবেন (TCP/UDP), ভিড় সামলানো (Load Balancer), আর চিঠির ভাষা ও খাম (HTTP/HTTPS)।

---

## 1. IP Address — কম্পিউটারের ঠিকানা

নেটওয়ার্কে প্রতিটা ডিভাইসের একটা ইউনিক নম্বর থাকে, এটাই IP।

- **IPv4:** `192.168.1.10`। এতে চারটা অংশ থাকে, প্রতিটা 0–255 এর মধ্যে। মোট প্রায় ৪৩০ কোটি ঠিকানা হয়, যা এখন প্রায় শেষ।
- **IPv6:** `2001:0db8:85a3::8a2e:0370:7334`। এতে ঠিকানার সংখ্যা কার্যত অসীম।
- **Private IP** (`192.168.x.x`, `10.x.x.x`): শুধু আপনার বাসা বা অফিসের লোকাল নেটওয়ার্কের ভেতরে ব্যবহার হয়।
- **Public IP:** ইন্টারনেটে আপনার রাউটারের আসল ঠিকানা। ভেতরের সব ডিভাইস **NAT**-এর মাধ্যমে এই একটা public IP শেয়ার করে।

## 2. DNS — ইন্টারনেটের ফোনবুক

মানুষ `google.com` মনে রাখে, কিন্তু কম্পিউটারের দরকার IP। DNS নামকে IP-তে রূপান্তর করে।

**ধাপগুলো:**
1. আপনি ব্রাউজারে `example.com` লিখলেন।
2. ব্রাউজার আর OS প্রথমে নিজেদের **cache** চেক করে।
3. cache-এ না পেলে প্রশ্নটা যায় **Resolver**-এর কাছে (ISP-এর, বা `8.8.8.8`, `1.1.1.1`)।
4. Resolver পর্যায়ক্রমে জিজ্ঞেস করে: Root server → `.com` server → `example.com`-এর authoritative server।
5. উত্তর আসে: `93.184.216.34`।

**কমন রেকর্ড টাইপ:**
- `A`: নাম থেকে IPv4
- `AAAA`: নাম থেকে IPv6
- `CNAME`: এক নামকে আরেক নামের alias বানায়
- `MX`: ইমেইল সার্ভার
- `TXT`: ভেরিফিকেশন ইত্যাদি

**TTL** ঠিক করে একটা উত্তর কতক্ষণ cache-এ থাকবে।

## 3. Port — বাড়ির রুম নম্বর

IP দিয়ে কম্পিউটার পর্যন্ত পৌঁছানো যায়। কিন্তু ওই কম্পিউটারে একসাথে অনেক প্রোগ্রাম চলে, তাই কোন প্রোগ্রামের কাছে ডেটা যাবে সেটা বলে দেয় **port** (০–৬৫৫৩৫)।

| Port | সার্ভিস |
|---|---|
| 22 | SSH |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 3306 / 5432 | MySQL / PostgreSQL |
| 6379 | Redis |

`IP:Port` মিলে একটা নির্দিষ্ট গন্তব্য হয়, যেমন `93.184.216.34:443`। এই জোড়াকে **socket** বলে।

## 4. TCP vs UDP — কীভাবে পাঠাবেন

| | **TCP** | **UDP** |
|---|---|---|
| কানেকশন | আগে কানেকশন তৈরি করে (3-way handshake: SYN → SYN-ACK → ACK) | কানেকশন ছাড়াই সরাসরি পাঠায় |
| নির্ভরযোগ্যতা | ডেটা হারালে আবার পাঠায়, সঠিক ক্রমে পৌঁছায় | হারালে হারাল, ক্রমের গ্যারান্টি নেই |
| গতি | তুলনামূলক ধীর | দ্রুত, overhead কম |
| উদাহরণ | ওয়েব, ইমেইল, ফাইল ট্রান্সফার, ডেটাবেস | ভিডিও কল, অনলাইন গেম, DNS, লাইভ স্ট্রিম |

TCP হলো **রেজিস্টার্ড ডাক**: প্রাপ্তি নিশ্চিত করা হয়। UDP হলো **লিফলেট ছুড়ে দেওয়া**: দ্রুত, কিন্তু কোনো গ্যারান্টি নেই। ভিডিও কলে একটা ফ্রেম মিস হলে আবার পাঠানোর চেয়ে সামনে এগিয়ে যাওয়াই ভালো, তাই সেখানে UDP ব্যবহার হয়।

> 💡 HTTP/3 চলে **QUIC**-এর উপর। QUIC হলো UDP-এর উপর বানানো একটা প্রোটোকল, যা TCP-এর মতো নির্ভরযোগ্যতা দেয় কিন্তু দ্রুত।

## 5. Load Balancer — ভিড় সামলানোর ম্যানেজার

একটা সার্ভার লাখো ইউজার সামলাতে পারে না। তাই একাধিক সার্ভার রাখা হয়, আর সামনে বসে **Load Balancer**। সে রিকোয়েস্টগুলো সার্ভারগুলোর মধ্যে ভাগ করে দেয়।

```
              ┌──→ Server 1
User → [LB] ──┼──→ Server 2
              └──→ Server 3
```

**কেন দরকার:**
- **Scalability:** নতুন সার্ভার যোগ করলেই ক্ষমতা বাড়ে।
- **High availability:** কোনো সার্ভার নষ্ট হলে **health check** দেখে LB তাকে বাদ দেয়।

**অ্যালগরিদম:**
- **Round Robin:** পালা করে একেকটা সার্ভারে পাঠায়।
- **Least Connections:** যার হাতে সবচেয়ে কম কাজ, তাকে দেয়।
- **IP Hash:** একই ইউজারকে সবসময় একই সার্ভারে পাঠায় (sticky session)।

**লেয়ার অনুযায়ী দুই ধরন:**
- **L4 (TCP/UDP লেভেল):** শুধু IP আর port দেখে সিদ্ধান্ত নেয়। খুব দ্রুত।
- **L7 (HTTP লেভেল):** URL, header, cookie দেখে রাউট করতে পারে। যেমন `/api` এক সার্ভারে, `/images` আরেক সার্ভারে।

**উদাহরণ:** Nginx, HAProxy, AWS ALB/NLB, Cloudflare।

## 6. HTTP / HTTPS — ওয়েবের ভাষা

**HTTP** হলো ব্রাউজার আর সার্ভারের কথা বলার নিয়ম। এটা request–response ভিত্তিক।

```
GET /users/42 HTTP/1.1
Host: example.com
```

```
HTTP/1.1 200 OK
Content-Type: application/json

{"id": 42, "name": "Rahim"}
```

**Method:**
- `GET`: ডেটা পড়া
- `POST`: নতুন তৈরি করা
- `PUT`/`PATCH`: আপডেট করা
- `DELETE`: মুছে ফেলা

**Status code:**
- `2xx`: সফল (200 OK, 201 Created)
- `3xx`: redirect (301, 302)
- `4xx`: ক্লায়েন্টের ভুল (400, 401, 403, 404)
- `5xx`: সার্ভারের ভুল (500, 502, 503)

HTTP **stateless**: প্রতিটা রিকোয়েস্ট আলাদা, সার্ভার আগের রিকোয়েস্ট মনে রাখে না। তাই লগইন অবস্থা ধরে রাখতে cookie, session বা token ব্যবহার হয়।

**HTTPS = HTTP + TLS এনক্রিপশন**

সাধারণ HTTP-তে সব ডেটা খোলা চিঠির মতো যায়। পথে যে কেউ (যেমন পাবলিক Wi-Fi-তে) পড়ে ফেলতে পারে। HTTPS-এ:
1. **TLS handshake:** সার্ভার তার **certificate** দেখায়, যেটা একটা বিশ্বস্ত CA (যেমন Let's Encrypt) সাইন করেছে। এতে প্রমাণ হয় সার্ভারটা আসল।
2. দুই পক্ষ মিলে একটা গোপন **session key** ঠিক করে।
3. এরপর সব ডেটা ওই key দিয়ে এনক্রিপ্টেড অবস্থায় যায়।

ফলে তিনটা জিনিস পাওয়া যায়: **গোপনীয়তা**, **ডেটা অক্ষত থাকা**, আর **সার্ভারের পরিচয় যাচাই**। HTTPS-এর ডিফল্ট port 443।

---

## সব একসাথে: আপনি `https://example.com` খুললে কী হয়

1. **DNS** থেকে `example.com`-এর **IP** পাওয়া যায়।
2. ব্রাউজার ওই IP-এর **port 443**-এ **TCP** কানেকশন খোলে (3-way handshake)।
3. **TLS handshake** হয়ে এনক্রিপ্টেড চ্যানেল তৈরি হয়।
4. রিকোয়েস্ট পৌঁছায় **Load Balancer**-এ, সে একটা সুস্থ সার্ভারে পাঠিয়ে দেয়।
5. সার্ভার **HTTP response** পাঠায় (`200 OK` + HTML)।
6. ব্রাউজার পেজ রেন্ডার করে।


---

# পরের ধাপ: OSI/TCP-IP, Subnet/CIDR, CDN, Reverse Proxy

---

## 1. OSI ও TCP/IP মডেল — নেটওয়ার্কের স্তর

একটা ডেটা পাঠাতে অনেক কাজ লাগে। সব কাজ একসাথে না করে **স্তরে (layer)** ভাগ করা হয়। প্রতিটা স্তর শুধু নিজের কাজ করে, আর উপর-নিচের স্তরের সাথে কথা বলে।

**OSI** একটা ধারণাগত (theoretical) মডেল, এতে ৭টা স্তর। **TCP/IP** হলো ইন্টারনেটে বাস্তবে যেটা চলে, এতে ৪টা স্তর।

| # | OSI Layer | কাজ | উদাহরণ | TCP/IP |
|---|---|---|---|---|
| 7 | Application | ইউজারের অ্যাপের প্রোটোকল | HTTP, DNS, SMTP, SSH | **Application** |
| 6 | Presentation | ডেটার ফরম্যাট, এনক্রিপশন | TLS, JSON, JPEG | ↑ |
| 5 | Session | কানেকশন সেশন চালানো | — | ↑ |
| 4 | Transport | প্রোগ্রাম থেকে প্রোগ্রাম ডেলিভারি, port | **TCP, UDP** | **Transport** |
| 3 | Network | এক নেটওয়ার্ক থেকে আরেক নেটওয়ার্কে রাউটিং | **IP**, ICMP (ping) | **Internet** |
| 2 | Data Link | একই লোকাল নেটওয়ার্কে ডিভাইস থেকে ডিভাইসে | Ethernet, Wi-Fi, **MAC address** | **Link** |
| 1 | Physical | বিট পাঠানো: তার, সিগন্যাল, আলো | Cable, fiber, radio | ↑ |

মনে রাখার কৌশল (৭ থেকে ১): **"All People Seem To Need Data Processing"**

**Encapsulation:** ডেটা নিচের দিকে যাওয়ার সময় প্রতিটা স্তর নিজের **header** যোগ করে, যেন খামের ভেতরে খাম।

```
[ Ethernet | IP | TCP | HTTP ডেটা ]
   L2        L3   L4     L7
```

প্রাপকের দিকে উল্টোটা ঘটে। প্রতিটা স্তর নিজের header খুলে বাকিটা উপরের স্তরে পাঠায়।

**বাস্তবে কেন কাজে লাগে:** প্রকৌশলীরা প্রায়ই "L4 load balancer", "L7 firewall", "এটা L3 সমস্যা" বলেন। এর মানে কোন স্তরে কাজ বা সমস্যা হচ্ছে।

- `ping` কাজ না করলে সমস্যা সম্ভবত **L3** বা তার নিচে।
- `ping` কাজ করে কিন্তু ওয়েবসাইট খোলে না, তাহলে **L4** (port বন্ধ?) বা **L7** (অ্যাপ ক্র্যাশ?) দেখতে হবে।

---

## 2. Subnet ও CIDR — নেটওয়ার্ককে ভাগ করা

একটা IPv4 ঠিকানা আসলে **৩২ বিটের** একটা সংখ্যা। এর দুটো অংশ:
- **Network অংশ:** কোন এলাকা (যেমন রাস্তার নাম)
- **Host অংশ:** ওই এলাকায় কোন ডিভাইস (যেমন বাড়ির নম্বর)

কতটুকু Network আর কতটুকু Host, সেটা বলে দেয় **CIDR notation**: `/` এর পরের সংখ্যা।

```
192.168.1.0/24
```

এখানে `/24` মানে প্রথম ২৪ বিট network, বাকি ৮ বিট host। তাই host-এর জন্য `2⁸ = 256` টা ঠিকানা থাকে।

**কমন সাইজ:**

| CIDR | Subnet Mask | মোট IP | ব্যবহারযোগ্য host |
|---|---|---|---|
| `/32` | 255.255.255.255 | 1 | একটা নির্দিষ্ট IP |
| `/30` | 255.255.255.252 | 4 | 2 |
| `/28` | 255.255.255.240 | 16 | 14 |
| `/24` | 255.255.255.0 | 256 | 254 |
| `/16` | 255.255.0.0 | 65,536 | 65,534 |
| `/8` | 255.0.0.0 | ~১.৬৭ কোটি | — |
| `/0` | 0.0.0.0 | সব IP | "পুরো ইন্টারনেট" |

**সূত্র:** মোট IP = `2^(32 − prefix)`

**ব্যবহারযোগ্য কেন ২টা কম:** প্রথম ঠিকানাটা **network address** (`192.168.1.0`), আর শেষটা **broadcast** (`192.168.1.255`)। এই দুটো ডিভাইসকে দেওয়া যায় না।

**উদাহরণ: `10.0.5.0/26`**
- মোট IP: `2^(32−26) = 64`
- রেঞ্জ: `10.0.5.0` থেকে `10.0.5.63`
- ব্যবহারযোগ্য host: `10.0.5.1` থেকে `10.0.5.62`

**বাস্তবে কোথায় লাগে:**
- **ক্লাউড (AWS VPC ইত্যাদি):** পুরো VPC হয়তো `10.0.0.0/16`। তার ভেতরে ভাগ করা হয়:
  - Public subnet `10.0.1.0/24`: web server, load balancer
  - Private subnet `10.0.2.0/24`: ডেটাবেস, যেখানে ইন্টারনেট থেকে সরাসরি ঢোকা যায় না
- **Firewall/Security group নিয়ম:**
  - `0.0.0.0/0` থেকে port 443 খোলা মানে সবাই HTTPS দিয়ে ঢুকতে পারবে।
  - `203.0.113.5/32` থেকে port 22 খোলা মানে শুধু এই একটা IP SSH করতে পারবে।

একটা মূল নিয়ম: একই subnet-এর ডিভাইসগুলো সরাসরি কথা বলে। ভিন্ন subnet-এ যেতে হলে **router/gateway** পার হতে হয়।

---

## 3. CDN (Content Delivery Network) — কন্টেন্ট কাছাকাছি রাখা

ধরুন আপনার সার্ভার আমেরিকায়, আর ইউজার ঢাকায়। প্রতিটা রিকোয়েস্ট হাজার হাজার কিলোমিটার যায় আর ফেরে, তাই **latency** বেশি হয়।

**CDN** সারা বিশ্বে শত শত **edge server** (PoP) রাখে, আর আপনার কন্টেন্টের কপি **cache** করে রাখে। ঢাকার ইউজার তখন কাছের (হয়তো সিঙ্গাপুর বা ঢাকারই) edge থেকে কন্টেন্ট পায়।

```
ঢাকার ইউজার ──→ [Edge: সিঙ্গাপুর] ──(cache miss হলে)──→ [Origin: আমেরিকা]
                    ↑ cache hit হলে এখান থেকেই উত্তর
```

**কীভাবে কাজ করে:**
1. ইউজার `cdn.example.com` চায়।
2. **DNS** (বা **Anycast** রাউটিং) তাকে সবচেয়ে কাছের edge-এর IP দেয়।
3. Edge-এ কন্টেন্ট থাকলে (**cache hit**) সাথে সাথে পাঠিয়ে দেয়।
4. না থাকলে (**cache miss**) origin থেকে এনে পাঠায়, আর পরের জনের জন্য রেখে দেয়।
5. কতক্ষণ রাখবে সেটা ঠিক হয় `Cache-Control` header দিয়ে, যেমন `max-age=86400` মানে এক দিন।

**কী cache হয়:** ছবি, ভিডিও, CSS, JS, ফন্ট, অর্থাৎ **static** কন্টেন্ট। ইউজারভেদে আলাদা **dynamic** ডেটা (যেমন আপনার ব্যাংক ব্যালেন্স) সাধারণত cache হয় না।

**সুবিধা:**
- দ্রুত লোড হয়, latency কম
- origin সার্ভারে চাপ অনেক কমে
- **DDoS সুরক্ষা:** বিশাল নেটওয়ার্ক আক্রমণ শুষে নেয়
- TLS-এর কাজ edge-এই হয়ে যায়

**উদাহরণ:** Cloudflare, Akamai, AWS CloudFront, Fastly

**একটা চ্যালেঞ্জ: cache invalidation।** কন্টেন্ট আপডেট করলেও পুরনো কপি edge-এ থেকে যেতে পারে। সমাধান দুটো:
- **purge** করা, অর্থাৎ cache জোর করে মুছে ফেলা
- ফাইলের নামে ভার্সন রাখা, যেমন `app.v42.js`

---

## 4. Reverse Proxy — সার্ভারের দারোয়ান

প্রথমে **Proxy** কী তা বুঝি। Proxy হলো একজন মধ্যস্থতাকারী, যে আপনার হয়ে কাজ করে।

| | **Forward Proxy** | **Reverse Proxy** |
|---|---|---|
| কার পক্ষে | **ক্লায়েন্টের** পক্ষে | **সার্ভারের** পক্ষে |
| কী লুকায় | ক্লায়েন্টের পরিচয় | পেছনের সার্ভারগুলোর পরিচয় |
| উদাহরণ | অফিসের proxy, VPN | Nginx, Cloudflare, Traefik |

```
Forward:  [আপনি] → [Proxy] → ইন্টারনেট → [যেকোনো সাইট]
Reverse:  [যেকোনো ইউজার] → ইন্টারনেট → [Reverse Proxy] → [আপনার ভেতরের সার্ভার]
```

ইউজার জানেই না পেছনে কয়টা সার্ভার আছে বা সেগুলো কী। সে শুধু reverse proxy-র সাথে কথা বলে।

**Reverse Proxy কী কী কাজ করে:**
- **Load balancing:** হ্যাঁ, load balancer আসলে এক ধরনের reverse proxy।
- **SSL/TLS termination:** HTTPS ডিক্রিপ্ট এখানেই হয়, পেছনের অ্যাপ সাধারণ HTTP-তে চলতে পারে।
- **Routing:** যেমন:
  - `/api/*` → Node.js সার্ভার (port 3000)
  - `/admin/*` → Python সার্ভার (port 8000)
  - `/*` → static ফাইল
- **Caching:** ছোট আকারের CDN-এর মতো কাজ করে।
- **Compression:** gzip বা brotli দিয়ে response ছোট করে।
- **নিরাপত্তা:** rate limiting, IP block, আসল সার্ভারের IP লুকানো।

**একটা Nginx উদাহরণ:**

```nginx
server {
    listen 443 ssl;
    server_name example.com;

    location /api/ {
        proxy_pass http://localhost:3000;
    }

    location / {
        root /var/www/html;
    }
}
```

**তিনটার পার্থক্য:**
- **Reverse proxy** হলো সাধারণ ধারণা: সার্ভারের সামনে বসা মধ্যস্থতাকারী।
- **Load balancer** হলো একটা reverse proxy, যার মূল কাজ একাধিক সার্ভারে লোড ভাগ করা।
- **CDN** হলো সারা বিশ্বে ছড়ানো reverse proxy-র নেটওয়ার্ক, যার মূল কাজ caching।

---

## সব মিলিয়ে একটা বাস্তব আর্কিটেকচার

```
ইউজার (ঢাকা)
   │  DNS → কাছের edge
   ▼
[CDN Edge] ── static ফাইল cache থেকে দেয়
   │  dynamic রিকোয়েস্ট সামনে পাঠায়
   ▼
[Load Balancer / Reverse Proxy]  ← Public subnet 10.0.1.0/24
   │  TLS termination, routing
   ├──→ App Server 1 ┐
   └──→ App Server 2 ┘            ← Private subnet 10.0.2.0/24
            │
            ▼
        [Database]                ← Private subnet 10.0.3.0/24 (শুধু app server ঢুকতে পারে)
```

এখানে প্রতিটা ধাপে আগের সব ধারণা কাজ করছে: IP, DNS, port, TCP, HTTPS, subnet, CDN, reverse proxy।


---
---
---

# পরের ধাপ: NAT ও ফায়ারওয়াল, WebSocket, ডিবাগিং টুল

---

## 1. NAT (Network Address Translation) — একটা ঠিকানা, অনেক ডিভাইস

আগে বলেছি IPv4 ঠিকানা প্রায় শেষ। তাহলে আপনার বাসার ফোন, ল্যাপটপ আর টিভি সবাই ইন্টারনেট চালায় কীভাবে? উত্তর হলো **NAT**।

বাসার সব ডিভাইস পায় **private IP** (`192.168.1.x`)। রাউটারের থাকে **একটা public IP**। ডিভাইস বাইরে রিকোয়েস্ট পাঠালে রাউটার ঠিকানাটা বদলে দেয়, আর একটা **টেবিলে** লিখে রাখে কে কোন রিকোয়েস্ট পাঠিয়েছিল।

```
ল্যাপটপ 192.168.1.10:51000 ──┐
                              ├──→ [Router: 103.x.x.x] ──→ google.com:443
ফোন    192.168.1.11:51000 ──┘
```

**NAT টেবিল:**

| ভেতরের ঠিকানা | বাইরের ঠিকানা |
|---|---|
| `192.168.1.10:51000` | `103.x.x.x:40001` |
| `192.168.1.11:51000` | `103.x.x.x:40002` |

উত্তর যখন `103.x.x.x:40002`-এ ফেরে, রাউটার টেবিল দেখে বোঝে এটা ফোনের, তাই ফোনে পাঠিয়ে দেয়। port দিয়ে ডিভাইস আলাদা করার এই পদ্ধতিকে **PAT** (Port Address Translation) বা **NAT overload** বলে। বাসার রাউটারে এটাই চলে।

**NAT-এর একটা পার্শ্বপ্রতিক্রিয়া:** বাইরে থেকে কেউ নিজে থেকে **ভেতরে ঢুকতে পারে না**, কারণ টেবিলে তার কোনো এন্ট্রি নেই। রাউটার জানে না প্যাকেটটা কোন ডিভাইসে দেবে। এটা একরকম সুরক্ষা, তবে আসল ফায়ারওয়ালের বিকল্প নয়।

**বাইরে থেকে ভেতরে ঢোকানোর দরকার হলে** (যেমন বাসায় একটা গেম সার্ভার চালালে) **Port Forwarding** করতে হয়। রাউটারে নিয়ম লিখে দেন: "port 25565-এ যা আসবে, `192.168.1.10`-এ পাঠাও।"

**CGNAT:** বাংলাদেশসহ অনেক দেশে ISP-রা নিজেরাও আরেক স্তরের NAT চালায়। তখন আপনার রাউটারের "public" IP আসলে public নয় (প্রায়ই `100.64.x.x` রেঞ্জে থাকে)। এতে port forwarding কাজ করে না। সমাধান হিসেবে ISP থেকে real IP নিতে হয়, অথবা Cloudflare Tunnel, Tailscale ইত্যাদি ব্যবহার করতে হয়।

**ক্লাউডে NAT Gateway:** private subnet-এর সার্ভার (যেমন ডেটাবেস) বাইরে থেকে কেউ ছুঁতে পারবে না, কিন্তু সে নিজে আপডেট ডাউনলোড করতে বাইরে যেতে পারবে।

---

## 2. Firewall — নেটওয়ার্কের দারোয়ান

**Firewall** নিয়ম অনুযায়ী ঠিক করে কোন ট্রাফিক ঢুকবে বা বেরোবে, আর কোনটা আটকাবে।

একটা নিয়ম সাধারণত এই জিনিসগুলো দেখে:
- **উৎস (source)** IP / CIDR
- **গন্তব্য (destination)** IP
- **Port**
- **Protocol** (TCP/UDP/ICMP)
- **Action**: Allow / Deny

**উদাহরণ নিয়ম (একটা ওয়েব সার্ভারের জন্য):**

| দিক | Source | Port | Protocol | Action |
|---|---|---|---|---|
| Inbound | `0.0.0.0/0` | 443 | TCP | ✅ Allow |
| Inbound | `0.0.0.0/0` | 80 | TCP | ✅ Allow (HTTPS-এ redirect করার জন্য) |
| Inbound | `203.0.113.5/32` | 22 | TCP | ✅ Allow (শুধু আপনার অফিস থেকে SSH) |
| Inbound | `0.0.0.0/0` | সব | সব | ❌ Deny |

শেষ নিয়মটাই সবচেয়ে গুরুত্বপূর্ণ: **Default Deny**। যা স্পষ্টভাবে অনুমতি দেওয়া হয়নি, তা নিষেধ। নিয়মগুলো সাধারণত **উপর থেকে নিচে** মেলানো হয়, আর প্রথম মিলটাই কার্যকর হয়।

**Stateless vs Stateful:**
- **Stateless:** প্রতিটা প্যাকেট আলাদাভাবে বিচার করে। তাই ফেরত ট্রাফিকের জন্যও আলাদা নিয়ম লিখতে হয়। যেমন AWS Network ACL।
- **Stateful:** কানেকশন মনে রাখে। ভেতর থেকে একটা কানেকশন শুরু হলে তার উত্তর আপনাআপনি ঢুকতে দেয়। যেমন AWS Security Group, `iptables` conntrack। আধুনিক বেশিরভাগ firewall stateful।

**স্তর অনুযায়ী firewall:**
- **L3/L4 firewall:** IP আর port দেখে। দ্রুত এবং সাধারণ।
- **L7 / WAF (Web Application Firewall):** HTTP রিকোয়েস্টের ভেতরটা পড়ে, যেমন SQL injection বা XSS-এর চেষ্টা ধরে। উদাহরণ: Cloudflare WAF, AWS WAF।

**কোথায় কোথায় থাকে:**
- **Host firewall:** সার্ভারের নিজের ভেতরে। Linux-এ `iptables`/`nftables`, সহজ ইন্টারফেস `ufw`। Windows-এ Windows Defender Firewall।
- **Network firewall:** নেটওয়ার্কের প্রবেশপথে, যেমন রাউটার বা ডেডিকেটেড ডিভাইস।
- **Cloud firewall:** Security Group, NACL।

`ufw`-এর উদাহরণ:

```bash
sudo ufw default deny incoming
sudo ufw allow 443/tcp
sudo ufw allow from 203.0.113.5 to any port 22
sudo ufw enable
```

> ⚠️ রিমোট সার্ভারে firewall চালু করার **আগে** SSH (port 22) allow করতে ভুলবেন না। নইলে নিজেই নিজেকে বাইরে আটকে ফেলবেন।

---

## 3. WebSocket — দুই দিকে সারাক্ষণ খোলা লাইন

**HTTP-র সীমাবদ্ধতা:** HTTP-তে সবসময় **ক্লায়েন্ট প্রশ্ন করে, সার্ভার উত্তর দেয়**। সার্ভার নিজে থেকে কিছু পাঠাতে পারে না। তাহলে চ্যাট অ্যাপে নতুন মেসেজ এলে ক্লায়েন্ট জানবে কীভাবে?

**পুরনো সমাধানগুলো:**
- **Polling:** প্রতি ২ সেকেন্ডে জিজ্ঞেস করা, "নতুন কিছু আছে?" বেশিরভাগ সময় উত্তর "না", তাই এটা অপচয়।
- **Long polling:** রিকোয়েস্ট পাঠিয়ে অপেক্ষা করা, সার্ভার নতুন কিছু এলে তবেই উত্তর দেয়। কাজ চলে, কিন্তু জটিল।

**WebSocket** একবার কানেকশন খোলে, তারপর সেটা **খোলাই থাকে**। দুই পক্ষই যেকোনো সময় মেসেজ পাঠাতে পারে। একে **full-duplex** বলে।

```
HTTP:       Client → প্রশ্ন → Server
            Client ← উত্তর ← Server      (কানেকশন শেষ বা পরের প্রশ্নের অপেক্ষা)

WebSocket:  Client ⇄⇄⇄⇄⇄⇄⇄⇄⇄⇄ Server     (খোলা থাকে, যেকোনো দিক থেকে মেসেজ)
```

**কীভাবে শুরু হয়:** কানেকশন শুরু হয় একটা সাধারণ HTTP রিকোয়েস্ট দিয়ে, যেটা বলে "চলো WebSocket-এ উন্নীত হই":

```
GET /chat HTTP/1.1
Host: example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
```

সার্ভার রাজি হলে উত্তর দেয়:

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
```

এরপর থেকে একই TCP কানেকশনে HTTP আর নয়, ছোট ছোট WebSocket **frame** চলাচল করে।

- `ws://` হলো এনক্রিপশন ছাড়া (port 80)।
- `wss://` হলো TLS সহ (port 443)। বাস্তবে সবসময় `wss://` ব্যবহার করুন।

**ব্রাউজারে কোড:**

```javascript
const ws = new WebSocket("wss://example.com/chat");

ws.onopen    = () => ws.send("হ্যালো!");
ws.onmessage = (e) => console.log("সার্ভার বলল:", e.data);
ws.onclose   = () => console.log("কানেকশন বন্ধ");
```

**কোথায় ব্যবহার হয়:** চ্যাট, লাইভ নোটিফিকেশন, মাল্টিপ্লেয়ার গেম, শেয়ার বাজারের লাইভ দাম, Google Docs-এর মতো একসাথে এডিটিং, লাইভ ড্যাশবোর্ড।

**বিকল্প: Server-Sent Events (SSE)।** শুধু সার্ভার থেকে ক্লায়েন্টে একমুখী আপডেট লাগলে (যেমন লাইভ স্কোর, বা AI চ্যাটের উত্তর ধীরে ধীরে আসা) SSE অনেক সহজ। এটা সাধারণ HTTP-র উপরেই চলে।

**বাস্তবের চ্যালেঞ্জ:**
- **Load balancer:** কানেকশন দীর্ঘক্ষণ খোলা থাকে, তাই LB-কে WebSocket সাপোর্ট করতে হয় আর idle timeout বাড়াতে হয়। Nginx-এ `Upgrade` header ফরোয়ার্ড করতে হয়।
- **Scaling:** ইউজার A সার্ভার 1-এ আর ইউজার B সার্ভার 2-এ থাকলে, A-এর মেসেজ B-এর কাছে পৌঁছাতে মাঝে **Redis Pub/Sub** বা অন্য message broker লাগে।
- **Reconnect:** নেটওয়ার্ক কাটলে ক্লায়েন্টকে নিজে আবার কানেক্ট করার লজিক রাখতে হয়।
- **Heartbeat:** নিয়মিত ping/pong পাঠিয়ে কানেকশন সজীব রাখতে হয়, নইলে মাঝের NAT বা firewall নিষ্ক্রিয় কানেকশন কেটে দেয়।

---

## 4. ডিবাগিং টুল — সমস্যা খুঁজে বের করা

এখানেই আগের সব তত্ত্ব হাতে-কলমে কাজে আসে। টুলগুলো স্তর অনুযায়ী সাজালে বোঝা সহজ।

### `ping` — "তুমি কি বেঁচে আছ?" (L3, ICMP)

```bash
ping google.com
ping -c 4 8.8.8.8        # Linux/Mac: ৪ বার পাঠিয়ে থামবে (Windows-এ -n 4)
```

```
64 bytes from 142.250.x.x: icmp_seq=1 ttl=117 time=38.2 ms
--- 4 packets transmitted, 4 received, 0% packet loss
```

- **`time`**: round-trip সময়, অর্থাৎ latency।
- **`packet loss`**: ০% না হলে নেটওয়ার্ক অস্থির।

**ডায়াগনসিস কৌশল:**
- `ping 8.8.8.8` কাজ করে কিন্তু `ping google.com` করে না, তাহলে **DNS সমস্যা**।
- কোনোটাই কাজ না করলে ইন্টারনেট বা রাউটার সমস্যা।

> ⚠️ অনেক সার্ভার firewall দিয়ে ICMP বন্ধ রাখে। তাই ping-এ উত্তর না এলেই সার্ভার বন্ধ, এমন নয়।

### `traceroute` — "পথে কোথায় আটকাচ্ছে?" (L3)

প্যাকেট গন্তব্যে যেতে কোন কোন রাউটার (hop) পার হয়, সেটা দেখায়।

```bash
traceroute google.com     # Linux/Mac
tracert google.com        # Windows
mtr google.com            # ping + traceroute একসাথে, লাইভ (খুব কাজের)
```

```
 1  192.168.1.1     1.2 ms     ← আপনার রাউটার
 2  100.64.0.1      5.4 ms     ← ISP (দেখুন, CGNAT রেঞ্জ!)
 3  103.x.x.x       8.1 ms
 ...
 9  142.250.x.x    38.0 ms     ← গন্তব্য
```

**কীভাবে কাজ করে:** প্রতিটা প্যাকেটে **TTL** নামে একটা কাউন্টার থাকে। প্রতি রাউটারে এটা ১ করে কমে, ০ হলে রাউটার প্যাকেট ফেলে দিয়ে "সময় শেষ" জানায়। traceroute ইচ্ছা করে TTL=1, 2, 3... দিয়ে প্যাকেট পাঠায়, ফলে প্রতিটা রাউটার পর্যায়ক্রমে নিজের পরিচয় দিয়ে ফেলে।

কোনো hop-এ হঠাৎ latency লাফিয়ে বাড়লে বা সেখান থেকে `* * *` শুরু হলে সমস্যা সম্ভবত ওখানে। তবে মাঝের কিছু hop-এ `* * *` দেখা গেলেও শেষ গন্তব্যে পৌঁছালে সেটা স্বাভাবিক, ওই রাউটারগুলো শুধু উত্তর দেয় না।

### `dig` — DNS জিজ্ঞাসাবাদ (L7)

```bash
dig example.com              # A রেকর্ড
dig example.com AAAA         # IPv6
dig example.com MX           # ইমেইল সার্ভার
dig +short example.com       # শুধু IP, বাড়তি কিছু ছাড়া
dig @1.1.1.1 example.com     # নির্দিষ্ট DNS সার্ভারকে জিজ্ঞেস করা
dig +trace example.com       # root থেকে পুরো resolution চেইন দেখা
```

```
;; ANSWER SECTION:
example.com.    3600    IN    A    93.184.216.34
                 ↑ TTL (সেকেন্ড)
```

**কখন কাজে লাগে:**
- নতুন ডোমেইন সেট করেছেন কিন্তু সাইট খুলছে না: `dig` দিয়ে দেখুন রেকর্ড আসলে কী দেখাচ্ছে।
- `dig @8.8.8.8` আর `dig @1.1.1.1` আলাদা উত্তর দিলে DNS পরিবর্তন এখনো সব জায়গায় ছড়ায়নি (propagation চলছে, পুরনো TTL শেষ হওয়ার অপেক্ষা)।

Windows-এ বিকল্প হলো `nslookup example.com`।

### `curl` — HTTP হাতে-কলমে (L7)

ব্রাউজার ছাড়াই HTTP রিকোয়েস্ট পাঠায়। ডেভেলপারদের সবচেয়ে প্রিয় টুল।

```bash
curl https://example.com                 # পেজের কন্টেন্ট
curl -I https://example.com              # শুধু header (status code দেখতে)
curl -v https://example.com              # সব বিস্তারিত: DNS, TCP, TLS handshake, header
curl -L http://example.com               # redirect অনুসরণ করা

# API-তে POST
curl -X POST https://api.example.com/users \
     -H "Content-Type: application/json" \
     -d '{"name": "Rahim"}'

# সময় মাপা: কোন ধাপে দেরি হচ্ছে?
curl -o /dev/null -s -w "DNS: %{time_namelookup}s\nTCP: %{time_connect}s\nTLS: %{time_appconnect}s\nমোট: %{time_total}s\n" https://example.com
```

`-v` আউটপুটে পুরো যাত্রাটা দেখা যায়: কোন IP-তে কানেক্ট হলো, TLS certificate কার, কোন header গেল আর এল। শেষের কমান্ডটা দিয়ে বোঝা যায় দেরিটা DNS-এ, কানেকশনে, নাকি সার্ভারের প্রসেসিংয়ে।

### `netstat` / `ss` — "আমার মেশিনে কী চলছে?" (L4)

`netstat` পুরনো টুল। আধুনিক Linux-এ তার জায়গায় **`ss`** ব্যবহার হয়, যা দ্রুত। দুটোর কাজ একই।

```bash
ss -tulnp          # কোন কোন port-এ কোন প্রোগ্রাম শুনছে (listen করছে)
netstat -tulnp     # একই কাজ, পুরনো টুল দিয়ে
```

flag-গুলোর মানে: `-t` TCP, `-u` UDP, `-l` listening, `-n` নম্বর দেখাও (নাম নয়), `-p` প্রোগ্রামের নাম।

```
State   Local Address:Port   Process
LISTEN  0.0.0.0:22           sshd
LISTEN  127.0.0.1:5432       postgres
LISTEN  0.0.0.0:3000         node
```

**খেয়াল করুন, এটা খুব গুরুত্বপূর্ণ:**
- `0.0.0.0:3000` মানে সব নেটওয়ার্ক ইন্টারফেসে শুনছে, বাইরে থেকে পৌঁছানো যাবে (firewall অনুমতি দিলে)।
- `127.0.0.1:5432` মানে শুধু এই মেশিনের ভেতর থেকে পৌঁছানো যাবে।

"অ্যাপ চলছে কিন্তু বাইরে থেকে কানেক্ট হচ্ছে না" সমস্যার একটা অতি সাধারণ কারণ হলো অ্যাপটা `127.0.0.1`-এ শুনছে।

**আরো কাজের:**

```bash
ss -tn state established       # এই মুহূর্তের সক্রিয় কানেকশনগুলো
lsof -i :3000                  # port 3000 কে দখল করে রেখেছে? ("address already in use" এরর হলে)
```

### বোনাস টুল

- **`nc` (netcat):** নির্দিষ্ট port খোলা কিনা দেখতে। `nc -zv example.com 443` চালালে বোঝা যায় TCP কানেকশন হচ্ছে কিনা। ping বন্ধ থাকলেও এটা কাজ করে।
- **`ip addr`** (Windows-এ `ipconfig`): নিজের IP, subnet দেখতে।
- **`tcpdump` / Wireshark:** নেটওয়ার্কের প্রতিটা প্যাকেট ধরে দেখা। এটাই চূড়ান্ত অস্ত্র, তবে শিখতে সময় লাগে।

---

## বাস্তব সমস্যা সমাধানের ধাপ: "ওয়েবসাইট খুলছে না"

নিচ থেকে উপরে, স্তর ধরে ধরে এগোন:

| ধাপ | কমান্ড | কী যাচাই করছে | স্তর |
|---|---|---|---|
| 1 | `ping 8.8.8.8` | আমার ইন্টারনেট আছে তো? | L3 |
| 2 | `dig +short example.com` | DNS ঠিক IP দিচ্ছে তো? | L7 (DNS) |
| 3 | `ping <ওই IP>` / `traceroute` | সার্ভার পর্যন্ত পথ আছে তো? | L3 |
| 4 | `nc -zv example.com 443` | Port খোলা? Firewall আটকাচ্ছে না তো? | L4 |
| 5 | `curl -v https://example.com` | TLS ঠিক আছে? HTTP status কী? | L7 |
| 6 | সার্ভারে: `ss -tulnp` | অ্যাপ আসলে চলছে? সঠিক ইন্টারফেসে শুনছে? | L4 |

যে ধাপে প্রথম ব্যর্থ হবে, সমস্যা সেখানেই। এভাবেই OSI মডেল বাস্তবে কাজে লাগে।

---
---
---


# পরের ধাপ: IPv6, VPN ও টানেলিং, HTTP/2 ও HTTP/3

---

## 1. IPv6 — ঠিকানার অভাব চিরতরে শেষ

### কেন দরকার হলো

IPv4-এ মোট ঠিকানা মাত্র ~৪৩০ কোটি, অথচ পৃথিবীতে মানুষই ৮০০ কোটির বেশি, ডিভাইস তার কয়েকগুণ। NAT আর CGNAT দিয়ে জোড়াতালি দিয়ে চালানো হচ্ছে। **IPv6** এর স্থায়ী সমাধান।

| | IPv4 | IPv6 |
|---|---|---|
| সাইজ | ৩২ বিট | **১২৮ বিট** |
| মোট ঠিকানা | ~৪.৩ × ১০⁹ | ~৩.৪ × ১০³⁸ (কার্যত অসীম) |
| লেখার ধরন | দশমিক: `192.168.1.10` | হেক্সাডেসিমাল: `2001:db8::1` |
| NAT | প্রায় বাধ্যতামূলক | দরকার নেই |
| Broadcast | আছে | **নেই** (multicast দিয়ে কাজ হয়) |
| কনফিগারেশন | DHCP বা ম্যানুয়াল | **SLAAC** দিয়ে নিজে নিজেই, বা DHCPv6 |
| MAC খোঁজা | ARP | **NDP** (Neighbor Discovery) |

### ঠিকানা লেখার নিয়ম

পূর্ণ ঠিকানায় ৮টা গ্রুপ থাকে, প্রতিটায় ৪টা হেক্স অঙ্ক:

```
2001:0db8:0000:0000:0000:ff00:0042:8329
```

ছোট করার দুটো নিয়ম:
1. **প্রতিটা গ্রুপের শুরুর শূন্য বাদ দেওয়া যায়:** `0db8` → `db8`, `0042` → `42`
2. **পরপর শূন্যের গ্রুপগুলোকে একবার `::` দিয়ে লেখা যায়:** `0000:0000:0000` → `::`

ফলাফল:

```
2001:db8::ff00:42:8329
```

> ⚠️ `::` একটা ঠিকানায় **একবারই** ব্যবহার করা যায়। দুবার করলে বোঝা যাবে না কোথায় কয়টা শূন্য-গ্রুপ ছিল।

URL-এ IPv6 লিখতে হয় বন্ধনীর ভেতরে, কারণ `:` এর সাথে port-এর `:` গুলিয়ে যায়:

```
http://[2001:db8::1]:8080/
```

### ঠিকানার ধরন

| ধরন | রেঞ্জ | মানে | IPv4-এ সমতুল্য |
|---|---|---|---|
| **Global Unicast** | `2000::/3` | ইন্টারনেটে সরাসরি পৌঁছানো যায় | Public IP |
| **Link-Local** | `fe80::/10` | শুধু একই লোকাল লিংকে। প্রতিটা ইন্টারফেস নিজে থেকে একটা পায় | `169.254.x.x` |
| **Unique Local (ULA)** | `fc00::/7` (বাস্তবে `fd00::/8`) | প্রাইভেট নেটওয়ার্কের জন্য | `10.x`, `192.168.x` |
| **Loopback** | `::1` | নিজের মেশিন | `127.0.0.1` |
| **Multicast** | `ff00::/8` | একসাথে অনেককে পাঠানো | broadcast-এর বদলে |
| **Unspecified** | `::` | "কোনো ঠিকানা নেই" বা "সব ইন্টারফেস" | `0.0.0.0` |

একটা ইন্টারফেসে একসাথে **একাধিক IPv6 ঠিকানা** থাকা খুবই স্বাভাবিক। যেমন একটা link-local, একটা global, আর গোপনীয়তার জন্য সাময়িক (temporary) ঠিকানা।

### Subnetting: হিসাব এখানে আলাদা

IPv6-এ সাধারণ নিয়ম:
- **`/64`** হলো একটা স্ট্যান্ডার্ড subnet (যেমন একটা LAN)। সামনের ৬৪ বিট network, পেছনের ৬৪ বিট host।
- একটা subnet-এ host ঠিকানা থাকে ২⁶⁴টা, অর্থাৎ ~১৮ কুইন্টিলিয়ন। পুরো IPv4 ইন্টারনেটের চেয়ে কোটি কোটি গুণ বেশি, **একটা subnet-এই**।
- ISP একটা বাসা বা অফিসকে সাধারণত দেয় **`/56`** (২৫৬টা `/64` subnet) বা **`/48`** (৬৫,৫৩৬টা subnet)।

```
2001:db8:abcd:0012::/64
└────────┬────────┘└┬┘
   ISP দিয়েছে /48  আপনার subnet নম্বর
```

IPv4-এর মতো "একটা ঠিকানাও নষ্ট করা যাবে না" মানসিকতা এখানে দরকার নেই। বরং `/64`-এর চেয়ে ছোট subnet করলে SLAAC কাজ করে না।

### SLAAC — নিজে নিজে ঠিকানা নেওয়া

**Stateless Address Autoconfiguration:**
1. ডিভাইস নেটওয়ার্কে যোগ দিয়েই নিজের জন্য একটা link-local ঠিকানা (`fe80::...`) বানায়।
2. রাউটার নিয়মিত **Router Advertisement (RA)** পাঠিয়ে জানায়: "এই নেটওয়ার্কের prefix হলো `2001:db8:abcd:12::/64`।"
3. ডিভাইস ওই prefix-এর সাথে নিজের তৈরি ৬৪-বিট অংশ জুড়ে পূর্ণ ঠিকানা বানিয়ে নেয়।

DHCP সার্ভারের কোনো দরকার পড়ে না।

### NAT নেই, তাহলে নিরাপত্তা?

IPv6-এ প্রতিটা ডিভাইস সরাসরি পৌঁছানোর মতো একটা global ঠিকানা পায়। আগে NAT যে "আপনাআপনি সুরক্ষা" দিত, সেটা এখানে নেই।

তাই **stateful firewall অত্যন্ত জরুরি**। বাসার রাউটারগুলো সাধারণত ডিফল্টভাবে বাইরে থেকে নতুন কানেকশন আটকায়, যা NAT-এর আচরণের মতোই। সার্ভারে firewall নিয়ম লেখার সময় IPv4 আর IPv6 **দুটোর জন্যই** নিয়ম লিখতে হবে। সাধারণ একটা ভুল হলো শুধু IPv4-এর নিয়ম লেখা, আর IPv6 দিয়ে সব খোলা রেখে দেওয়া।

> 💡 IPv6-এ ICMP পুরোপুরি বন্ধ করবেন না। NDP আর Path MTU Discovery-র মতো জরুরি কাজ ICMPv6-এর উপর নির্ভর করে।

### IPv4 থেকে IPv6-এ রূপান্তর

পুরো ইন্টারনেট একদিনে বদলানো সম্ভব নয়, তাই কয়েকটা কৌশল একসাথে চলে:
- **Dual Stack:** ডিভাইস IPv4 আর IPv6 দুটোই চালায়। এটাই সবচেয়ে প্রচলিত। দুটোই থাকলে ব্রাউজার একসাথে চেষ্টা করে যেটা আগে সংযোগ দেয় সেটা নেয়। একে **Happy Eyeballs** বলে।
- **NAT64 / DNS64:** শুধু-IPv6 নেটওয়ার্ক থেকে IPv4-এর সাইটে যাওয়ার জন্য। অনেক মোবাইল অপারেটর এটা ব্যবহার করে।
- **টানেলিং (6in4 ইত্যাদি):** IPv6 প্যাকেটকে IPv4 প্যাকেটের ভেতরে মুড়ে পাঠানো। এটাই পরের অংশের বিষয়।

### হাতে-কলমে

```bash
ip -6 addr                    # নিজের IPv6 ঠিকানাগুলো (Windows: ipconfig)
ping -6 google.com            # IPv6 দিয়ে ping
dig AAAA google.com +short    # IPv6 ঠিকানা খোঁজা
curl -6 https://ifconfig.co   # IPv6 দিয়ে নিজের public ঠিকানা দেখা
```

`curl -6` ব্যর্থ হলে আপনার ISP সম্ভবত এখনো IPv6 দিচ্ছে না।

---

## 2. Tunneling ও VPN — প্যাকেটের ভেতরে প্যাকেট

### Tunneling কী

**Tunneling** মানে একটা প্যাকেটকে **আরেকটা প্যাকেটের ভেতরে মুড়ে** পাঠানো। এটা আগের পর্বের encapsulation-এরই একটা প্রয়োগ।

```
সাধারণ:   [ IP header | TCP | ডেটা ]

টানেলে:   [ বাইরের IP | UDP | টানেল header | { ভেতরের IP | TCP | ডেটা } ]
                                                └──── এনক্রিপ্টেড (VPN হলে) ────┘
```

পথের রাউটারগুলো শুধু **বাইরের** header দেখে। ভেতরে কী আছে, তা জানে না বা পড়তে পারে না।

**কেন টানেল করা হয়:**
- এমন প্রোটোকল পাঠানো যেটা পথের নেটওয়ার্ক বোঝে না (যেমন IPv4 নেটওয়ার্কের উপর দিয়ে IPv6)।
- দূরের দুটো নেটওয়ার্ককে এমনভাবে জুড়ে দেওয়া যেন তারা একই LAN।
- ভেতরের ট্রাফিক লুকানো বা এনক্রিপ্ট করা। এটাই VPN।

### VPN (Virtual Private Network)

**VPN** হলো **এনক্রিপ্টেড টানেল**। এতে পাবলিক ইন্টারনেটের উপর দিয়ে একটা প্রাইভেট নেটওয়ার্ক তৈরি হয়।

**দুই ধরনের ব্যবহার:**

**ক) Remote Access VPN:** একজন ব্যবহারকারী একটা নেটওয়ার্কে ঢোকেন।

```
[বাসার ল্যাপটপ] ══════ এনক্রিপ্টেড টানেল ══════ [অফিসের VPN গেটওয়ে] → অফিসের ভেতরের সার্ভার
       ↑ ল্যাপটপ পায় একটা অফিসের IP, যেমন 10.8.0.5
```

উদাহরণ: বাসা থেকে অফিসের ভেতরের ড্যাশবোর্ড বা ডেটাবেস ব্যবহার করা।

**খ) Site-to-Site VPN:** দুটো পুরো নেটওয়ার্ককে যুক্ত করা।

```
[ঢাকা অফিস 10.1.0.0/16] ═══ VPN ═══ [চট্টগ্রাম অফিস 10.2.0.0/16]
```

দুই অফিসের কম্পিউটার একে অপরকে সরাসরি private IP দিয়ে ব্যবহার করতে পারে। ক্লাউড VPC-কে অফিসের নেটওয়ার্কের সাথে জোড়ার জন্যও এটা খুব প্রচলিত।

> 💡 এখানে subnet পরিকল্পনা জরুরি। দুই দিকে একই রেঞ্জ (যেমন দুটোই `192.168.1.0/24`) হলে রাউটিং গুলিয়ে যায়।

**Consumer VPN** (NordVPN, Proton VPN ইত্যাদি) আসলে remote access VPN-এরই একটা রূপ। পার্থক্য হলো এখানে টানেলের অপর প্রান্তে অফিস নেই, আছে VPN কোম্পানির সার্ভার, যেখান থেকে আপনার ট্রাফিক ইন্টারনেটে বের হয়।

### Full Tunnel vs Split Tunnel

- **Full tunnel:** **সব** ট্রাফিক VPN দিয়ে যায়, এমনকি YouTube-ও। নিরাপদ, কিন্তু ধীর হতে পারে আর VPN সার্ভারে চাপ বাড়ে।
- **Split tunnel:** শুধু নির্দিষ্ট গন্তব্যের ট্রাফিক (যেমন `10.0.0.0/8`, অফিসের নেটওয়ার্ক) VPN দিয়ে যায়, বাকি সব সরাসরি ইন্টারনেটে। দ্রুত, তবে নিয়ন্ত্রণ কম।

এটা নিয়ন্ত্রিত হয় **রাউটিং টেবিল** দিয়ে। কোন CIDR-এর ট্রাফিক কোন ইন্টারফেস দিয়ে যাবে, সেটাই নির্ধারণ করে।

### VPN প্রোটোকল

| প্রোটোকল | ট্রান্সপোর্ট | বৈশিষ্ট্য |
|---|---|---|
| **WireGuard** | UDP | আধুনিক, খুব দ্রুত, কোড অল্প হওয়ায় অডিট করা সহজ, কনফিগারেশন সরল। Linux kernel-এ সরাসরি অন্তর্ভুক্ত |
| **OpenVPN** | UDP বা TCP | পুরনো, পরীক্ষিত, খুব নমনীয়। TLS ভিত্তিক। TCP 443-এ চালালে কঠোর firewall-ও প্রায়ই পার হয় |
| **IPsec (IKEv2)** | সরাসরি IP-র উপর (ESP), NAT থাকলে UDP | এন্টারপ্রাইজ আর site-to-site-এর মান। রাউটার ও ক্লাউডে বিল্ট-ইন। মোবাইলে নেটওয়ার্ক বদলালেও ভালো টেকে। কনফিগারেশন জটিল |

নতুন সেটআপের জন্য সাধারণত **WireGuard** সবচেয়ে ভালো শুরু।

**WireGuard কনফিগারেশনের নমুনা (ক্লায়েন্ট):**

```ini
[Interface]
PrivateKey = <ক্লায়েন্টের private key>
Address    = 10.8.0.2/24          # টানেলের ভেতরে ক্লায়েন্টের IP

[Peer]
PublicKey  = <সার্ভারের public key>
Endpoint   = vpn.example.com:51820  # সার্ভারের public ঠিকানা ও UDP port
AllowedIPs = 10.0.0.0/16           # split tunnel: শুধু এই রেঞ্জ টানেলে যাবে
# AllowedIPs = 0.0.0.0/0, ::/0     # full tunnel: সব ট্রাফিক
PersistentKeepalive = 25           # NAT-এর পেছনে থাকলে কানেকশন সজীব রাখে
```

এখানে আগের সব ধারণা একসাথে দেখা যাচ্ছে: CIDR (`AllowedIPs`), UDP port, NAT, heartbeat।

### Mesh VPN: Tailscale ও তার মতো

প্রচলিত VPN-এ সব ট্রাফিক একটা কেন্দ্রীয় সার্ভার দিয়ে যায় (hub-and-spoke)। **Tailscale**, ZeroTier, Netbird-এর মতো **mesh VPN**-এ প্রতিটা ডিভাইস অন্যটার সাথে **সরাসরি** কানেক্ট হয়। Tailscale ভেতরে WireGuard ব্যবহার করে।

এদের বড় সুবিধা হলো **NAT traversal**। দুটো ডিভাইস দুটোই NAT বা CGNAT-এর পেছনে থাকলেও কৌশল খাটিয়ে (UDP hole punching) সরাসরি সংযোগ বানায়। একেবারেই না পারলে মাঝে relay সার্ভার ব্যবহার করে। কোনো port forwarding লাগে না, তাই CGNAT-এ আটকে থাকা বাংলাদেশি ব্যবহারকারীদের জন্য এটা খুব কাজের।

### SSH Tunneling — ছোট কাজের জন্য দ্রুত টানেল

পুরো VPN সেটআপ না করেও SSH দিয়ে নির্দিষ্ট port টানেল করা যায়।

**Local forwarding (`-L`): দূরের সার্ভিসকে নিজের মেশিনে আনা**

```bash
ssh -L 5432:localhost:5432 user@db-server.com
```

এখন নিজের মেশিনে `localhost:5432`-এ কানেক্ট করলে আসলে কানেক্ট হবেন সার্ভারের PostgreSQL-এ। ডেটাবেসটা হয়তো শুধু `127.0.0.1`-এ শুনছে, বাইরে খোলা নয়, তবুও কাজ হবে।

**Bastion/jump host হয়ে private সার্ভারে:**

```bash
ssh -L 5432:10.0.3.15:5432 user@bastion.example.com
```

Bastion-টা public subnet-এ, ডেটাবেস private subnet-এ (`10.0.3.15`)। Bastion মাঝখান দিয়ে পৌঁছে দেয়।

**Remote forwarding (`-R`): নিজের মেশিনের সার্ভিস বাইরে দেখানো**

```bash
ssh -R 8080:localhost:3000 user@public-server.com
```

`public-server.com:8080`-এ যা আসবে, তা চলে আসবে আপনার ল্যাপটপের port 3000-এ। CGNAT-এর পেছন থেকেও কাজ করে, কারণ কানেকশনটা ভেতর থেকে বাইরে যাচ্ছে।

**Dynamic forwarding (`-D`): SOCKS proxy**

```bash
ssh -D 1080 user@server.com
```

ব্রাউজারে SOCKS proxy হিসেবে `localhost:1080` সেট করলে সব ব্রাউজিং সার্ভারের দিক দিয়ে যাবে। এটা একরকম "গরিবের VPN"।

### Reverse Tunnel সার্ভিস

লোকাল ডেভেলপমেন্ট সার্ভার বা বাসার সার্ভার ইন্টারনেটে দেখাতে চাইলে, আর port forwarding সম্ভব না হলে (CGNAT), আছে **Cloudflare Tunnel**, **ngrok** ইত্যাদি। এরা `-R`-এর মতোই কাজ করে: আপনার মেশিন থেকে বাইরের দিকে একটা কানেকশন খুলে রাখে, আর ইন্টারনেটের রিকোয়েস্ট ওই পথ দিয়ে ভেতরে আনে।

### টানেলের একটা লুকানো সমস্যা: MTU

একটা প্যাকেটের সর্বোচ্চ সাইজকে **MTU** বলে, Ethernet-এ সাধারণত ১৫০০ বাইট। টানেল নিজের header যোগ করে, যেমন WireGuard যোগ করে ~৬০–৮০ বাইট। তাই ভেতরের প্যাকেটের জন্য জায়গা কমে যায়।

ভেতরের প্যাকেট বেশি বড় হলে তা ভাঙতে (fragment) হয়, বা ফেলে দেওয়া হয়। তখন এক অদ্ভুত লক্ষণ দেখা যায়: **ছোট রিকোয়েস্ট কাজ করে, বড়গুলো আটকে যায়।** যেমন `ping` চলে, SSH লগইন হয়, কিন্তু বড় ওয়েবপেজ বা ফাইল আটকে থাকে।

সমাধান হলো টানেল ইন্টারফেসের MTU কমানো। WireGuard ডিফল্ট ১৪২০ ব্যবহার করে।

### VPN কী করে আর কী করে না

| ✅ করে | ❌ করে না |
|---|---|
| আপনার ISP বা পাবলিক Wi-Fi থেকে ট্রাফিক লুকায় | আপনাকে পুরোপুরি বেনামী করে না। VPN কোম্পানি নিজেই সব দেখতে পারে |
| গন্তব্য সাইট আপনার আসল IP দেখে না | লগইন করা অবস্থায় Google বা Facebook আপনাকে ঠিকই চেনে (cookie, অ্যাকাউন্ট) |
| প্রাইভেট নেটওয়ার্কে নিরাপদে প্রবেশ দেয় | malware বা phishing থেকে রক্ষা করে না |

> ⚠️ **DNS leak:** VPN চালু থাকলেও DNS রিকোয়েস্ট কখনো কখনো টানেলের বাইরে দিয়ে ISP-এর DNS-এ চলে যায়। ফলে আপনি কোন সাইটে যাচ্ছেন তা ISP জেনে যায়। ভালো VPN ক্লায়েন্ট DNS-ও টানেলের ভেতর দিয়ে পাঠায়।

---

## 3. HTTP/2 ও HTTP/3 — ওয়েবকে দ্রুত করা

### সমস্যা: HTTP/1.1 ধীর কেন

একটা আধুনিক ওয়েবপেজে HTML, ডজন ডজন CSS ও JS ফাইল, শত শত ছবি থাকে। HTTP/1.1-এ:

1. **এক কানেকশনে একবারে একটা রিকোয়েস্ট।** একটার উত্তর পুরো না আসা পর্যন্ত পরেরটা যেতে পারে না। "Pipelining" নামে একটা সমাধান ছিল, কিন্তু বাস্তবে প্রায় কেউ চালু করেনি।
2. তাই ব্রাউজাররা প্রতি ডোমেইনে **~৬টা সমান্তরাল TCP কানেকশন** খোলে। প্রতিটার জন্য আলাদা TCP ও TLS handshake লাগে, যা ব্যয়বহুল।
3. **Header বারবার পাঠানো।** প্রতিটা রিকোয়েস্টে একই cookie, user-agent ইত্যাদি টেক্সট আকারে আবার যায়, যা প্রায়ই কয়েক কিলোবাইট।
4. **Head-of-Line (HOL) blocking:** একটা বড় বা ধীর response সামনে থাকলে পেছনের সবাই অপেক্ষা করে।

ডেভেলপাররা তখন কৌশল খাটাতেন: সব JS একটা ফাইলে জোড়া (bundling), ছোট ছবিগুলো একটা ছবিতে মেলানো (sprite), কন্টেন্ট অনেক ডোমেইনে ছড়ানো (domain sharding)। এগুলো সব ছিল প্রোটোকলের দুর্বলতা ঢাকার চেষ্টা।

### HTTP/2: এক কানেকশনে সব

HTTP/2-এর মূল পরিবর্তনগুলো:

**ক) Binary framing:** টেক্সটের বদলে বাইনারি **frame**-এ ডেটা যায়। মেশিনের জন্য পার্স করা দ্রুত আর নির্ভুল। HTTP-র *অর্থ* একই থাকে: method, status code, header সবই আছে। শুধু তারে যাওয়ার ধরন বদলেছে। তাই আপনার অ্যাপের কোড বদলাতে হয় না।

**খ) Multiplexing: সবচেয়ে বড় পরিবর্তন।** একটা মাত্র TCP কানেকশনের ভেতরে অনেকগুলো **stream** চলে, প্রতিটা রিকোয়েস্ট-রেসপন্স একটা stream। ভিন্ন ভিন্ন stream-এর frame মিলেমিশে একসাথে যায়।

```
HTTP/1.1 (একটা কানেকশন):
  [──── style.css ────][──── app.js ────][── logo.png ──]   ← একটার পর একটা

HTTP/2 (একটা কানেকশন):
  [css][js][png][css][js][png][js][css][png]...              ← সব একসাথে, মিশিয়ে
   s1   s3  s5   s1   s3  s5   s3  s1   s5    (stream ID দিয়ে আলাদা করা)
```

এক কানেকশনেই সব হয়ে যায়, তাই handshake-এর খরচ একবারই।

**গ) HPACK header compression:** দুই পক্ষ একটা টেবিল রাখে। আগে পাঠানো header-গুলো সেখানে থাকে। পরের বার পুরো header না পাঠিয়ে শুধু টেবিলের index নম্বর পাঠানো হয়। বারবার একই cookie পাঠানোর অপচয় প্রায় শেষ।

**ঘ) Stream prioritization:** ক্লায়েন্ট জানাতে পারে কোনটা বেশি জরুরি, যেমন পেজ দেখাতে CSS আগে লাগবে, পেজের নিচের ছবি পরে।

**ঙ) Server Push (এখন বিদায় নিয়েছে):** ধারণা ছিল ক্লায়েন্ট চাওয়ার আগেই সার্ভার CSS পাঠিয়ে দেবে। বাস্তবে ঠিকমতো কাজে লাগানো কঠিন ছিল, প্রায়ই ব্রাউজারের cache-এ আগে থেকে থাকা জিনিস আবার পাঠানো হতো। Chrome এটা সরিয়ে দিয়েছে। বিকল্প হিসেবে এখন `103 Early Hints` আর `<link rel="preload">` ব্যবহার হয়।

HTTP/2 আসার পর bundling আর domain sharding-এর মতো পুরনো কৌশলের দরকার অনেক কমে গেছে। domain sharding বরং ক্ষতিকর, কারণ এতে এক কানেকশনের সুবিধা নষ্ট হয়।

### HTTP/2-এর অবশিষ্ট সমস্যা: TCP-র HOL blocking

HTTP/2 অ্যাপ্লিকেশন স্তরের HOL blocking দূর করেছে। কিন্তু নিচে আছে **TCP**, আর TCP-র একটা কঠোর নিয়ম আছে: **সব বাইট ক্রমানুসারে পৌঁছাতে হবে।**

```
TCP প্যাকেট:  [s1][s3][s5][s1 ✗ হারাল][s3][s5][s1]
                              ↑
              এটা আবার না আসা পর্যন্ত পেছনের সব আটকে থাকবে।
              s3 আর s5-এর ডেটা এসে বসে আছে, কিন্তু ব্রাউজারকে দেওয়া যাচ্ছে না।
```

TCP জানে না ভেতরে আলাদা stream আছে। তার কাছে সব একটা বাইটের স্রোত। ফলে **একটা প্যাকেট হারালে সব stream থেমে যায়।**

ভালো নেটওয়ার্কে এটা বড় সমস্যা না। কিন্তু মোবাইল বা দুর্বল Wi-Fi-তে, যেখানে প্যাকেট লস বেশি, HTTP/2 কখনো কখনো HTTP/1.1-এর ৬টা আলাদা কানেকশনের চেয়েও খারাপ করে। কারণ ওখানে একটা কানেকশন আটকালে বাকি ৫টা চলতে থাকত।

TCP বদলানো প্রায় অসম্ভব, কারণ এটা OS kernel আর পথের অসংখ্য রাউটার ও firewall-এ গাঁথা। তাই সমাধানটা হলো TCP-কেই বাদ দেওয়া।

### HTTP/3: QUIC-এর উপর, UDP দিয়ে

**HTTP/3** চলে **QUIC**-এর উপর। QUIC হলো **UDP**-এর উপর বানানো নতুন একটা ট্রান্সপোর্ট প্রোটোকল। UDP বেছে নেওয়ার কারণ হলো পথের সব রাউটার আর firewall UDP চেনে। QUIC-এর সব বুদ্ধি থাকে অ্যাপ্লিকেশনে (ব্রাউজার ও সার্ভারে), তাই kernel না বদলেই দ্রুত উন্নত করা যায়।

```
HTTP/1.1, HTTP/2               HTTP/3
┌──────────────┐              ┌──────────────┐
│  HTTP/2      │              │  HTTP/3      │
├──────────────┤              ├──────────────┤
│  TLS         │              │  QUIC        │ ← TLS 1.3 + নির্ভরযোগ্যতা +
├──────────────┤              │ (TLS ভেতরে)  │   stream + congestion control
│  TCP         │              ├──────────────┤   সব একসাথে
├──────────────┤              │  UDP         │
│  IP          │              ├──────────────┤
└──────────────┘              │  IP          │
                              └──────────────┘
```

**QUIC-এর মূল সুবিধাগুলো:**

**ক) স্বাধীন stream, তাই HOL blocking নেই।** QUIC নিজেই stream বোঝে। stream 1-এর প্যাকেট হারালে শুধু stream 1 অপেক্ষা করে, stream 3 আর 5 চলতে থাকে।

**খ) দ্রুত handshake।** QUIC-এ TLS 1.3 প্রোটোকলের **ভেতরেই** বানানো, তাই কানেকশন আর এনক্রিপশন একসাথে প্রতিষ্ঠা হয়।

| সেটআপ | ডেটা পাঠানোর আগে কত round-trip (RTT) |
|---|---|
| TCP + TLS 1.2 | **৩ RTT** (TCP ১ + TLS ২) |
| TCP + TLS 1.3 | **২ RTT** |
| QUIC (প্রথমবার) | **১ RTT** |
| QUIC (আবার আসা, 0-RTT) | **০ RTT**: প্রথম প্যাকেটেই ডেটা |

ঢাকা থেকে আমেরিকার সার্ভারে এক RTT যদি ~২৫০ ms হয়, তাহলে ৩ RTT থেকে ১ RTT-এ নামা মানে প্রতিটা নতুন কানেকশনে প্রায় আধা সেকেন্ড বাঁচে।

> ⚠️ **0-RTT-এর ঝুঁকি:** প্রথম প্যাকেটের ডেটা আক্রমণকারী রেকর্ড করে আবার পাঠাতে পারে (replay attack)। তাই 0-RTT শুধু নিরাপদ রিকোয়েস্টের জন্য, যেমন `GET`। টাকা পাঠানোর মতো `POST`-এর জন্য নয়।

**গ) Connection Migration।** TCP কানেকশন চেনা হয় চারটা জিনিস দিয়ে: উৎস IP, উৎস port, গন্তব্য IP, গন্তব্য port। ফোন Wi-Fi থেকে মোবাইল ডেটায় গেলে IP বদলে যায়, তাই সব TCP কানেকশন ভেঙে যায়।

QUIC কানেকশন চেনা হয় একটা **Connection ID** দিয়ে, যা IP-র উপর নির্ভর করে না। IP বদলালেও কানেকশন বেঁচে থাকে। ফলে বাসা থেকে রাস্তায় বের হওয়ার সময় ভিডিও কল বা ডাউনলোড না থেমে চলতে থাকে।

**ঘ) পুরোটা এনক্রিপ্টেড।** TCP-র header খোলা থাকে, পথের যে কেউ পড়তে বা বদলাতে পারে। QUIC-এর প্রায় সব header-ও এনক্রিপ্টেড। গোপনীয়তা বাড়ে, আর পথের ডিভাইসগুলো প্রোটোকলে হস্তক্ষেপ করতে পারে না। এই হস্তক্ষেপই TCP-কে "জমিয়ে" দিয়েছিল।

**ঙ) QPACK:** HPACK-এর রূপান্তর, যা stream স্বাধীন থাকার সাথে মানানসই। HPACK সব header ক্রমানুসারে আসবে ধরে নিত।

### ব্রাউজার কীভাবে জানে সার্ভার HTTP/3 পারে

কোনো সার্ভার HTTP/3 সাপোর্ট করে কিনা, ব্রাউজার আগে থেকে জানে না। তাই:
1. প্রথমবার সাধারণত HTTP/2 (TCP) দিয়ে যায়।
2. সার্ভার উত্তরে একটা header দেয়:
   ```
   alt-svc: h3=":443"; ma=86400
   ```
   অর্থাৎ "আমি UDP 443-এ HTTP/3-ও পারি, এই তথ্য এক দিন মনে রেখো।"
3. পরের রিকোয়েস্ট থেকে ব্রাউজার HTTP/3 ব্যবহার করে।

নতুন পদ্ধতিতে DNS-এর **`HTTPS` রেকর্ড** দিয়েও এটা জানানো যায়। তখন প্রথম রিকোয়েস্ট থেকেই HTTP/3 চলে।

### বাস্তবের চ্যালেঞ্জ

- **UDP ব্লক:** কিছু কর্পোরেট firewall বা পুরনো নেটওয়ার্ক UDP 443 আটকে দেয়। তখন ব্রাউজার চুপচাপ HTTP/2-এ ফিরে যায়। এজন্য HTTP/2 এখনো বাধ্যতামূলক ব্যাকআপ।
- **CPU খরচ:** QUIC চলে user space-এ, আর প্রতিটা প্যাকেট আলাদাভাবে এনক্রিপ্ট হয়। তাই TCP-র চেয়ে সার্ভারের CPU বেশি লাগে, যদিও এটা ক্রমশ উন্নত হচ্ছে।
- **ডিবাগিং কঠিন:** সব এনক্রিপ্টেড বলে Wireshark-এ ভেতরটা দেখতে বাড়তি কনফিগারেশন (TLS key log) লাগে।
- **Load balancer:** connection migration হলে IP বদলায়, তাই LB-কে IP দিয়ে নয়, Connection ID দিয়ে রাউট করতে জানতে হয়।

### তিনটার তুলনা

| | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---|---|---|---|
| ট্রান্সপোর্ট | TCP | TCP | **QUIC (UDP)** |
| ফরম্যাট | টেক্সট | বাইনারি | বাইনারি |
| এক কানেকশনে সমান্তরাল রিকোয়েস্ট | ❌ | ✅ | ✅ |
| Header compression | ❌ | HPACK | QPACK |
| HOL blocking | অ্যাপ + TCP | শুধু TCP স্তরে | **নেই** |
| Handshake (নতুন কানেকশন) | ২–৩ RTT | ২–৩ RTT | **১ RTT** (পুনরায় ০) |
| এনক্রিপশন | ঐচ্ছিক | বাস্তবে বাধ্যতামূলক (ব্রাউজাররা শুধু TLS-এ সাপোর্ট করে) | **বাধ্যতামূলক, বিল্ট-ইন** |
| নেটওয়ার্ক বদলালে | কানেকশন ভাঙে | কানেকশন ভাঙে | **টিকে থাকে** |

কোনোটাই "মৃত" নয়। ব্রাউজার আর সার্ভার পরিস্থিতি অনুযায়ী সেরাটা বেছে নেয়। আপনার সার্ভারের সামনে CDN বা Nginx-এর মতো reverse proxy থাকলে, সাধারণত সেখানেই HTTP/2 ও HTTP/3 চালু করা হয়। পেছনের অ্যাপ সাধারণ HTTP/1.1-এ চলতে পারে।

### হাতে-কলমে যাচাই

```bash
curl -I --http2 https://www.cloudflare.com     # HTTP/2 দিয়ে
curl -I --http3 https://www.cloudflare.com     # HTTP/3 দিয়ে (curl-এর HTTP/3 সাপোর্টসহ বিল্ড লাগে)
curl -sI https://www.google.com | grep -i alt-svc   # সার্ভার HTTP/3 ঘোষণা করছে কিনা
```

**ব্রাউজারে দেখার উপায়:** DevTools খুলুন (F12) → **Network** ট্যাব → কলামের হেডারে ডান-ক্লিক করে **Protocol** চালু করুন। এখন প্রতিটা রিকোয়েস্টের পাশে দেখবেন `http/1.1`, `h2`, বা `h3`। Google, YouTube বা Cloudflare-এর কোনো সাইট খুলে দেখুন। অনেক রিকোয়েস্ট `h3` দেখাবে।

---

চার পর্বে আপনি নেটওয়ার্কিংয়ের মূল ভিত্তি প্রায় পুরোটাই ঘুরে এলেন: IP থেকে শুরু করে QUIC পর্যন্ত। এবার পুরোটার উপর একটা **কুইজ** বা **ফ্ল্যাশকার্ড** বানিয়ে দেব রিভিশনের জন্য? চাইলে **নেটওয়ার্ক সিকিউরিটি** (TLS-এর ভেতরের কাজ, certificate chain, DDoS, MITM আক্রমণ) বা **Kubernetes নেটওয়ার্কিং** (Service, Ingress, DNS-ভিত্তিক service discovery) নিয়েও এগোতে পারি।

