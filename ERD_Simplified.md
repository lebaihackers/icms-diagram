# ERD Diagram Ringkas - Sistem E-Aduan JIM 3.0

## 📊 Gambaran Keseluruhan Database

Sistem ini menggunakan **16 tables** yang dibahagikan kepada 5 kategori utama:

```
📁 SISTEM E-ADUAN DATABASE
│
├── 👥 USER MANAGEMENT (2 tables)
│   ├── pengadu (complainants)
│   └── pentadbir (administrators)
│
├── 📝 COMPLAINT CORE (6 tables)
│   ├── aduan (main complaints table)
│   ├── lampiran (file attachments)
│   ├── video_lampiran (video attachments)
│   ├── komen (comments)
│   ├── aduan_workflow_history (workflow tracking)
│   └── aduan_kembalikan (returned complaints)
│
├── 🔔 NOTIFICATIONS (2 tables)
│   ├── notifikasi_pengadu (for complainants)
│   └── notifikasi_pentadbir (for admins)
│
├── 📚 REFERENCE DATA (2 tables)
│   ├── negeri (states)
│   └── kategori_aduan (categories)
│
└── 🔍 AUDIT & MONITORING (4 tables)
    ├── audit_logs (security audit)
    ├── slow_queries (performance)
    ├── news_updates (announcements)
    └── saved_searches (user preferences)
```

---

## 🔗 Relationship Flow (Simplified)

```
┌─────────────────────────────────────────────────────────────┐
│                    SISTEM E-ADUAN FLOW                       │
└─────────────────────────────────────────────────────────────┘

┌──────────┐                    ┌──────────┐
│ PENGADU  │ ──── membuat ────> │  ADUAN   │
│ (User)   │                    │(Complaint)│
└──────────┘                    └─────┬────┘
     │                                │
     │ tinggal di                     │ berlaku di
     ▼                                ▼
┌──────────┐                    ┌──────────┐
│  NEGERI  │                    │ KATEGORI │
│ (State)  │                    │(Category)│
└──────────┘                    └──────────┘

                            ┌────────────┐
┌──────────────┐            │   ADUAN    │ ◄──── dikendalikan oleh
│  PENTADBIR   │ ───────────│(Complaint) │
│   (Admin)    │  3 roles   └─────┬──────┘
└──────┬───────┘                  │
       │                          │ mempunyai
       │                          ├──► LAMPIRAN (files)
       │                          ├──► VIDEO_LAMPIRAN
       │                          ├──► KOMEN (comments)
       │                          ├──► WORKFLOW_HISTORY
       │                          └──► TINDAKAN_ADUAN
       │
       └─── menerima ────> NOTIFIKASI_PENTADBIR


┌──────────┐                    ┌────────────────┐
│ PENGADU  │ ─── menerima ────> │  NOTIFIKASI_   │
│          │                    │    PENGADU     │
└──────────┘                    └────────────────┘
```

---

## 🎯 Main Entities Explained

### 1️⃣ **PENGADU** (Complainant/Public User)
```
┌────────────────────────────────┐
│         PENGADU                 │
├────────────────────────────────┤
│ • id (PK)                       │
│ • nama_penuh                    │
│ • email (unique)                │
│ • password (hashed)             │
│ • no_telefon                    │
│ • alamat, poskod, daerah        │
│ • negeri_id (FK → negeri)       │
│ • google_id, facebook_id (OAuth)│
│ • foto_profil                   │
│ • status (aktif/tidak_aktif)    │
└────────────────────────────────┘
```
**Purpose**: Store public users who submit complaints

---

### 2️⃣ **PENTADBIR** (Administrator/Officer)
```
┌────────────────────────────────┐
│        PENTADBIR                │
├────────────────────────────────┤
│ • id (PK)                       │
│ • nama_penuh                    │
│ • email (unique)                │
│ • password (hashed)             │
│ • workflow_role:                │
│   - super_admin                 │
│   - pegawai_penerima (HQ)       │
│   - pengarah (HQ)               │
│   - pegawai_negeri (State)      │
│ • negeri_id (FK → negeri)       │
│ • jabatan                       │
│ • status                        │
└────────────────────────────────┘
```
**Purpose**: Store admin users with different roles in workflow

---

