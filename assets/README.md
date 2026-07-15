# Assets

This folder holds screenshots, diagrams, and any other supporting images referenced from your lab files. Nothing else goes here — no lab write-ups, no notes, no reflections.

## Structure

Organize by week, matching your `week-0X/` folders:

```
assets/
└── screenshots/
    ├── week-02/
    │   └── diagram.png
    └── week-0X/
        └── ...
```

## Embedding Images (Relative Paths Only)

From a lab file at `week-0X/labs/lab-0X-[name].md`, reference an image like this:

```markdown
![Description](../../assets/screenshots/week-0X/filename.png)
```

**Do NOT use:**
- Absolute file paths from your computer (e.g. `C:\Users\YourName\Desktop\image.png`)
- Drag-and-drop links that reference your local machine
- Public URL links unless a lab explicitly tells you to

If an image doesn't render on GitHub, the path is almost always the problem — count the folder levels and fix it before committing. See the CVI GitHub Handbook for a full relative-path refresher.
