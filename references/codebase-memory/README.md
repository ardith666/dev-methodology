# Codebase Memory MCP Integration Module

Modul referensi untuk AI agent dan pengguna yang memakai `dev-methodology`. **Aktif** saat `codebase-memory-mcp` (CBM) terpasang di sistem atau MCP server-nya terdaftar di agent.

Dibuat oleh [DeusData](https://github.com/DeusData/codebase-memory-mcp) (MIT License). Native C11, background coordination daemon, persistent SQLite knowledge graph, 0 external API key needed.

---

## 1. Kenapa CBM Menghemat Token?

Berdasarkan evaluasi terhadap 31 repository nyata (preprint Maret 2026): **10× lebih hemat token** dan **2.1× lebih sedikit tool calls** dibanding pembacaan file-by-file biasa (`read_file` / `cat` / `grep` mentah).

1. **Targeted Query vs File Dump**: Alih-alih membaca file 500-1000 baris untuk mencari satu fungsi, agent hanya menarik simbol yang relevan via `get_code_snippet` atau menelusuri pemanggil via `trace_path`.
2. **Compact Tree Format & Semantic Truncation**: Respons paged dan dipadatkan dengan prefix-directory references (`@0+filename`), memotong token overhead hingga >15% sebelum masuk context window.
3. **Blast Radius Presisi**: `detect_changes` langsung memetakan git diff ke fungsi/simbol terdampak tanpa perlu grep menyeluruh ke seluruh repo.

---

## 2. Perbedaan Peran: CBM vs Graphify

| Aspek | Codebase Memory MCP (CBM) | Graphify |
|---|---|---|
| **Core Engine** | Native C11, SQLite, Tree-sitter, Hybrid LSP | Python, Tree-sitter AST, NetworkX |
| **Operasi** | Background daemon + MCP tools real-time | CLI on-demand (`extract`, `query`, `explain`) |
| **Fokus Utama** | Surgical discovery, snippet extraction, blast radius, hemat token saat eksekusi task | Visualisasi arsitektur (HTML), Wiki Obsidian, `GRAPH_REPORT.md`, community clustering |
| **Tipe Pengetahuan** | Real-time code structure, caller-callee, type-binding, infra trace (Docker, K8s, Terraform) | Visual semantic graph, God nodes, bridging concepts, multi-repo merge |
| **Lokasi Data** | Cache internal `~/.cache/codebase-memory-mcp/` (atau `.codebase-memory/` jika di-share) | Folder `graphify-out/` di root repo |
| **Use Case dev-meth** | Phase 1 (orient), Phase 2 (spec evidence), Phase 4 (surgical read), Phase 5 (targeted tests) | Phase 1 (arsitektur besar), Phase 2 (domain map), Phase 6 (wiki / report retention) |

*Aturan di dev-meth:* CBM dipakai agent saat bekerja mencari dan mengedit kode (efisiensi token); Graphify dipakai saat kamu/agent butuh peta visual dan rangkuman arsitektur yang disimpan ke `knowledge/`.

---

## 3. Daftar 17 MCP Tools & Fungsinya

### A. Indexing & Manajemen Project
| Tool | Fungsi | Contoh Parameter |
|---|---|---|
| `index_repository` | Mengindeks repo ke graph SQLite lokal. Mendukung mode `async: true` untuk repo raksasa | `repo_path: "/abs/path"`, `mode: "full"`, `async: false` |
| `list_projects` | Menampilkan daftar repo yang sudah diindeks beserta statistik node/edge | `detail: "stats"`, `limit: 20` |
| `index_status` | Mengecek status kesegaran index dan status background watcher | `project: "my-project"`, `verbose: true` |
| `check_index_coverage` | Mengecek apakah path file tertentu sudah terindeks penuh atau ada bagian yang terlewat | `paths: ["src/auth.ts"]` |
| `delete_project` | Menghapus index suatu project dari database lokal | `project: "my-project"` |

### B. Pencarian & Navigasi Simbol
| Tool | Fungsi | Contoh Parameter |
|---|---|---|
| `search_graph` | Pencarian struktural, BM25 text, dan semantic vector search (Nomic int8 embed) | `name_pattern: ".*Order.*"`, `label: "Function"`, `semantic_query: "jwt auth"` |
| `get_code_snippet` | Mengambil implementasi fungsi/class tertentu saja (tanpa baca 1 file penuh) | `qualified_name: "src/auth.verifyToken"` |
| `get_file_outline` | Mengambil daftar deklarasi fungsi/class dalam satu file sesuai urutan baris | `file_path: "src/auth.ts"` |
| `search_code` | Grep terindeks cepat dengan perankingan graph | `pattern: "processPayment"` |
| `get_graph_schema` | Melihat relasi, node label, dan statistik struktur graph database | *(tanpa parameter)* |

### C. Analisis Relasi & Arsitektur
| Tool | Fungsi | Contoh Parameter |
|---|---|---|
| `trace_path` | Menelusuri jalur pemanggil (inbound/outbound), data flow, cross-service, atau infra | `function_name: "getUser"`, `direction: "inbound"`, `mode: "calls"` |
| `get_architecture` | Ringkasan arsitektur tingkat tinggi: bahasa, route REST, hotspot, clustering | `project: "my-project"`, `aspects: ["routes", "hotspots"]` |
| `query_graph` | Menjalankan query Cypher langsung ke knowledge graph | `query: "MATCH (f:Function)-[:CALLS]->(g) RETURN f.name, g.name LIMIT 10"` |
| `compare_graphs` | Membandingkan snapshot index lama vs baru (melihat delta node & relasi) | `base_snapshot: "v1"`, `target_snapshot: "v2"` |

### D. Perubahan, Dampak, & Keputusan
| Tool | Fungsi | Contoh Parameter |
|---|---|---|
| `detect_changes` | Memetakan uncommitted git diff ke simbol yang terdampak (blast radius) dan test relevan | `scope: "symbols"`, `scope: "tests"` |
| `manage_adr` | CRUD Architecture Decision Records yang tersimpan langsung di graph | `mode: "get"`, `mode: "set_sections"`, `sections: {...}` |
| `ingest_traces` | Memasukkan runtime call traces nyata untuk melengkapi static call graph | `run_label: "staging-run"`, `traces: [...]` |

---

## 4. Opsi Perintah CLI (Penggunaan Mandiri / Terminal)

Selain sebagai MCP server untuk agent, CBM menyediakan CLI mandiri:

```bash
# 1. Indeks repository saat ini
codebase-memory-mcp cli index_repository --repo-path .

# 2. Cek daftar project yang terindeks
codebase-memory-mcp cli list_projects --detail stats

# 3. Cari fungsi berdasarkan regex pattern
codebase-memory-mcp cli search_graph --project my-app --name-pattern '.*Handler.*' --label Function

# 4. Telusuri siapa yang memanggil suatu fungsi
codebase-memory-mcp cli trace_path --project my-app --function-name loginUser --direction inbound

# 5. Baca hanya snippet fungsi tertentu
codebase-memory-mcp cli get_code_snippet --project my-app --qualified-name 'src/auth.loginUser'

# 6. Cek efek perubahan uncommitted git diff terhadap kode & test
codebase-memory-mcp cli detect_changes --project my-app --scope tests

# 7. Buka CBM Lens UI di browser (Visual 3D & Source Reader)
codebase-memory-mcp daemon start --open --port=9749
```

---

## 5. Aturan Pakai di Dev-Methodology

### Aturan Aktivasi (Triviality & Need Gate)
1. **Task Trivial (<10 baris, perbaikan typo/bug jelas):** Lewati CBM & Graphify. Langsung lakukan surgical edit (Ponytail ladder).
2. **Task Non-Trivial (fitur baru, refactor, pelacakan bug lintas file):**
   - Jika CBM terpasang: **Wajib gunakan CBM terlebih dahulu** sebelum menggunakan `grep` atau membaca file penuh.
   - Urutan penelusuran:
     `search_graph` → `trace_path` → `get_code_snippet` → `detect_changes` → baru `grep`/`read` file mentah jika data non-kode.

### Aturan Penyimpanan Output
- Database internal CBM berada di `~/.cache/codebase-memory-mcp/` (tidak mengotori workspace).
- Jika agent menghasilkan laporan arsitektur, ringkasan ADR, atau catatan eksplorasi dari CBM: **WAJIB ditulis ke dalam folder `knowledge/`** (contoh: `knowledge/architecture-cbm.md` atau update `knowledge/KNOWLEDGE.md`).
- Dilarang membuat folder baru di root di luar `knowledge/` kecuali file konfigurasi opsional `.codebase-memory/` jika kamu ingin commit graph snapshot untuk tim.

---

## 6. Hook per Phase di Dev-Methodology

- **Phase 1: Understand**
  - Cek `list_projects` / `index_status`. Jika repo belum diindeks, jalankan `index_repository`.
  - Panggil `get_architecture` untuk mendapatkan daftar REST route, hotspot file, dan modul tanpa menghabiskan ratusan token untuk membaca direktori manual.
- **Phase 2: Spec**
  - Kumpulkan evidence relasi antar-komponen via `trace_path(mode="calls")` atau `trace_path(mode="cross_service")`.
  - Pastikan batas sistem (trust boundaries) terlihat jelas dari jalur panggilan yang dihasilkan graph.
- **Phase 4: Implement (Ponytail Mode & Karpathy Surgical Changes)**
  - **Surgical Reading**: Jangan panggil tool `read` untuk membaca 400 baris file jika hanya butuh 1 fungsi! Panggil `get_code_snippet(qualified_name="...")`.
  - Gunakan `get_file_outline` untuk melihat struktur file sebelum memutuskan membaca isinya.
- **Phase 5: Test & Verify**
  - Jalankan `detect_changes(scope="symbols")` untuk mengetahui simbol apa saja yang terdampak perubahan kode.
  - Jalankan `detect_changes(scope="tests")` untuk menentukan test suite mana yang wajib dijalankan sesuai blast radius.

---

## 7. Panduan Instalasi (Self-Healing)

Cek ketersediaan di terminal:
```bash
which codebase-memory-mcp
```

Jika belum terpasang:
```bash
# macOS / Linux
curl -fsSL https://raw.githubusercontent.com/DeusData/codebase-memory-mcp/main/install.sh | bash

# Windows (PowerShell)
Invoke-WebRequest -Uri https://raw.githubusercontent.com/DeusData/codebase-memory-mcp/main/install.ps1 -OutFile install.ps1
Unblock-File .\install.ps1
.\install.ps1
```

Installer otomatis mengonfigurasi MCP server di client aktif (Claude Code, OpenCode, Codex, Cursor, Gemini CLI, Zed, dll.). Setelah dipasang, restart agent.
