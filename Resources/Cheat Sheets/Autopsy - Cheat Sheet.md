# Autopsy Cheat Sheet
**Digital Forensics — Quick Reference**

---

## Core Workflow

1. Verify/hash the forensic image before starting
2. Create a new **Case**
3. Add the image as a **Data Source**
4. Run **ingest modules** (hash lookup, keyword search, timeline, etc.)
5. Review results by category, tag evidence
6. Generate a report

---

## Case Setup (GUI Workflow)

| Step | Detail |
|---|---|
| New Case | File → New Case → name it, set base directory |
| Add Data Source | Select image type (Disk Image, Local Drive, Logical Files) → point to file |
| Ingest Modules | Select which modules run automatically on import (see table below) |
| Timeline | Tools → Timeline, once ingest completes |
| Reporting | Tools → Generate Report → choose format (HTML, PDF, Excel) |

---

## Common Ingest Modules

| Module | Purpose |
|---|---|
| **Hash Lookup** | Flags known-good (NSRL) or known-bad files by hash |
| **File Type Identification** | Identifies true file type regardless of extension |
| **Keyword Search** | Indexes and searches all text content in the image |
| **Timeline** | Builds a chronological view of file system activity |
| **Recent Activity** | Extracts browser history, recent documents, USB device history |
| **Registry Analysis** | Parses Windows registry hives for artifacts |
| **PhotoRec Carver** | Recovers deleted files via data carving |
| **Email Parser** | Extracts and indexes email content (PST, MBOX, etc.) |

---

## Evidence Review Panes

| Pane | Shows |
|---|---|
| **Data Sources** | The image(s)/drive(s) added to the case |
| **File Types** | Files categorized by type (documents, images, executables, etc.) |
| **Deleted Files** | Recoverable deleted files found during carving |
| **Results** | Hits from ingest modules (keyword hits, hash matches, web history) |
| **Tags** | Evidence you've manually flagged during review |

---

## Sleuth Kit CLI Quick Reference

*(Autopsy's underlying engine — useful for scripting or quick lookups outside the GUI)*

| Command | Purpose |
|---|---|
| `mmls image.dd` | Display partition table/layout |
| `fsstat image.dd` | Display file system details for a partition |
| `fls -r image.dd` | List all files recursively, including deleted |
| `fls -rd image.dd` | List only deleted files |
| `icat image.dd <inode>` | Extract file contents by inode number |
| `istat image.dd <inode>` | Display metadata for a specific inode |

---

## Hashing (Integrity Verification)

| Command | Purpose |
|---|---|
| `md5sum image.dd` | Generate MD5 hash of an image |
| `sha1sum image.dd` | Generate SHA1 hash of an image |
| `sha256sum image.dd` | Generate SHA256 hash of an image |

**Always hash before and after acquisition/analysis** — matching hashes prove the image wasn't altered.

---

## Pro Tips

- **Never analyze the original evidence.** Work exclusively from a verified image or write-blocked copy.
- **Hash first, hash again at the end.** A mismatched hash invalidates the integrity of the entire analysis.
- **Let ingest modules finish before drawing conclusions.** Keyword search and timeline indexing can take significant time on large images — premature review misses results still being indexed.
- **Tag as you go.** Don't rely on memory to reconstruct which files mattered and why — tag and annotate evidence during the first pass.
- **Cross-reference Recent Activity + Timeline together** — browser history alone rarely tells the full story without file system context around it.
- **Document methodology in real time**, not after the fact — reconstructing steps after the analysis is finished is unreliable and looks unreliable in a report.
