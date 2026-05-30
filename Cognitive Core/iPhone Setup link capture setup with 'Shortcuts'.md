### Flow:
```
iPhone → Google Sheets → Obsidian Capture System
```

Resources:
- Google Form: 
- Google Sheet: https://docs.google.com/spreadsheets/d/10W1JNMVprc_iMHuwiowky_5DWCrkxGVRxvKhNPmBsfE/edit?usp=sharing

## Goal

Capture content from an iPhone with minimal friction and process it later in Obsidian.

Supported content:

- YouTube videos
- Articles
- Web pages
- References
- Future: tasks and ideas

Architecture:

```text
iPhone
    ↓
Shortcut (Share Sheet)
    ↓
Google Form
    ↓
Google Sheet
    ↓
PC Script (future)
    ↓
Obsidian Inbox
```

---

# What We Built

We created a Share Sheet shortcut that:

1. Appears in the iPhone Share menu.
2. Receives a URL from Chrome, Safari, YouTube, etc.
3. Extracts metadata where possible.
4. Sends the captured information to a Google Form.
5. The Google Form automatically stores the entry in Google Sheets.

This avoids:

- Zapier
- Make.com
- Cloud automation services
- Manual copy/paste

---

# Google Sheets Setup

## Create Sheet

Create a Google Sheet:

```text
Knowledge Capture
```

Columns:

|Timestamp|Source|Title|URL|
|---|---|---|---|

---

# Google Form Setup

## Create Form

Create:

```text
Knowledge Capture Form
```

Fields:
### Source

```text
Short Answer
```

Example:

```text
iPhoneSave
```

---

### Title

```text
Short Answer
```

---

### URL

```text
Short Answer
```

---

## Connect Form To Sheet

Google Forms:

```text
Responses
    ↓
Link to Spreadsheet
    ↓
Knowledge Capture
```

Every submission becomes a row.

---

# Find Google Form Field IDs

Open Form Preview. (Eye symbol)

Inspect page source.

Find entries similar to:

```text
entry.1114988905
entry.339363384
entry.544040729
```

Example mapping:

```text
Source → entry.1114988905
Title  → entry.339363384
URL    → entry.544040729
```

Save these IDs.

---

# Create iPhone Shortcut

## Step 1

Open:

```text
Shortcuts
```

Create (empty shortcut with no actions):

```text
Save Link
```

---

## Step 2

Enable Share Sheet,  (long press the new shortcut to see this option)

Shortcut Details:

```text
Show in Share Sheet = ON
```

Accepted Types:

```text
URLs
Web Pages
Text
```

---

## Step 3

Receive Shared URL

Action:

```text
Get URLs from Input
```

---

## Step 4

Extract Title

Action:

```text
Get Details of URL
```

Property:

```text
Name
```

Note:

YouTube often returns:

```text
YouTube
```

instead of the actual video title.

This is acceptable for now because the future PC script can fetch proper metadata.

---

## Step 5

URL Encode Title

Action:

```text
URL Encode
```

Input:

```text
Title
```

Store result:

```text
Encoded Title
```

---

## Step 6

URL Encode Shared URL

Action:

```text
URL Encode
```

Input:

```text
Shared URL
```

Store result:

```text
Encoded URL
```

---

## Step 7

Build Google Form Submission URL

Add:

```text
Text
```

Template:

```text
https://docs.google.com/forms/d/e/FORM_ID/formResponse?entry.1114988905=iPhoneSave&entry.339363384=[Encoded Title]&entry.544040729=[Encoded URL]
```

Important:

Only encode:

```text
Title
URL
```

Never encode the entire form URL.

Correct:

```text
...?entry.title=My%20Title
```

Wrong:

```text
formResponse%3Fentry...
```

---

## Step 8

Submit Form

Action:

```text
Get Contents of URL
```

Input:

```text
Generated Form URL
```

Method:

```text
GET
```

---

## Step 9

Success Notification

Action:

```text
Show Notification
```

Message:

```text
Saved to Knowledge Capture
```

---

# Usage

## Saving A YouTube Video

```text
YouTube
    ↓
Share
    ↓
Save Link
    ↓
Done
```

Google Sheet receives:

|Timestamp|Source|Title|URL|
|---|---|---|---|
|...|iPhoneSave|YouTube|video URL|

---

## Saving An Article

```text
Chrome
    ↓
Share
    ↓
Save Link
    ↓
Done
```

Google Sheet receives:

|Timestamp|Source|Title|URL|
|---|---|---|---|
|...|iPhoneSave|Article Title|article URL|

---

# Future Obsidian Integration

A Python script on the PC will:

1. Read new rows from Google Sheets.
    
2. Track the last processed row.
    
3. Avoid duplicates.
    
4. Generate markdown entries.
    
5. Append to:
    

```text
Obsidian/Inbox.md
```

Example:

```markdown
# Inbox

## Articles

- [ ] Read https://example.com/article

## Videos

- [ ] Watch https://youtube.com/watch?v=abc123
```

---

# Lessons Learned

1. Share Sheet debugging is easiest with:
    

```text
Show Result
→ Shortcut Input
```

2. Chrome and YouTube provide different metadata.
    
3. YouTube often does not expose the actual video title through Shortcuts.
    
4. URL encoding is required for:
    
    - Titles with spaces
        
    - URLs containing `?`, `=`, `&`
        
5. Encode only variable values, not the entire Google Form URL.
    
6. Google Forms + Google Sheets is a simple and reliable capture backend for iPhone shortcuts.