# Repositori ini digunakan untuk pembelajaran [langchain](https://langchain.com/) di pusdiklat BPS

## Panduan Setup Project

Panduan ini menyediakan dua metode untuk menyiapkan lingkungan kerja (*development environment*) Anda: menggunakan **uv** (metode modern yang sangat cepat dan direkomendasikan) atau menggunakan **pip** standar.

---

### Langkah Persiapan (Sama untuk Kedua Opsi)

1. **Salin file environment template:**
   Salin file [example.env](file:///home/murphi/Projects/langchain-pusdiklat/example.env) menjadi `.env` di direktori utama project:
   ```bash
   cp example.env .env
   ```

2. **Konfigurasi API Key:**
   Buka file `.env` yang baru dibuat dan isi dengan API Key Anda untuk Google Gemini dan Tavily Search:
   ```env
   GOOGLE_API_KEY = 'isi_api_key_gemini_anda_di_sini'
   TAVILY_API_KEY = 'isi_api_key_tavily_anda_di_sini'
   ```


---

## Daftar Materi Pembelajaran

Repositori ini terdiri dari 5 materi pembelajaran utama berupa Jupyter Notebook:

1. **[1_aplikasi_sederhana.ipynb](file:///home/murphi/Projects/langchain-pusdiklat/1_aplikasi_sederhana.ipynb)** — Membangun aplikasi chat sederhana dengan model Gemini menggunakan LangChain. Mempelajari inisialisasi model, pemanggilan model (`invoke`), membaca metadata respons, konfigurasi parameter model (`temperature`, `max_tokens`), serta menyusun pesan menggunakan `SystemMessage` & `HumanMessage`.
2. **[2_prompting.ipynb](file:///home/murphi/Projects/langchain-pusdiklat/2_prompting.ipynb)** — Teknik rekayasa prompt (*prompt engineering*). Mempelajari manual prompt, penggunaan `PromptTemplate`, `ChatPromptTemplate` (Structured Prompt), dan memaksa output model agar konsisten menggunakan Pydantic (`Structured Output`).
3. **[3_tool.ipynb](file:///home/murphi/Projects/langchain-pusdiklat/3_tool.ipynb)** — Menambahkan kapabilitas eksternal ke dalam model. Mempelajari cara menggunakan pre-built tools (seperti pencarian internet menggunakan Tavily Search) dengan agen LangChain (`create_agent`).
4. **[4_custom_tool.ipynb](file:///home/murphi/Projects/langchain-pusdiklat/4_custom_tool.ipynb)** — Membuat tool kustom buatan sendiri menggunakan decorator `@tool` agar agen dapat memanggil fungsi Python spesifik Anda.
5. **[5_memory.ipynb](file:///home/murphi/Projects/langchain-pusdiklat/5_memory.ipynb)** — Menyimpan riwayat percakapan agar model memiliki ingatan (stateful). Mempelajari cara menggunakan `InMemorySaver` dari LangGraph dan parameter `thread_id`.

---

### Opsi 1: Menggunakan `uv` (Sangat Direkomendasikan)

[uv](https://github.com/astral-sh/uv) adalah manajer paket Python yang sangat cepat dan modern yang ditulis dalam bahasa Rust. Metode ini direkomendasikan karena akan otomatis membuat virtual environment dan menginstal semua dependensi yang tercantum dalam [pyproject.toml](file:///home/murphi/Projects/langchain-pusdiklat/pyproject.toml) dengan sangat cepat dan konsisten menggunakan [uv.lock](file:///home/murphi/Projects/langchain-pusdiklat/uv.lock).

1. **Pastikan `uv` sudah terinstal:**
   Jika belum, Anda bisa menginstalnya melalui perintah berikut:
   * **macOS/Linux:**
     ```bash
     curl -LsSf https://astral.sh/uv/install.sh | sh
     ```
   * **Windows (PowerShell):**
     ```powershell
     powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
     ```
   * Atau via **pip**:
     ```bash
     pip install uv
     ```

2. **Sinkronisasi Dependensi:**
   Cukup jalankan perintah berikut di direktori project:
   ```bash
   uv sync
   ```
   Perintah ini akan secara otomatis:
   * Membuat virtual environment di folder `.venv` (menggunakan Python versi yang sesuai seperti tercantum di [pyproject.toml](file:///home/murphi/Projects/langchain-pusdiklat/pyproject.toml)).
   * Menginstal semua dependensi secara aman dan cepat.

3. **Menjalankan Project:**
   Anda dapat langsung menjalankan JupyterLab di dalam virtual environment menggunakan `uv run`:
   ```bash
   uv run jupyter lab
   ```

---

### Opsi 2: Menggunakan `pip` Standar

Jika Anda lebih memilih menggunakan alat bawaan Python standar (pip dan venv):

1. **Buat Virtual Environment:**
   Buat lingkungan virtual baru (direkomendasikan menggunakan Python 3.12):
   ```bash
   python3 -m venv .venv
   ```

2. **Aktifkan Virtual Environment:**
   * **macOS/Linux:**
     ```bash
     source .venv/bin/activate
     ```
   * **Windows (Command Prompt):**
     ```cmd
     .venv\Scripts\activate.bat
     ```
   * **Windows (PowerShell):**
     ```powershell
     .venv\Scripts\Activate.ps1
     ```

3. **Instal Dependensi:**
   Instal semua paket yang diperlukan melalui file [requirements.txt](file:///home/murphi/Projects/langchain-pusdiklat/requirements.txt):
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. **Menjalankan Project:**
   Pastikan virtual environment Anda tetap aktif, lalu jalankan JupyterLab:
   ```bash
   jupyter lab
   ```

---

## Menjalankan Script Python (`.py`)

Jika Anda ingin menjalankan kode berupa script Python biasa (file `.py`), Anda tidak perlu menjalankan JupyterLab. Cukup jalankan perintah berikut di terminal:

### Opsi 1: Menggunakan `uv`
Jika menggunakan `uv`, Anda tidak perlu mengaktifkan virtual environment secara manual. Cukup gunakan `uv run`:
```bash
uv run nama_script.py
```

### Opsi 2: Menggunakan `pip` (Python Standar)
Jika menggunakan Python standar, pastikan virtual environment Anda sudah aktif terlebih dahulu, kemudian jalankan menggunakan `python`:
```bash
# Aktifkan virtual environment (jika belum)
source .venv/bin/activate  # macOS/Linux
# Atau: .venv\Scripts\Activate.ps1  # Windows PowerShell

# Jalankan script
python nama_script.py
```
