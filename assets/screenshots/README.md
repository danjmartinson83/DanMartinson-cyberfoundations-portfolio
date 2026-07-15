# Screenshots

Every image you reference from a lab, note, or reflection lives here — one subfolder per week.

## Folder Naming

Use the same week number as the folder it supports:

```
assets/screenshots/
├── week-02/
├── week-04/
├── week-07/
├── week-09/
└── week-11/
```

Only create a week's subfolder when you actually have a screenshot to put in it — don't pre-create empty folders for weeks you haven't reached yet.

## File Naming

Name each file for what it shows, not for when you took it:

```
week-02/hardware-diagram.png
week-04/vm-network-settings.png
week-07/nsg-inbound-rules.png
```

Avoid generic names like `Screenshot 2026-07-03 at 4.12.03 PM.png` — rename before you commit. Use lowercase with hyphens, no spaces.

## Format and Size

- PNG or JPG only
- Crop to the relevant window or region — don't submit a full-desktop screenshot when the lab only needs one dialog box
- Redact anything sensitive before committing: your real IP address, subscription/account IDs, personal file paths, or any credentials visible on screen

## Referencing From a Lab

From `week-0X/labs/lab-0X-[name].md`:

```markdown
![NSG inbound rules](../../assets/screenshots/week-07/nsg-inbound-rules.png)
```

Double-check the image renders on GitHub (not just locally) before you consider the lab done — a broken image link is one of the most common submission issues.
