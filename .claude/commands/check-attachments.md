# Check Attachments — Find and Bin Orphans

Scans `04 - System/Attachments/` for files not referenced in any vault note and moves orphans to `04 - System/Bin/` for manual review and deletion.

## Usage

```
/check-attachments
```

No arguments needed. Safe to run repeatedly.

---

## Instructions

Run the Python script below exactly as written using the Bash tool. Do not modify it unless the user asks.

### Step 1 — Run the script

```bash
python3 << 'PYEOF'
import os, re, json, shutil

VAULT      = "/Users/Carl/Library/Mobile Documents/iCloud~md~obsidian/Documents/Home"
ATTACH_DIR = os.path.join(VAULT, "04 - System", "Attachments")
BIN_DIR    = os.path.join(VAULT, "04 - System", "Bin")

# ── 1. Collect all files in Attachments ──────────────────────────────────────
attachments = {}
for fname in os.listdir(ATTACH_DIR):
    fpath = os.path.join(ATTACH_DIR, fname)
    if os.path.isfile(fpath):
        attachments[fname] = fpath

if not attachments:
    print("Attachments folder is empty. Nothing to check.")
    exit()

# ── 2. Scan every .md and .canvas file in the vault for references ────────────
referenced = set()  # lowercase filenames found in any note or canvas

for root, dirs, files in os.walk(VAULT):
    # Skip hidden folders (.obsidian, .claude, etc.) and Bin
    dirs[:] = [d for d in dirs if not d.startswith('.') and d != 'Bin']
    for fname in files:
        fpath = os.path.join(root, fname)

        if fname.endswith('.md'):
            # Markdown: wikilinks and standard markdown links/embeds
            try:
                with open(fpath, 'r', encoding='utf-8', errors='ignore') as f:
                    content = f.read()
                # Wikilinks:  [[file.ext]]  or  [[file.ext|alias]]
                for link in re.findall(r'\[\[([^\]|]+?)(?:\|[^\]]+?)?\]\]', content):
                    referenced.add(os.path.basename(link).lower())
                # Markdown links/embeds:  ![alt](path)  or  [text](path)
                for link in re.findall(r'!?\[[^\]]*\]\(([^)]+)\)', content):
                    referenced.add(os.path.basename(link).lower())
            except Exception:
                pass

        elif fname.endswith('.canvas'):
            # Canvas (JSON): file-type nodes reference attachments by vault path;
            # text-type nodes may contain wikilinks
            try:
                with open(fpath, 'r', encoding='utf-8', errors='ignore') as f:
                    canvas = json.load(f)
                for node in canvas.get('nodes', []):
                    if node.get('type') == 'file' and 'file' in node:
                        # e.g. "04 - System/Attachments/image.png"
                        referenced.add(os.path.basename(node['file']).lower())
                    elif node.get('type') == 'text' and 'text' in node:
                        for link in re.findall(r'\[\[([^\]|]+?)(?:\|[^\]]+?)?\]\]', node['text']):
                            referenced.add(os.path.basename(link).lower())
            except Exception:
                pass

# ── 3. Classify ───────────────────────────────────────────────────────────────
orphans = {n: p for n, p in attachments.items() if n.lower() not in referenced}
safe    = {n: p for n, p in attachments.items() if n.lower() in referenced}

print(f"Attachments scanned : {len(attachments)}")
print(f"Referenced (kept)   : {len(safe)}")
print(f"Orphaned (to bin)   : {len(orphans)}")

if safe:
    print("\nKept (referenced in vault):")
    for name in sorted(safe):
        print(f"  ✓  {name}")

# ── 4. Move orphans to Bin ────────────────────────────────────────────────────
if not orphans:
    print("\nNo orphans found. Attachments folder is clean.")
else:
    os.makedirs(BIN_DIR, exist_ok=True)
    print(f"\nMoved to 04 - System/Bin/:")
    for name in sorted(orphans):
        src = orphans[name]
        dst = os.path.join(BIN_DIR, name)
        if os.path.exists(dst):                         # avoid overwriting Bin duplicates
            base, ext = os.path.splitext(name)
            dst = os.path.join(BIN_DIR, f"{base}_dup{ext}")
        shutil.move(src, dst)
        print(f"  →  {name}")
    print(f"\nDone. Review 04 - System/Bin/ and delete manually when ready.")
PYEOF
```

### Step 2 — Report back

After the script runs, confirm:
- How many files were in Attachments
- Which files were kept (referenced) and which were moved to Bin
- Whether the Bin folder was created or already existed

---

## Rules

- **Never delete files directly** — move to Bin only. Carl deletes manually.
- **Never touch files outside** `04 - System/Attachments/`
- **Safe to re-run** — already-binned files are excluded from scanning automatically
- If Bin does not exist, create it before moving
- Report every file moved — no silent operations
