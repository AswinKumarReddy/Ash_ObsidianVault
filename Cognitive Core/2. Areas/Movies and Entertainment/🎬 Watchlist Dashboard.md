
---

# 📥 Backlog (To Watch)

```dataview
table 
	category as "Type",
	priority as "Priority",
	genre as "Genre",
	platform as "Platform",
	runtime as "Runtime"
from "2. Areas"
where type = "watch_list_entry" and status = "backlog"
sort priority desc, date_added asc
```

---

# ▶️ Currently Watching

```dataview
table
	category as "Type",
	genre as "Genre",
	progress as "Progress",
	platform as "Platform"
from "2. Areas"
where type = "watch_list_entry" and status = "in-progress"
sort date_added asc
```

---

# ✅ Completed

```dataviewjs
const pages = dv.pages('"2. Areas"')
  .where(p => p.type === "watch_list_entry" && p.status === "done")
  .sort(p => p.rating, 'desc');

function renderStars(rating) {
    rating = Number(rating) || 0;

    let full = Math.floor(rating);
    let half = rating % 1 >= 0.5 ? 1 : 0;
    let empty = 5 - full - half;

    return "⭐".repeat(full) +
           "✨".repeat(half) +
           "☆".repeat(empty);
}

dv.table(
  ["Title", "Type", "Genre", "Rating", "Completed"],
  pages.map(p => [
      p.file.link,
      p.category,
      p.genre,
      renderStars(p.rating),
      p.date_completed
  ])
);
```

---

# ⭐ Top Rated

```dataview
table 
	file.link as "Title",
	category as "Type",
	genre as "Genre",
	rating as "Rating"
from "2. Areas"
where type = "watch_list_entry" and status = "done" and rating >= 4
sort rating desc
limit 15
```

---

# 📺 Series In Progress

```dataview
table
	series_name as "Series",
	season as "Season",
	episode as "Episode",
	progress as "Progress"
from "2. Areas"
where type = "watch_list_entry"
and category = "series"
and status = "in-progress"
sort series_name asc
```

---

# 🎥 Movies To Watch Soon

```dataview
table
	genre as "Genre",
	platform as "Platform",
	priority as "Priority"
from "2. Areas"
where type = "watch_list_entry"
and category = "movie"
and priority = "high"
and status != "done"
sort date_added asc
```

---

# 🗑️ Archived

```dataview
table
	file.link as "Title",
	category as "Type",
	genre as "Genre"
from "2. Areas"
where type = "watch_list_entry" and status = "archived"
```

---

# 📊 Watch Stats

## Total Completed

```dataview
table without id
	length(rows) as "Completed Entries"
from "2. Areas"
where type = "watch_list_entry" and status = "done"
group by true
```

---

## Movies vs Series

```dataview
table length(rows) as "Count"
from "2. Areas"
where type = "watch_list_entry"
group by category
```

---

# 🚀 Workflow

## ➕ Add Entry

- Create note in your watch folder
- Use `Watch Template`
- Keep:

```yaml
status: backlog
```

---

## ▶️ Start Watching

```yaml
status: in-progress
progress: Episode 3 / Season 1
```

---

## ✅ Finish Watching

```yaml
status: done
rating: 4.5
date_completed: 2026-05-24
```

---

## 🗑️ Archive

```yaml
status: archived
```

---

# 🧠 Rules

- Keep watchlist manageable
- Archive dropped series
- Don’t endlessly collect recommendations
- Prioritize completion
- Rate immediately after finishing

---

# 🔥 System Behavior

- Update `status`
- Dashboard updates automatically
- Ratings auto-sort favorites
- Click any title to open full review