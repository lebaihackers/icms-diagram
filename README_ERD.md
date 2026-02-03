# 📊 ERD Documentation - Sistem E-Aduan JIM 3.0

## 📁 Files Included

Dokumentasi ERD (Entity Relationship Diagram) untuk sistem E-Aduan JIM 3.0 terdiri daripada 3 fail utama:

| File | Format | Description | Best For |
|------|--------|-------------|----------|
| **ERD_Diagram.md** | Markdown + Mermaid | Complete documentation dengan Mermaid diagram | Dokumentasi lengkap, GitHub |
| **ERD_Simplified.md** | Markdown | Gambaran ringkas dan mudah faham | Quick reference, overview |
| **ERD_Visual.puml** | PlantUML | Visual diagram untuk generate gambar | Presentation, detailed diagram |
| **README_ERD.md** | Markdown | Panduan penggunaan (fail ini) | Getting started |

---

## 🎯 Which File Should I Use?

### For **Quick Overview**
👉 **ERD_Simplified.md**
- Tree structure yang mudah faham
- Flow diagram ASCII art
- Ringkasan fungsi setiap table
- Best untuk: First-time readers, management

### For **Complete Documentation**
👉 **ERD_Diagram.md**
- Full table definitions
- All relationships explained
- Mermaid ERD diagram (visual)
- Indexes, constraints, security
- Best untuk: Developers, database admins

### For **Visual Presentation**
👉 **ERD_Visual.puml**
- PlantUML diagram format
- Can generate PNG/SVG images
- Detailed entity boxes with all fields
- Best untuk: Presentations, documentation

---

## 🖼️ How to View/Render ERD Diagrams

### Option 1: GitHub (Easiest)
1. Upload files ke GitHub repository
2. GitHub akan auto-render:
   - ✅ Markdown files (ERD_Diagram.md, ERD_Simplified.md)
   - ✅ Mermaid diagrams (dalam ERD_Diagram.md)
3. Click pada file untuk preview

### Option 2: VS Code (Local)
1. Install extension: **Markdown Preview Mermaid Support**
   ```
   Name: Markdown Preview Mermaid Support
   Id: bierner.markdown-mermaid
   Publisher: Matt Bierner
   ```
2. Open `ERD_Diagram.md`
3. Press `Ctrl+Shift+V` untuk preview
4. Mermaid diagram akan render automatically

### Option 3: PlantUML (for ERD_Visual.puml)

#### Method A: VS Code Extension
```bash
# Install extension
Name: PlantUML
Id: jebbs.plantuml
Publisher: jebbs
```

Cara guna:
1. Open `ERD_Visual.puml` in VS Code
2. Press `Alt+D` untuk preview
3. Right-click → Export → PNG/SVG

#### Method B: Command Line
```bash
# Download PlantUML JAR
# From: https://plantuml.com/download

# Generate PNG
java -jar plantuml.jar ERD_Visual.puml

# Generate SVG (better quality)
java -jar plantuml.jar -tsvg ERD_Visual.puml

# Output: ERD_Visual.png or ERD_Visual.svg
```

#### Method C: Online Tools
1. Copy content dari `ERD_Visual.puml`
2. Paste ke salah satu:
   - http://www.plantuml.com/plantuml/uml/
   - https://www.planttext.com/
   - https://plantuml-editor.kkeisuke.com/
3. Download as PNG/SVG

### Option 4: Mermaid Live Editor
1. Open `ERD_Diagram.md`
2. Copy code block yang bermula dengan ` ```mermaid`
3. Paste ke: https://mermaid.live/
4. Edit dan download as PNG/SVG

### Option 5: Draw.io / Lucidchart
1. Import data dari dokumentasi
2. Manually create diagram
3. Best untuk: Custom styling, presentation-ready diagrams

---

## 📋 Database Overview (Quick Stats)

```
Database: sistem_eaduan
Engine: InnoDB
Charset: utf8mb4_unicode_ci
Tables: 16
Views: 1
```

### Tables by Category

| Category | Count | Tables |
|----------|-------|--------|
| **Core** | 6 | aduan, pengadu, pentadbir, lampiran, video_lampiran, komen |
| **Workflow** | 3 | aduan_workflow_history, aduan_kembalikan, tindakan_aduan |
| **Notification** | 2 | notifikasi_pengadu, notifikasi_pentadbir |
| **Reference** | 2 | negeri, kategori_aduan |
| **Audit** | 3 | audit_logs, slow_queries, saved_searches |

---

## 🔗 Key Relationships

```
PENGADU (1) ─────► (N) ADUAN
                      │
PENTADBIR (1) ────────┼───────► (N) ADUAN
                      │            (3 roles)
                      │
                      ├───────► (N) LAMPIRAN
                      ├───────► (N) VIDEO_LAMPIRAN
                      ├───────► (N) KOMEN
                      ├───────► (N) WORKFLOW_HISTORY
                      └───────► (N) TINDAKAN

NEGERI (1) ──────► (N) PENGADU
           ──────► (N) PENTADBIR
           ──────► (N) ADUAN

