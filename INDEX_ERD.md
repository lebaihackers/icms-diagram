# 📚 Index - ERD Documentation

## 📂 Dokumentasi ERD Sistem E-Aduan JIM 3.0

Dokumentasi lengkap Entity Relationship Diagram untuk database `sistem_eaduan`.

---

## 📑 Quick Navigation

| # | File | Format | Description | Best For |
|---|------|--------|-------------|----------|
| 1 | [ERD_Simplified.md](ERD_Simplified.md) | Markdown | 🎯 Ringkasan & overview | Quick reference, first-time readers |
| 2 | [ERD_Diagram.md](ERD_Diagram.md) | Markdown + Mermaid | 📖 Complete documentation | Developers, detailed study |
| 3 | [ERD_Visual.puml](ERD_Visual.puml) | PlantUML | 🖼️ Visual diagram source | Generate PNG/SVG images |
| 4 | [ERD_ASCII.txt](ERD_ASCII.txt) | ASCII Art | 📺 Text-based diagram | Terminal viewing, printing |
| 5 | [README_ERD.md](README_ERD.md) | Markdown | 📚 Usage guide | Getting started, how-to |
| 6 | **INDEX.md** | Markdown | 📋 This file | Navigation hub |

---

## 🎯 Start Here

### New to the System?
👉 Start with **[ERD_Simplified.md](ERD_Simplified.md)**
- Get overview of database structure
- Understand main entities
- See data flow diagrams

### Need Details?
👉 Read **[ERD_Diagram.md](ERD_Diagram.md)**
- Complete table definitions
- All relationships explained
- Indexes and constraints
- Security features
- Sample queries

### Need Visual Diagram?
👉 Use **[ERD_Visual.puml](ERD_Visual.puml)**
- Generate PNG/SVG images
- For presentations
- For documentation
- See [README_ERD.md](README_ERD.md) for how-to

### Working in Terminal?
👉 View **[ERD_ASCII.txt](ERD_ASCII.txt)**
- Text-based diagram
- No tools needed
- Easy to print
- Quick reference

### Don't Know Where to Start?
👉 Read **[README_ERD.md](README_ERD.md)**
- Step-by-step guide
- Tool recommendations
- FAQ section
- Tips & tricks

---

## 📊 Database Overview

```
Database: sistem_eaduan
Engine: InnoDB
Charset: utf8mb4_unicode_ci
Tables: 16
```

### Table Categories

| Category | Count | Tables |
|----------|-------|--------|
| 👥 Users | 2 | pengadu, pentadbir |
| 📝 Core | 6 | aduan, lampiran, video_lampiran, komen, aduan_workflow_history, aduan_kembalikan |
| 🔔 Notifications | 2 | notifikasi_pengadu, notifikasi_pentadbir |
| 📚 Reference | 2 | negeri, kategori_aduan |
| 🔍 Audit | 4 | audit_logs, slow_queries, news_updates, saved_searches |

---

## 🔗 Quick Links

### Related Documentation
- [Database Schema (SQL)](../db/schema_complete.sql)
- [Migration Scripts](../db/)
- [Architecture Documentation](architecture_detail.md)
- [JIM Discussion Document](JIM_Discussion_Document.md)

