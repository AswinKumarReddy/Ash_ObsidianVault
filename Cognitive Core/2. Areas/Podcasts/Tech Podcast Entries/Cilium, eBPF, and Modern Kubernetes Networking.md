---
type: podcast
status: done
priority: medium
podcast:
episode:
duration: 59m
link:
rating: 3.5
date_added: 2026-04-05
date_completed:
tags:
  - podcast
  - tech
  - kubernetes
  - networking
  - ebpf
  - cilium
---

# 🎧 Cilium, eBPF, and Modern Kubernetes Networking

## 🔗 Episode Info
- Podcast: Software Engineering Daily
- Episode: Cilium, eBPF, and Modern Kubernetes Networking
- Duration: 59min
- Link: https://open.spotify.com/episode/1j8GN4lnCB0H1LXzWEpMfn

---

## 🎯 Why I Saved This
-  AI Suggested - Top rated in this podcast (just starting)
- 
- 

---

## 🚧 Listening Progress
- Notes while listening:
  - what is EBPF ?
  - Salem is a networking infrastructure for kubernetties. Kubernetties help you maintain the docker images
  - ebpf allow us to add programs to the kernel now without actually making changes to the it so this is an easier way of updating flows in the kernel in a safe way. How does it do it more investigate
  - Info on network mesh
  - Info on hubble and pwru
  - Is this relevent our realtime services like bromine 
  - Try out cilium hands on, starwars demo

---

# ✅ Summary (Fill ONLY after completion)

# 🧭 Key Takeaways  
  
1. **eBPF = programmable kernel**  
2. **Cilium = networking powered by eBPF**  
3. Shift from **IP-based → identity-based networking**  
4. **Service mesh without sidecars**  
5. Observability built into networking layer

  
# 🧠 Core Idea  
  
Modern Kubernetes networking struggles because:  
- Built for **static infrastructure (IPs, routes)**  
- Kubernetes is **dynamic (ephemeral pods, scaling)**  
  
👉 **Solution**:  
- **eBPF → makes Linux kernel programmable**  
- **Cilium → uses eBPF for networking, security, observability**


# 🔑 Key Concepts  
  
## 1. What is eBPF?  
- A way to **run programs inside the Linux kernel safely**  
- No need to:  
- modify kernel source  
- load kernel modules  
  
### Why it matters:  
- Networking happens in the kernel  
- eBPF allows **custom logic directly in packet flow**  
  
### Mental Model:  
- Old: user-space + iptables  
- New: **kernel-level execution (faster, simpler)**  
  
---  
  
## 2. What is Cilium?  
- A **Kubernetes CNI (networking layer)**  
- Built using **eBPF**  
  
### Handles:  
- Connectivity  
- Security policies  
- Observability  
  
### Key Advantage:  
- Moves logic **from user-space → kernel-space**  
  
---  
  
## 3. Problems with Traditional K8s Networking  
  
- iptables rules become large and slow  
- Debugging is difficult  
- Security is IP-based (not flexible)


---

## 💡 Actionable Insights and follow-ups
  
- [ ] **Try Cilium Star Wars demo**  
- [ ] Explore:  
	- L3/L7 policies  
	- service communication flows  
- [ ] Deeper understanding of Kubernetes vs Docker

---

## 📝 My Thoughts
- 
- 

---

## ⭐ Rating
- 