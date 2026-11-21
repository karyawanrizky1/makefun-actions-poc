# makefun-actions-poc

Bukti konsep: build entry make.fun di GitHub Actions, submit tetap dari VM.

## Desain

- Runner Actions **hanya build**: unduh kit, `makefun init`, jalankan Codex
  (Xingchi `gpt-6.1-sol`), hasilkan repo entry + sesi Codex (rollout).
- Repo + rollout diunggah sebagai artifact. **Check + bundle + submit
  dikerjakan di VM operator**, tempat kredensial akun make.fun berada.
- Satu-satunya secret di repo ini: `XINGCHI_API_KEY` (kunci API Xingchi,
  dipakai bersama semua akun). Tidak ada API key make.fun, keypair, atau
  secret wallet apa pun di sini.
- Init repo memakai `--wallet <alamat wallet akun>` (alamat itu publik):
  anchor drand menamai wallet akun sendiri, jadi cek `repo_owner` lolos
  saat submit tanpa keypair di runner.

## Cara menjalankan

1. Tambahkan secret `XINGCHI_API_KEY` di repo ini:
   Settings > Secrets and variables > Actions > New repository secret.
2. Buka tab Actions > `build-entry-poc` > Run workflow.
3. Unduh artifact `entry-agent94-news-image-20261120` (berisi `repo.tar.gz`,
   `rollout.jsonl`, dan `codex-build.log`).
4. Di VM: ekstrak repo, jalankan `makefun check`, `bundle`, lalu `submit`
   dengan kredensial akun agent-94 (@quiet-owl-40).

## Akun PoC

- Akun: agent-94 Niko Kala, @quiet-owl-40 (0 entry sebelum PoC)
- Kompetisi: `news-image-20261120` (tutup 22 Nov 2026 07:00 WIB)
- Prompt: `prompt-agent94-news-image-20261120.txt`
- Data berita: `news-image-20261120-dense-brief-v3-DATAONLY.md` (repo root)
