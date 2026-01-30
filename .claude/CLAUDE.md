# GeoCurator

GitHub Pages site for hosting processed scientific papers with extracted charts and data.

**Repository**: https://github.com/psaboia/geocurator
**Live Site**: https://psaboia.github.io/geocurator/

## Relationship with deepseek-ocr-experiments

This repository receives processed papers from the `deepseek-ocr-experiments` pipeline. The workflow is:

1. Papers are processed in `deepseek-ocr-experiments` using DeepSeek-OCR + Gemini for chart extraction
2. Output is copied to this repository (geocurator) for public viewing via GitHub Pages
3. The `viewer_template.html` from deepseek-ocr-experiments should be kept in sync with viewers here

## Structure

```
geocurator/
├── index.html          # Main page listing all papers
├── papers.json         # Metadata for all papers
├── <PaperName>/        # Each processed paper
│   ├── viewer.html     # Interactive viewer
│   ├── processed_document.json
│   ├── document.md
│   ├── images/
│   └── page_images/
```

## Papers Currently Hosted

- **Mercadier2011** - Origin of uranium deposits revealed by their rare earth element signature
- **S0883292716302670** - Chemical and Sr isotopic characterization of North America uranium ores
- **Lach2013** - In Situ Quantitative Measurement of Rare Earth Elements in Uranium Oxides

## Updating Viewers

When `viewer_template.html` is updated in deepseek-ocr-experiments, manually copy to all papers:

```bash
cp /path/to/deepseek-ocr-experiments/scripts/viewer_template.html Mercadier2011/viewer.html
cp /path/to/deepseek-ocr-experiments/scripts/viewer_template.html S0883292716302670/viewer.html
cp /path/to/deepseek-ocr-experiments/scripts/viewer_template.html Lach2013/viewer.html
```

## Recent Work

- Smart chart extraction (300 DPI render for better quality)
- Viewer fixes: logarithmic scale detection, bounding box positioning, document title display
- Chart data extraction with Gemini and replotting in viewer
