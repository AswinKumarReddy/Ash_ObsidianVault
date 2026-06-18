---
tags:
  - dashboard
  - podcast
  - dataview
---

# 🎧 Podcast Dashboard

---

## 📥 Backlog (To Listen)

```dataview
table priority, podcast, duration
from "2. Areas"
where type = "podcast" and status = "backlog"
sort priority desc, date_added asc
```

---

## ▶️ In Progress

```dataview
table podcast, episode, duration
from "2. Areas"
where type = "podcast" and status = "in-progress"
sort date_added asc
```

---

## ✅ Completed

```dataviewjs
const pages = dv.pages('"2. Areas"')
  .where(p => p.type === "podcast" && p.status === "done")
  .sort(p => p.rating, 'desc');

dv.table(
  ["Episode", "Podcast", "Rating", "Date"],
  pages.map(p => {
    let r = Number(p.rating) || 0;
    let full = "⭐".repeat(Math.floor(r));
    let half = (r % 1 >= 0.5) ? "★" : "";
    let empty = "☆".repeat(5 - Math.ceil(r));

    return [
      p.file.link,
      p.podcast,
      full + half + empty,
      p.date_completed
    ];
  })
);
```

---

## ⭐ Top Rated (Quick Revisit)

```dataview
table file.link as "Episode", podcast, episode, rating
from "2. Areas"
where type = "podcast" and status = "done" and rating >= 4
sort rating desc
limit 10
```

---

## 🗑️ Archived

```dataview
table file.link as "Episode", podcast, episode
from "2. Areas"
where type = "podcast" and status = "archived"
```

---

# ⚙️ How to Use

### ➕ Add a Podcast

- Create a new note in `Podcasts/`
    
- Use your template
    
- Fill basic info
    
- Keep:
    
    - `status: backlog`
        

---

### ▶️ Start Listening

Update the note:

```yaml
status: in-progress
```

---

### ✅ Finish Episode

Update:

```yaml
status: done
rating: 4
date_completed: YYYY-MM-DD
```

Then fill your summary in the same note.

---

### 🗑️ Archive

```yaml
status: archived
```

---

# 🧠 Rules

- Keep backlog ≤ 20–30 episodes
    
- If skipped twice → archive
    
- Don’t over-write summaries (keep it short)
    
- Focus on completion, not collection
    

---

# 🚀 That’s It

- Click any **Episode** → opens full note
    
- Update `status` → it moves automatically
    
- Dashboard updates instantly
    

You now have a **self-updating podcast system**