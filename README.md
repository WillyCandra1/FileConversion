# PDFtoJPG

Convert multi-page PDFs into individual **JPG images** or a single **DOCX document** — effortlessly.

Double-click the script to use GUI dialogs, or run it from the command line for full control.

## Features

- **Two output formats** — JPG (one image per page) or DOCX
- **GUI mode** — file picker and format picker dialogs; no terminal needed
- **Batch processing** — convert multiple PDFs in one run
- **DPI & quality control** — configurable resolution (72–600 DPI) and JPG quality (1–100)
- **Page range selection** — convert specific pages instead of the whole document
- **Encrypted PDF support** — supply a password via `--password`
- **CMYK / transparency handling** — flattened to RGB automatically for JPG output
- **Recursive directory scanning** — process all PDFs in a folder tree

## Dependencies

```
pip install PyMuPDF Pillow pdf2docx
```

| Package | Purpose |
|---|---|
| PyMuPDF | PDF rendering and page extraction |
| Pillow | JPG encoding and color space handling |
| pdf2docx | PDF → DOCX conversion |

## Usage

### GUI (double-click)

Run the script with no arguments. A file picker opens first, then a format dialog:

```
python FileConversion.py
```

### Command line

```
python FileConversion.py <input> [options]
```

**Examples**

```bash
# Convert to JPG (default)
python FileConversion.py document.pdf

# Convert to DOCX
python FileConversion.py document.pdf --format docx

# JPG with custom DPI and quality
python FileConversion.py document.pdf -o out/ -d 300 -q 95

# Convert specific pages only
python FileConversion.py document.pdf --pages 1-5

# Batch convert a whole folder
python FileConversion.py pdfs/ --recursive

# Password-protected PDF
python FileConversion.py document.pdf --password secret
```

## Options

| Flag | Default | Description |
|---|---|---|
| `input` | *(file picker)* | PDF file or directory |
| `-f, --format` | `jpg` | Output format: `jpg` or `docx` |
| `-o, --output` | next to PDF | Output directory |
| `-d, --dpi` | `200` | Resolution in DPI (72–600); JPG only |
| `-q, --quality` | `90` | JPG quality (1–100); JPG only |
| `-p, --password` | — | Password for encrypted PDFs |
| `--pages` | all | Page range, e.g. `1-5` or `3` |
| `--recursive` | off | Recurse into subdirectories |
| `--pick-output` | off | Open a folder picker for output |
| `--no-picker` | off | Disable GUI fallback |
| `-v, --verbose` | off | Enable debug logging |

## Output

- **JPG** — saved to `<stem>_images/` next to the PDF, one file per page
- **DOCX** — saved as `<stem>.docx` next to the PDF
