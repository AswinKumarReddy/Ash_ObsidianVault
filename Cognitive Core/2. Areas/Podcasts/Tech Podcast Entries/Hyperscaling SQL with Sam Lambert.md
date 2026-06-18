---
type: podcast
status: done
priority: high
podcast:
episode:
duration: 45m
link:
rating: 3
date_added: 2026-04-06
date_completed:
tags:
  - podcast
  - tech
  - databases
  - sql
  - scaling
---

# 🎧 Hyperscaling SQL with Sam Lambert

## 🔗 Episode Info
- Podcast: Software Engineering Daily
- Episode: Hyperscaling SQL with Sam Lambert
- Duration: 45min
- Link: https://open.spotify.com/episode/6MW3BPjDKFW1jE2NIQoXrN

---

## 🎯 Why I Saved This
- 
- 

---

## 🚧 Listening Progress

- Notes while listening:
  - what are the limitations of implementing somw functions with sharding like foreign key
  - What is trigger in mysql and why cant it be done with sharding
  - check our whats the difference btwn mysql and postgres

Post listening research:
#### Sharding limitations (foreign keys)  
- Sharding splits data across multiple databases (shards)  
- Foreign keys require checking related data in another table  
- In sharded systems:  
- Related data may live in different shards ❌  
- Requires cross-shard queries → slow & complex  
- **Result:** Foreign keys are usually disabled  
- **Alternative:** Enforce relationships in application logic or async validation jobs  
  
  
#### Triggers in MySQL & sharding  
  
**What is a trigger?**  
- Automatic DB logic executed on events (INSERT, UPDATE, DELETE)  
  
**Why it doesn’t work with sharding:**  
- Assumes all data is local to one DB  
- Sharding spreads data across nodes  
- Leads to:  
- Cross-shard communication ❌  
- Performance issues ❌  
- Inconsistent execution ❌  
  
**Result:** Avoid triggers in sharded systems  
**Alternative:** Use event-driven systems (queues, workers, Kafka)

---

# ✅ Summary (Fill ONLY after completion)

Sam Lambert (CEO of PlanetScale) explains how to scale relational databases—especially MySQL—to massive workloads using **sharding + Vitess**, while _rethinking traditional SQL features_.

## 🧠 Key Takeaways
- Sharding is the only real way to hyperscale SQL
- SQL features don’t scale cleanly across shards
- Vitess = abstraction layer over MySQL
	- Makes sharded DB _feel_ like a single DB
    - Query routing
    - Connection pooling
    - Resharding



---

## 💡 Actionable Insights
- [ ] Learn more about MySQL vs PostgreSQL, and when to use what. 
- [ ] 

---

## 📝 My Thoughts
- 
- 

---

## ⭐ Rating
- 