### External Resources
- [Mermaid Live Editor](https://mermaid.live/)
- [PlantUML Online](http://www.plantuml.com/plantuml/)
- [dbdiagram.io](https://dbdiagram.io/)

---

## 📖 Reading Order (Recommended)

For **First-Time Readers**:
```
1. ERD_Simplified.md     (15 min) - Get overview
2. ERD_Diagram.md        (30 min) - Understand details
3. ERD_Visual.puml       (5 min)  - Generate visual diagram
```

For **Developers**:
```
1. ERD_Diagram.md        - Complete documentation
2. /db/schema_complete.sql - Actual SQL schema
3. ERD_ASCII.txt         - Quick reference while coding
```

For **Database Admins**:
```
1. ERD_Diagram.md        - Schema understanding
2. ERD_Visual.puml       - Generate documentation images
3. /db/schema_complete.sql - Implementation
4. /db/migration_*.sql   - Database updates
```

For **Project Managers**:
```
1. ERD_Simplified.md     - System overview
2. ERD_Visual.puml       - Generate presentation slides
3. README_ERD.md         - Share with team
```

---

## 🛠️ Tools Needed

### To View Markdown Files (.md)
- ✅ GitHub (auto-renders)
- ✅ VS Code (with Mermaid extension)
- ✅ Any markdown viewer

### To Render Mermaid Diagrams
- ✅ GitHub (automatic)
- ✅ VS Code extension: `bierner.markdown-mermaid`
- ✅ Mermaid Live: https://mermaid.live/

### To Generate PlantUML Images
- ✅ VS Code extension: `jebbs.plantuml`
- ✅ Command line: `java -jar plantuml.jar`
- ✅ Online: http://www.plantuml.com/plantuml/

### To View ASCII Diagram
- ✅ Any text editor
- ✅ Terminal: `cat ERD_ASCII.txt`
- ✅ Notepad, VS Code, etc.

---

## 💡 Usage Examples

### Scenario 1: Quick Database Reference
**You need**: Quick lookup of table structure
**Use**: [ERD_ASCII.txt](ERD_ASCII.txt) - Open in terminal or text editor

### Scenario 2: Team Presentation
**You need**: Visual diagram for slides
**Use**: [ERD_Visual.puml](ERD_Visual.puml) - Generate PNG/SVG

### Scenario 3: Code Development
**You need**: Understanding relationships while coding
**Use**: [ERD_Diagram.md](ERD_Diagram.md) - Keep open in VS Code

### Scenario 4: Onboarding New Developer
**You need**: Explain system to new team member
**Use**: [ERD_Simplified.md](ERD_Simplified.md) → [ERD_Diagram.md](ERD_Diagram.md)

### Scenario 5: Database Migration
**You need**: Understand current schema before changes
**Use**: [ERD_Diagram.md](ERD_Diagram.md) + `/db/schema_complete.sql`

---

## 📝 File Descriptions

### 1. ERD_Simplified.md
**Size**: Medium  
**Complexity**: ⭐⭐☆☆☆ (Easy)  
**Best For**: Quick overview, management, first-time readers

**Contains**:
- Tree structure of database
- Simple flow diagrams (ASCII)
- Brief table descriptions
- Key relationships summary
- Quick statistics

**When to Use**:
- Need quick understanding
- Explaining to non-technical stakeholders
- First introduction to the system
- Planning discussions

---

### 2. ERD_Diagram.md
**Size**: Large  
**Complexity**: ⭐⭐⭐⭐☆ (Detailed)  
**Best For**: Developers, database admins, technical documentation

**Contains**:
- Complete Mermaid ERD diagram
- Full table definitions with all columns
- All relationships explained
- Foreign key constraints
- ON DELETE behaviors
- Indexes and performance notes
- Security features
- Sample SQL queries
- Views documentation

**When to Use**:
- Developing new features
- Database maintenance
- Understanding complex relationships
- Writing database queries
- Technical documentation

---

### 3. ERD_Visual.puml
**Size**: Medium  
**Complexity**: ⭐⭐⭐☆☆ (Technical)  
**Best For**: Generating visual diagrams, presentations

**Contains**:
- PlantUML source code
- Detailed entity boxes
- All fields with types
- Visual relationships
- Color-coded sections
- Legend and notes

**When to Use**:
- Need PNG/SVG image
- Creating presentation slides
- Printing documentation
- Visual communication
- Architecture diagrams

**How to Use**:
```bash
# Generate PNG
java -jar plantuml.jar ERD_Visual.puml

# Generate SVG
java -jar plantuml.jar -tsvg ERD_Visual.puml
```

---

### 4. ERD_ASCII.txt
**Size**: Large  
**Complexity**: ⭐⭐☆☆☆ (Visual)  
**Best For**: Terminal viewing, quick reference, printing

**Contains**:
- ASCII art diagram
- Box drawings
- Table structures
- Relationships with arrows
- Workflow diagrams
- Cardinality summary
- Foreign key constraints
- Legend

**When to Use**:
- Working in terminal/SSH
- Quick reference while coding
- Print for desk reference
- No GUI available
- Simple text-based view

**How to View**:
```bash
# Terminal
cat ERD_ASCII.txt
less ERD_ASCII.txt

# Windows
type ERD_ASCII.txt
more ERD_ASCII.txt
```

---

### 5. README_ERD.md
**Size**: Large  
**Complexity**: ⭐⭐☆☆☆ (Guide)  
**Best For**: Getting started, learning how to use ERD files

**Contains**:
- Guide to all ERD files
- How to view/render diagrams
- Tool recommendations
- Installation instructions
- FAQ section
- Usage examples
- Tips and tricks

**When to Use**:
- First time using ERD documentation
- Need help viewing diagrams
- Installing tools
- Troubleshooting
- Best practices

---

## 🔍 Common Questions

### Q: Which file should I start with?
**A**: Start with [ERD_Simplified.md](ERD_Simplified.md) for overview, then [ERD_Diagram.md](ERD_Diagram.md) for details.

### Q: Can I view these on GitHub?
**A**: Yes! GitHub auto-renders Markdown files and Mermaid diagrams.

### Q: How do I generate a visual diagram?
**A**: Use [ERD_Visual.puml](ERD_Visual.puml) with PlantUML. See [README_ERD.md](README_ERD.md) for instructions.

### Q: I'm on a terminal with no GUI, what can I use?
**A**: Use [ERD_ASCII.txt](ERD_ASCII.txt) - pure text format.

### Q: Where is the actual database schema?
**A**: Check `/db/schema_complete.sql` for complete SQL schema.

### Q: How do I update ERD when database changes?
**A**: 
1. Update `/db/*.sql` files first
2. Update all ERD documentation files
3. Regenerate visual diagrams
4. Commit all changes together

---

## 📊 Comparison Matrix

| Feature | Simplified.md | Diagram.md | Visual.puml | ASCII.txt | README.md |
|---------|--------------|------------|-------------|-----------|-----------|
| Quick Overview | ✅ Best | ✅ Yes | ❌ No | ✅ Yes | ❌ No |
| Complete Details | ❌ No | ✅ Best | ✅ Yes | ✅ Yes | ❌ No |
| Visual Diagram | ⚠️ ASCII | ✅ Mermaid | ✅ Best | ⚠️ ASCII | ❌ No |
| GitHub Friendly | ✅ Yes | ✅ Yes | ❌ Source | ✅ Yes | ✅ Yes |
| Generate Image | ❌ No | ⚠️ Yes | ✅ Best | ❌ No | ❌ No |
| Terminal View | ✅ Yes | ✅ Yes | ❌ No | ✅ Best | ✅ Yes |
| Printable | ✅ Good | ⚠️ OK | ✅ Best | ✅ Good | ✅ Good |
| For Developers | ⚠️ OK | ✅ Best | ✅ Yes | ✅ Yes | ⚠️ Guide |
| For Managers | ✅ Best | ⚠️ Too much | ✅ Yes | ✅ Yes | ⚠️ Guide |
| For Presentations | ⚠️ OK | ⚠️ OK | ✅ Best | ❌ No | ❌ No |

Legend:
- ✅ Best / Yes
- ⚠️ OK / Partial
- ❌ No / Not suitable

---

## 🎓 Learning Path

### Beginner (Never seen this system)
```
Day 1: Read ERD_Simplified.md
       Understand main entities and flow

Day 2: Read ERD_Diagram.md (first half)
       Learn table structures

Day 3: Read ERD_Diagram.md (second half)
       Understand relationships

Day 4: Generate visual from ERD_Visual.puml
       See the complete picture

Day 5: Start working with actual database
       Refer to ERD_ASCII.txt for quick checks
```

### Intermediate (Familiar with databases)
```
Hour 1: Skim ERD_Simplified.md
        Get system overview

Hour 2: Deep dive ERD_Diagram.md
        Understand all relationships

Hour 3: Review /db/schema_complete.sql
        See actual implementation

Hour 4: Generate ERD_Visual.puml
        For documentation/reference
```

### Advanced (Database expert)
```
30 min: Read ERD_Diagram.md
        Focus on relationships and constraints

15 min: Check /db/schema_complete.sql
        Verify implementation

15 min: Keep ERD_ASCII.txt open
        Quick reference while working
```

---

## 📦 Package Contents

This ERD documentation package includes:

```
docs/
├── ERD_Simplified.md      (📖 Overview & quick reference)
├── ERD_Diagram.md         (📚 Complete documentation)
├── ERD_Visual.puml        (🖼️ Visual diagram source)
├── ERD_ASCII.txt          (📺 Text-based diagram)
├── README_ERD.md          (📋 Usage guide)
└── INDEX.md              (📑 This navigation file)
```

**Total Size**: ~500 KB  
**Format**: Plain text (Markdown, PlantUML, ASCII)  
**Version**: 1.0  
**Created**: 2026-02-03  

---

## 🔄 Update Schedule

**ERD documentation should be updated when**:
- ✅ New tables added
- ✅ Table structure modified
- ✅ Relationships changed
- ✅ Indexes added/removed
- ✅ Major database refactoring

**Update checklist**:
1. ✅ Update `/db/*.sql` files
2. ✅ Update `ERD_Simplified.md`
3. ✅ Update `ERD_Diagram.md`
4. ✅ Update `ERD_Visual.puml`
5. ✅ Update `ERD_ASCII.txt`
6. ✅ Regenerate visual diagrams
7. ✅ Update version history
8. ✅ Commit all changes

---

## 📞 Support & Feedback

**For questions about**:
- Database structure: See [ERD_Diagram.md](ERD_Diagram.md)
- How to use files: See [README_ERD.md](README_ERD.md)
- Technical issues: Check [README_ERD.md#FAQ](README_ERD.md#faq)

---

## 📄 Document Information

**System**: E-Aduan JIM 3.0  
**Database**: sistem_eaduan  
**Version**: 1.0  
**Created**: 2026-02-03  
**Format**: Multi-format ERD documentation  
**Maintained by**: System Administrator  

---

**Last Updated**: 3 February 2026

---

[🔝 Back to Top](#-index---erd-documentation)