KATEGORI_ADUAN (1) ──────► (N) ADUAN
```

---

## 📊 Important Notes

### 1. **Workflow Roles (PENTADBIR)**
```
super_admin          → Full system access
pegawai_penerima     → HQ Officer (receives & checks)
pengarah             → Director (assigns to state)
pegawai_negeri       → State Officer (takes action)
```

### 2. **Workflow Stages (ADUAN)**
```
1. baru                     → New submission
2. semakan_kelengkapan      → Completeness check (HQ)
3. tidak_lengkap            → Incomplete (returned)
4. menunggu_agihan          → Waiting assignment
5. dalam_tindakan           → Under action (State)
6. menunggu_pengesahan      → Waiting confirmation
7. selesai                  → Completed
8. ditolak                  → Rejected
```

### 3. **Foreign Key Behaviors**
- **CASCADE**: Delete related records (e.g., lampiran when aduan deleted)
- **SET NULL**: Keep record, nullify FK (preserve historical data)

### 4. **Security Features**
- ✅ Password hashing (bcrypt via PHP `password_hash()`)
- ✅ Audit logging (all critical actions)
- ✅ IP address tracking
- ✅ User agent logging
- ✅ JSON storage for flexible audit details

---

## 🔍 Common Use Cases

### For Developers
📖 Read: **ERD_Diagram.md**
- Understand table structure
- Learn relationships
- Check constraints & indexes
- SQL query examples

### For Database Admins
📖 Read: **ERD_Diagram.md** + **ERD_Visual.puml**
- Database schema
- Performance indexes
- Backup strategy
- Migration scripts location: `/db/*.sql`

### For Project Managers
📖 Read: **ERD_Simplified.md**
- High-level overview
- System capabilities
- Data flow understanding
- Planning & discussions

### For Presentations
🖼️ Generate: **ERD_Visual.puml** → PNG/SVG
- Visual diagram for slides
- Stakeholder meetings
- Documentation
- Training materials

---

## 📂 Related Files in Project

```
/eaduan/
├── db/
│   ├── schema_complete.sql              ← Full database schema
│   ├── migration_add_new_fields.sql     ← Recent migrations
│   ├── create_audit_logs.sql
│   ├── create_notifications_table.sql
│   └── ... (other migration files)
│
├── docs/
│   ├── ERD_Diagram.md                   ← COMPLETE DOCUMENTATION
│   ├── ERD_Simplified.md                ← QUICK OVERVIEW
│   ├── ERD_Visual.puml                  ← VISUAL DIAGRAM
│   ├── README_ERD.md                    ← THIS FILE
│   ├── architecture_detail.md
│   └── JIM_Discussion_Document.md
│
└── includes/
    └── db_connect.php                   ← Database connection
```

---

## 🛠️ Tools & Extensions Recommended

### VS Code Extensions
```json
{
  "recommendations": [
    "bierner.markdown-mermaid",     // Mermaid preview
    "jebbs.plantuml",                // PlantUML preview
    "yzhang.markdown-all-in-one",   // Markdown utilities
    "shd101wyy.markdown-preview-enhanced" // Enhanced preview
  ]
}
```

### Install Command
```bash
code --install-extension bierner.markdown-mermaid
code --install-extension jebbs.plantuml
code --install-extension yzhang.markdown-all-in-one
```

### Online Tools
- Mermaid Live: https://mermaid.live/
- PlantUML Online: http://www.plantuml.com/plantuml/
- Draw.io: https://app.diagrams.net/
- dbdiagram.io: https://dbdiagram.io/

---

## 📝 Update History

| Date | Version | Changes |
|------|---------|---------|
| 2026-02-03 | 1.0 | Initial ERD documentation created |
| - | - | 16 tables documented |
| - | - | 3 formats provided (MD, Mermaid, PlantUML) |

---

## 💡 Tips for Best Experience

### For Reading Documentation
1. Start with **ERD_Simplified.md** untuk overview
2. Then read **ERD_Diagram.md** untuk details
3. Refer to actual SQL files in `/db/` folder for implementation

### For Visual Diagram
1. Use **PlantUML** for detailed entity boxes
2. Use **Mermaid** for quick GitHub-friendly diagrams
3. Export to PNG/SVG for presentations

### For Database Development
1. Read ERD documentation first
2. Check `/db/schema_complete.sql` for schema
3. Use migration files in `/db/*.sql` untuk updates
4. Test queries on development database first

### For Documentation Updates
When database structure changes:
1. Update `/db/*.sql` files first
2. Then update ERD documentation files
3. Regenerate visual diagrams
4. Commit all changes together

---

## ❓ FAQ

### Q: Mana file paling penting?
**A:** **ERD_Diagram.md** - Contains complete documentation with Mermaid diagram.

### Q: Boleh render Mermaid diagram?
**A:** Yes! Upload to GitHub or use VS Code with Mermaid extension.

### Q: PlantUML tak boleh preview?
**A:** Install Java first, then PlantUML extension in VS Code.

### Q: Nak generate gambar ERD?
**A:** Use PlantUML (java -jar plantuml.jar ERD_Visual.puml) atau online tools.

### Q: Database structure berubah, apa perlu update?
**A:** 
1. Update `/db/*.sql` files
2. Update semua ERD documentation files
3. Regenerate visual diagrams

### Q: Format mana untuk presentation?
**A:** Generate PNG/SVG dari ERD_Visual.puml using PlantUML.

### Q: Boleh customize diagram?
**A:** Yes! Edit ERD_Visual.puml untuk custom colors, layout, etc.

---

## 📞 Support

Untuk soalan atau masalah:
1. Check documentation in `/docs/` folder
2. Review SQL schemas in `/db/` folder
3. Contact system administrator

---

## 📄 License & Credits

- **System**: E-Aduan JIM 3.0
- **Database**: MariaDB 10.6+ / MySQL 8.0+
- **Documentation**: Created on 3 February 2026
- **Tools Used**: Mermaid, PlantUML, Markdown

---

**Happy Reading! 📖**