### 3️⃣ **ADUAN** (Complaint - Core Table)
```
┌─────────────────────────────────────────┐
│              ADUAN                       │
├─────────────────────────────────────────┤
│ BASIC INFO:                              │
│ • id (PK)                                │
│ • id_pengadu (FK → pengadu)              │
│ • tajuk_aduan                            │
│ • butiran_aduan                          │
│ • jenis_aduan (Aduan/Cadangan/Penghargaan)│
│                                          │
│ CLASSIFICATION:                          │
│ • kategori_aduan_id (FK → kategori)      │
│ • kategori_lain (if "Lain-lain")         │
│                                          │
│ LOCATION:                                │
│ • negeri_id (FK → negeri)                │
│ • daerah, poskod, lokasi                 │
│                                          │
│ PATI SPECIFIC:                           │
│ • anggaran_bilangan_pati                 │
│ • waktu_operasi (dari/hingga)            │
│ • warganegara                            │
│ • jenis_premis                           │
│                                          │
│ WORKFLOW:                                │
│ • workflow_stage (8 stages)              │
│ • status_kelengkapan                     │
│                                          │
│ ASSIGNED OFFICERS:                       │
│ • pegawai_penerima_id (FK → pentadbir)   │
│ • pengarah_id (FK → pentadbir)           │
│ • pegawai_negeri_id (FK → pentadbir)     │
│                                          │
│ TIMESTAMPS:                              │
│ • tarikh_aduan, tarikh_semakan           │
│ • tarikh_agihan, tarikh_selesai          │
└─────────────────────────────────────────┘
```
**Purpose**: Central table storing all complaints with complete lifecycle tracking

---

## 📊 Workflow Stages (ADUAN)

```
┌─────────┐
│  BARU   │ ◄── New complaint submitted
└────┬────┘
     ▼
┌─────────────────────┐
│ SEMAKAN_KELENGKAPAN │ ◄── HQ officer checks completeness
└────┬────────────────┘
     ├──► TIDAK_LENGKAP ──► (returned to pengadu)
     ▼
┌──────────────────┐
│ MENUNGGU_AGIHAN  │ ◄── Waiting assignment to state
└────┬─────────────┘
     ▼
┌─────────────────┐
│ DALAM_TINDAKAN  │ ◄── State officer taking action
└────┬────────────┘
     ▼
┌───────────────────────┐
│ MENUNGGU_PENGESAHAN   │ ◄── Waiting confirmation
└────┬──────────────────┘
     ├──► SELESAI ──► (Completed)
     └──► DITOLAK ──► (Rejected)
```

---

## 🔐 Security & Audit

### AUDIT_LOGS Table
```
Purpose: Track all critical user actions
┌──────────────────────────────────┐
│ • action (login, create, update) │
│ • user_type (pengadu/pentadbir)  │
│ • user_id                         │
│ • ip_address (IPv4/IPv6)          │
│ • user_agent (browser info)       │
│ • details (JSON)                  │
│ • created_at                      │
└──────────────────────────────────┘
```

**Common Actions Tracked**:
- login_success / login_failed
- aduan_created
- aduan_updated
- aduan_deleted
- profile_updated
- password_changed
- etc.

---

## 📁 File Management

### LAMPIRAN (General Attachments)
```
┌─────────────────────────┐
│ • id (PK)                │
│ • aduan_id (FK → aduan)  │
│ • nama_fail              │
│ • fail_path              │
│ • jenis_fail (image/pdf) │
│ • saiz_fail (bytes)      │
│ • tarikh_muat_naik       │
└─────────────────────────┘
```

### VIDEO_LAMPIRAN (Video Attachments)
```
┌─────────────────────────────┐
│ • id (PK)                    │
│ • aduan_id (FK → aduan)      │
│ • nama_fail                  │
│ • fail_path                  │
│ • saiz_fail (bigint)         │
│ • durasi (seconds)           │
│ • dimuat_naik_oleh           │
│   (pengadu/pentadbir)        │
│ • tarikh_muat_naik           │
└─────────────────────────────┘
```

---

## 🔔 Notification System

### For PENGADU
```
NOTIFIKASI_PENGADU
├── Aduan anda telah diterima
├── Aduan anda sedang disemak
├── Aduan anda dikembalikan untuk pembetulan
├── Aduan anda dalam tindakan
└── Aduan anda telah selesai
```

### For PENTADBIR
```
NOTIFIKASI_PENTADBIR
├── Aduan baharu memerlukan semakan (Pegawai Penerima)
├── Aduan memerlukan agihan (Pengarah)
├── Aduan diagihkan kepada anda (Pegawai Negeri)
└── Komen baharu daripada pengadu
```

---

## 📈 Key Statistics

| Metric | Value |
|--------|-------|
| Total Tables | 16 |
| Core Tables | 6 |
| Foreign Keys | 20+ |
| Indexes | 40+ |
| Views | 1 (v_aduan_summary) |
| Stored Procedures | 0 (logic in PHP) |

---

