# PDFMathTranslate: PDF Scientific Paper Translation with Layout Preservation

## Introduction
[PDFMathTranslate](https://github.com/PDFMathTranslate/PDFMathTranslate) is an open-source tool designed for translating PDF documents—especially scientific papers with complex mathematical formulas—while keeping formatting and layouts fully intact. It supports bilingual (dual-language) PDF generation.

## Installation
### Via PyPI
```bash
pip install pdfmathtranslate
```

## Usage
### 1. Command Line Interface (CLI)
Translate a PDF file using the default translator:
```bash
pdfatrans -i input.pdf -o output.pdf
```

Generate a bilingual (dual-language) translation:
```bash
pdfatrans -i input.pdf -o output.pdf -b
```

### 2. GUI / Web Interface
Start the local interactive Web UI:
```bash
pdfatrans_gui
```

## Key Features
- **Formula Preservation**: Automatically detects and preserves LaTeX mathematical formulas and symbols during translation.
- **Layout Preservation**: Maintains the original document's structure, fonts, columns, and image alignments.
- **Bilingual Output**: Generates PDF documents containing both the original and translated text side-by-side or line-by-line.
- **Multiple Translation Engines**: Supports translation via Google Translate, DeepL, OpenAI (GPT-3.5/4), Gemini, and others.

---
*Source: [PDFMathTranslate/PDFMathTranslate](https://github.com/PDFMathTranslate/PDFMathTranslate)*
