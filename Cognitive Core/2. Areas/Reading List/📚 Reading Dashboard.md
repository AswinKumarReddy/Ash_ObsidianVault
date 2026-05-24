

---

# 📥 Backlog (To Read)

```dataview
table priority as "Priority", author as "Author", genre as "Genre", pages as "Pages"
from "2. Areas"
where type = "book_reading_list_entry" and status = "backlog"
sort priority desc, date_added asc
```

---

# 📖 Currently Reading

```dataview
table author as "Author", genre as "Genre", progress as "Progress", pages as "Pages"
from "2. Areas"
where type = "book_reading_list_entry" and status = "in-progress"
sort date_added asc
```

---

# ✅ Finished Books

```dataviewjs
const pages = dv.pages('"Books"')
  .where(p => p.type === "book_reading_list_entry" && p.status === "done")
  .sort(p => p.rating, 'desc');

dv.table(
  ["Book", "Author", "Genre", "Rating", "Completed"],
  pages.map(p => {
    let r = Number(p.rating) || 0;
    let full = "⭐".repeat(Math.floor(r));
    let half = (r % 1 >= 0.5) ? "★" : "";
    let empty = "☆".repeat(5 - Math.ceil(r));

    return [
      p.file.link,
      p.author,
      p.genre,
      full + half + empty,
      p.date_completed
    ];
  })
);
```

---

# ⭐ Top Rated Books

```dataview
table file.link as "Book", author as "Author", genre as "Genre", rating as "Rating"
from "2. Areas"
where type = "book_reading_list_entry" and status = "done" and rating >= 4
sort rating desc
limit 10
```

---

# 📚 By Genre

## 🧠 Self Improvement

```dataview
table file.link as "Book", author, status
from "2. Areas"
where type = "book_reading_list_entry" and contains(lower(genre), "self")
sort status asc
```

---

## ⚔️ Fantasy / Fiction

```dataview
table file.link as "Book", author, status
from "2. Areas"
where type = "book_reading_list_entry" and (
	contains(lower(genre), "fantasy") or
	contains(lower(genre), "fiction")
)
sort status asc
```

---

## 💼 Business / Productivity

```dataview
table file.link as "Book", author, status
from "2. Areas"
where type = "book_reading_list_entry" and (
	contains(lower(genre), "business") or
	contains(lower(genre), "productivity")
)
sort status asc
```

---

# 🗑️ Archived

```dataview
table file.link as "Book", author as "Author", genre as "Genre"
from "2. Areas"
where type = "book_reading_list_entry" and status = "archived"
```

---

# 📊 Reading Stats

```dataview
table without id
	length(rows) as "Books Completed"
from "2. Areas"
where type = "book_reading_list_entry" and status = "done"
group by true
```

---

# 🚀 Workflow

## ➕ Add a Book

- Create a note inside `Books/`
- Use `Book Template`
- Keep:

```yaml
status: backlog
```

---

## 📖 Start Reading

```yaml
status: in-progress
progress: 25%
```

---

## ✅ Finish Book

```yaml
status: done
rating: 5
date_completed: 2026-05-24
```

---

## 🗑️ Archive

```yaml
status: archived
```

---

# 🧠 Rules

- Keep backlog manageable
- Finish before adding too many new books
- Archive books you stop enjoying
- Focus on retention, not collection
- Keep summaries concise

---

# 🔥 System Behavior

- Update `status`
- Dashboard updates automatically
- Click any book to open full note
- Ratings auto-sort your favorites