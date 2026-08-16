---
tags:
  - watchlist
  - anime
  - dataview
---

# Anime Watch List

```dataviewjs
const statusOptions = [
  "Awaiting first episode",
  "Somewhere in the arc",
  "Credits rolled"
];

const statusRank = new Map(statusOptions.map((status, index) => [status, index]));
const startMarker = "<!-- anime-data-start";
const endMarker = "anime-data-end -->";
const path = dv.current().file.path;
const file = app.vault.getAbstractFileByPath(path);
const content = await app.vault.read(file);

function readEntries() {
  const start = content.indexOf(startMarker);
  const end = content.indexOf(endMarker);
  if (start === -1 || end === -1 || end <= start) return [];

  const raw = content.slice(start + startMarker.length, end).trim();
  if (!raw) return [];

  try {
    return JSON.parse(raw);
  } catch (error) {
    dv.paragraph("Could not read anime data. Check the JSON block at the bottom of this note.");
    throw error;
  }
}

async function saveEntries(entries) {
  const sorted = [...entries].sort((a, b) => {
    const statusDiff = (statusRank.get(a.status) ?? 99) - (statusRank.get(b.status) ?? 99);
    return statusDiff || a.title.localeCompare(b.title);
  });

  const nextData = `${startMarker}\n${JSON.stringify(sorted, null, 2)}\n${endMarker}`;
  const nextContent = content.replace(
    new RegExp(`${startMarker}[\\s\\S]*?${endMarker}`),
    nextData
  );

  await app.vault.modify(file, nextContent);
}

function inputCell(value, placeholder, onChange, type = "text") {
  const input = document.createElement("input");
  input.type = type;
  input.value = value ?? "";
  input.placeholder = placeholder;
  input.style.width = "100%";
  input.onchange = () => onChange(input.value.trim());
  return input;
}

function saveButton(label, onClick) {
  const button = document.createElement("button");
  button.textContent = label;
  button.onclick = onClick;
  return button;
}

const entries = readEntries().sort((a, b) => {
  const statusDiff = (statusRank.get(a.status) ?? 99) - (statusRank.get(b.status) ?? 99);
  return statusDiff || a.title.localeCompare(b.title);
});

const root = dv.el("div", "");
root.addClass("anime-watchlist");

const addButton = saveButton("Add anime", async () => {
  const title = prompt("Anime name");
  if (!title?.trim()) return;

  await saveEntries([
    ...entries,
    {
      title: title.trim(),
      status: statusOptions[0],
      rating: "",
      finished: "",
      notes: ""
    }
  ]);
});
root.appendChild(addButton);

const table = document.createElement("table");
table.style.width = "100%";
table.style.marginTop = "0.75rem";

const header = table.createTHead().insertRow();
for (const heading of ["Anime", "Status", "Rating", "Finished", "Notes"]) {
  const th = document.createElement("th");
  th.textContent = heading;
  header.appendChild(th);
}

const body = table.createTBody();

for (const [index, entry] of entries.entries()) {
  const row = body.insertRow();

  const titleCell = row.insertCell();
  titleCell.appendChild(inputCell(entry.title, "Anime name", async value => {
    entries[index].title = value;
    await saveEntries(entries);
  }));

  const statusCell = row.insertCell();
  const status = document.createElement("select");
  status.style.width = "100%";
  for (const option of statusOptions) {
    const item = document.createElement("option");
    item.value = option;
    item.textContent = option;
    item.selected = entry.status === option;
    status.appendChild(item);
  }
  status.onchange = async () => {
    entries[index].status = status.value;
    await saveEntries(entries);
  };
  statusCell.appendChild(status);

  const ratingCell = row.insertCell();
  const rating = inputCell(entry.rating, "0-5", async value => {
    entries[index].rating = value;
    await saveEntries(entries);
  }, "number");
  rating.min = "0";
  rating.max = "5";
  rating.step = "0.5";
  ratingCell.appendChild(rating);

  const finishedCell = row.insertCell();
  finishedCell.appendChild(inputCell(entry.finished, "YYYY-MM-DD", async value => {
    entries[index].finished = value;
    await saveEntries(entries);
  }, "date"));

  const notesCell = row.insertCell();
  notesCell.appendChild(inputCell(entry.notes, "Optional", async value => {
    entries[index].notes = value;
    await saveEntries(entries);
  }));
}

root.appendChild(table);
```

<!--
The hidden JSON block below stores the table rows.
Use the rendered table above instead of editing this by hand.
-->

<!-- anime-data-start
[
  {
    "title": "Attack on Titan",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "Chainsaw Man",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "My Hero Academia",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "Tokyo Revengers",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "Vinland Saga",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "Wind Breaker",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "Frieren season 2",
    "status": "Credits rolled",
    "rating": "",
    "finished": "",
    "notes": ""
  }
]
anime-data-end -->
addButton.onclick = async () => {
  const title = prompt("Anime name");
  if (!title?.trim()) return;

  await saveEntries([
    ...entries,
    {
      title: title.trim(),
      status: statusOptions[0],
      rating: "",
      finished: "",
      notes: ""
    }
  ]);
};

dv.table(
  ["Anime", "Status", "Rating", "Finished", "Notes"],
  entries.map((entry, index) => {
    const title = inputCell(entry.title, "Anime name", async value => {
      entries[index].title = value;
      await saveEntries(entries);
    });

    const status = document.createElement("select");
    for (const option of statusOptions) {
      const item = document.createElement("option");
      item.value = option;
      item.textContent = option;
      item.selected = entry.status === option;
      status.appendChild(item);
    }
    status.onchange = async () => {
      entries[index].status = status.value;
      await saveEntries(entries);
    };

    const rating = inputCell(entry.rating, "0-5", async value => {
      entries[index].rating = value;
      await saveEntries(entries);
    }, "number");
    rating.min = "0";
    rating.max = "5";
    rating.step = "0.5";

    const finished = inputCell(entry.finished, "YYYY-MM-DD", async value => {
      entries[index].finished = value;
      await saveEntries(entries);
    }, "date");

    const notes = inputCell(entry.notes, "Optional", async value => {
      entries[index].notes = value;
      await saveEntries(entries);
    });

    return [title, status, rating, finished, notes];
  })
);
```

<!-- anime-data-start
[
  {
    "title": "Attack on Titan",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "Chainsaw Man",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "My Hero Academia",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "Tokyo Revengers",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "Vinland Saga",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "Wind Breaker",
    "status": "Awaiting first episode",
    "rating": "",
    "finished": "",
    "notes": ""
  },
  {
    "title": "Frieren season 2",
    "status": "Credits rolled",
    "rating": "",
    "finished": "",
    "notes": ""
  }
]
anime-data-end -->
