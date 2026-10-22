# Codebase Memory MCP Integration Module

Modul referensi untuk AI agent yang memakai `dev-methodology`. **Aktif** saat `codebase-memory-mcp` (CBM) terpasang di sistem atau MCP server-nya terdaftar di agent.

Dibuat oleh [DeusData](https://github.com/DeusData/codebase-memory-mcp) (MIT License). Native C, standalone daemon, persistent SQLite knowledge graph, 0 external API key needed.

## Kenapa CBM Menghemat Token?

Hasil evaluasi 31 repository nyata (Maret 2026): **10× lebih hemat token** dan **2.1× lebih sedikit tool calls** dibanding pembacaan file-by-file biasa (`read_file` / `cat` / `grep` mentah).

1. **Targeted query vs File dump**: Alih-alih membaca ratusan baris file utuh, agent hanya menarik simbol yang relevan (`get_code_snippet`) atau jejak pemanggil (`trace_path`).
2. **Compact tree format & Semantic truncation**: Respons paged, terstruktur, dan memiliki rasio token tinggi tanpa sampah teks berulang.
3. **Blast radius presisi**: `detect_changes` langsung memetakan git diff ke fungsi/simbol terdampak tanpa perlu grep menyeluruh ke seluruh repo.

## Perbedaan Peran: CBM vs Graphify

| Aspek | Codebase Memory MCP (CBM) | Graphify |
|---|---|---|
| **Core Engine** | Native C (C11), SQLite, tree-sitter, Hybrid LSP | Python, tree-sitter AST, networkx |
| **Operasi** | Persistent background daemon + MCP tools real-time | CLI on-demand (`extract`, `query`, `explain`) |
| **Fokus Utama** | Surgical discovery, snippet extraction, blast radius, token efficiency saat implementasi | Visualisasi arsitektur (HTML), Wiki Obsidian, `GRAPH_REPORT.md`, community discovery |
| **MCP Tools** | 17 tools aktif (`search_graph`, `trace_path`, `detect_changes`, dll.) | stdio server (`graphify.serve`) |
| **Use case dev-meth** | Phase 1 (orient), Phase 2 (spec evidence), Phase 4 (surgical read), Phase 5 (targeted tests) | Phase 1 (arsitektur besar), Phase 2 (domain map), Phase 6 (wiki / report retention) |

*Keduanya saling melengkapi:* Gunakan CBM untuk efisiensi token real-time saat membaca/mengubah kode; gunakan Graphify untuk visualisasi graph interaktif dan rangkuman komunitas ke `knowledge/`.

## Priority Order Pencarian Kode (CBM Active)

Jika CBM tersedia di environment atau client MCP:
1. `search_graph` — cari fungsi, class, route, struct berdasarkan pattern nama/label
2. `trace_path` — telusuri caller (inbound) atau callee (outbound)
3. `get_code_snippet` — baca hanya implementasi fungsi/class terkait (jangan `read` satu file penuh jika hanya butuh 1 fungsi!)
4. `detect_changes` — cek blast radius simbol dari uncommitted git diff
5. `check_index_coverage` — verifikasi apakah file/scope sudah masuk graph
6. **Fallback ke grep/glob/read**: hanya untuk string literal, pesan error, konfigurasi mentah, atau file non-kode yang belum terindeks

## Hook per Phase di Dev-Methodology

- **Phase 1 (Understand)**:
  - Cek project terdaftar: `codebase-memory-mcp cli list_projects` atau panggil `list_projects` / `index_status`.
  - Jika belum diindeks: tawarkan `index_repository(repo_path=".")`.
  - Gunakan `get_architecture` untuk melihat modul, cluster, dan REST route dalam hitungan token minimal.
- **Phase 2 (Spec & Evidence)**:
  - Gunakan `trace_path` mode `calls` atau `data_flow` untuk mengumpulkan evidence relasi antar modul tanpa membaca semua file terkait.
  - Untuk endpoint/service: gunakan `trace_path` mode `cross_service` / `topology`.
- **Phase 4 (Implement - Ponytail Mode & Step 4)**:
  - **Surgical reading**: Panggil `get_code_snippet(qualified_name="...")` untuk membaca fungsi target. Hindari membaca 500 baris file kalau hanya mengedit 1 fungsi 20 baris.
  - Saat butuh referensi file: `get_file_outline` untuk melihat struktur deklarasi file sebelum memutuskan membaca isinya.
- **Phase 5 (Test & Verify)**:
  - Jalankan `detect_changes(scope="symbols")` untuk mengetahui simbol apa saja yang terdampak perubahan git saat ini.
  - Jalankan `detect_changes(scope="tests")` untuk mengetahui test yang wajib dijalankan sesuai blast radius perubahan.

## Dependensi & Instalasi

Kebijakan: capability belum ada → **tanya user dulu → bantu deploy → verify.**

### 1. Cek Ketersediaan

```bash
which codebase-memory-mcp
```

### 2. Panduan Instalasi CBM

**macOS / Linux:**
```bash
curl -fsSL https://raw.githubusercontent.com/DeusData/codebase-memory-mcp/main/install.sh | bash
```

Installer otomatis mendeteksi client aktif (Claude Code, OpenCode, Codex, Gemini CLI, Cursor, Zed, dll.) dan memasang config MCP, instructions, serta skill.

**Verifikasi:**
```bash
codebase-memory-mcp --version
codebase-memory-mcp cli list_projects
```

Jika belum terpasang atau gagal di-setup: agent bekerja menggunakan file ops standar (grep/glob/read) atau Graphify, dan mencatat `PENDING: codebase-memory-mcp tidak aktif` di report jika relevan.
