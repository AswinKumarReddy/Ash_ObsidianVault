---
tags:
  - watchlist
  - anime
  - dataview
---

# Anime Watch List

## Add Here

- [ ] Wind Breaker
- [ ] Tokyo Revengers
- [ ] Attack on Titan
- [ ] Chainsaw Man
- [ ] My Hero Academia
- [ ] Vinland Saga
- [x] Frieren season 2 [rating:: ] [finished:: ]

## To Watch

```dataview
TASK
WHERE file.path = this.file.path
  AND meta(section).subpath = "Add Here"
  AND !completed
SORT text ASC
```

## Completed

```dataview
TASK
WHERE file.path = this.file.path
  AND meta(section).subpath = "Add Here"
  AND completed
SORT finished DESC, rating DESC, text ASC
```

## Quick Format

```text
- [ ] Anime name
- [x] Anime name [rating:: 4] [finished:: 2026-08-16]
```