## 🔑 Key Foreign Key Relationships

```sql
-- Pengadu to Aduan (One to Many)
aduan.id_pengadu → pengadu.id (CASCADE)

-- Pentadbir to Aduan (Multiple FKs)
aduan.pegawai_penerima_id → pentadbir.id (SET NULL)
aduan.pengarah_id → pentadbir.id (SET NULL)
aduan.pegawai_negeri_id → pentadbir.id (SET NULL)

-- Aduan to Lampiran (One to Many)
lampiran.aduan_id → aduan.id (CASCADE)
video_lampiran.aduan_id → aduan.id (CASCADE)

-- Aduan to Workflow (One to Many)
aduan_workflow_history.aduan_id → aduan.id (CASCADE)
komen.aduan_id → aduan.id (CASCADE)
tindakan_aduan.aduan_id → aduan.id (CASCADE)

-- Reference Data
aduan.negeri_id → negeri.id (SET NULL)
aduan.kategori_aduan_id → kategori_aduan.id (SET NULL)
pengadu.negeri_id → negeri.id (SET NULL)
pentadbir.negeri_id → negeri.id (SET NULL)
```

**ON DELETE Behaviors**:
- `CASCADE`: Delete related records (lampiran, workflow, etc.)
- `SET NULL`: Keep record but nullify FK (preserve historical data)

---

## 🎨 Database Design Principles

### 1. **Normalization**
- ✅ 3rd Normal Form (3NF)
- ✅ No redundant data
- ✅ Reference tables for lookup data

### 2. **Denormalization (Strategic)**
- ✅ Store officer names in aduan table (performance)
- ✅ Store user names in history tables (audit trail)

### 3. **Data Integrity**
- ✅ Foreign Key constraints
- ✅ ENUM for controlled vocabulary
- ✅ NOT NULL on critical fields

### 4. **Performance Optimization**
- ✅ Indexes on FK columns
- ✅ Indexes on frequently queried columns
- ✅ Composite indexes for common queries

### 5. **Security**
- ✅ Password hashing (bcrypt)
- ✅ Audit logging
- ✅ IP tracking
- ✅ No sensitive data in logs

### 6. **Scalability**
- ✅ InnoDB engine (row-level locking)
- ✅ UTF8MB4 charset (future-proof)
- ✅ Partitioning ready (by date)

---

## 📝 Common Queries

### Get all complaints by user
```sql
SELECT a.*, k.nama as kategori, n.nama as negeri
FROM aduan a
LEFT JOIN kategori_aduan k ON a.kategori_aduan_id = k.id
LEFT JOIN negeri n ON a.negeri_id = n.id
WHERE a.id_pengadu = ?
ORDER BY a.tarikh_aduan DESC;
```

### Get workflow history
```sql
SELECT wh.*, p.nama_penuh as pentadbir
FROM aduan_workflow_history wh
LEFT JOIN pentadbir p ON wh.pentadbir_id = p.id
WHERE wh.aduan_id = ?
ORDER BY wh.tarikh_tindakan DESC;
```

### Get unread notifications
```sql
SELECT *
FROM notifikasi_pengadu
WHERE pengadu_id = ? AND dibaca = 0
ORDER BY tarikh_cipta DESC
LIMIT 10;
```

### Dashboard statistics
```sql
SELECT 
  workflow_stage,
  COUNT(*) as jumlah
FROM aduan
GROUP BY workflow_stage;
```

---

## 🚀 How to Use These ERD Files

### 1. **ERD_Diagram.md** (This file)
- Complete documentation
- Mermaid diagram (renders on GitHub)
- Open in VS Code with Mermaid extension

### 2. **ERD_Visual.puml** (PlantUML)
```bash
# Install PlantUML
# Then generate PNG/SVG:
java -jar plantuml.jar ERD_Visual.puml

# Or use online:
# http://www.plantuml.com/plantuml/uml/
```

### 3. **View Online**
- Mermaid Live: https://mermaid.live/
- PlantUML Online: http://www.plantuml.com/plantuml/

---

## 📌 Summary

✅ **16 tables** covering all aspects of complaint management
✅ **Proper normalization** with reference tables
✅ **Complete workflow tracking** with audit trail
✅ **Notification system** for real-time updates
✅ **Security features** with audit logs
✅ **Optimized performance** with strategic indexes
✅ **Scalable design** ready for growth

**Database Name**: `sistem_eaduan`  
**Character Set**: `utf8mb4_unicode_ci`  
**Engine**: `InnoDB`  
**DBMS**: MariaDB 10.6+ / MySQL 8.0+

---

**Last Updated**: 3 February 2026
