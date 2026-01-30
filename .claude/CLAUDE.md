# GeoCurator

GitHub Pages site for hosting processed scientific papers with extracted charts and data.

**Repository**: https://github.com/psaboia/geocurator
**Live Site**: https://psaboia.github.io/geocurator/

## Relationship with deepseek-ocr-experiments

This repository receives processed papers from the `deepseek-ocr-experiments` pipeline:
- Path: `/mnt/slow_data/TAI/Users/pmoreira/deepseek-ocr-experiments`
- The `viewer_template.html` from there should be kept in sync with viewers here

## Structure

```
geocurator/
├── index.html          # Main page listing all papers
├── papers.json         # Metadata for all papers
├── <PaperName>/        # Each processed paper
│   ├── viewer.html     # Interactive viewer (has commit hash comment)
│   ├── processed_document.json
│   ├── document.md
│   ├── comparison.html # Chart comparison page (optional)
│   ├── images/
│   └── page_images/
```

## Papers Currently Hosted

- **Mercadier2011** - Origin of uranium deposits revealed by their rare earth element signature
- **S0883292716302670** - Chemical and Sr isotopic characterization of North America uranium ores
- **Lach2013** - In Situ Quantitative Measurement of Rare Earth Elements in Uranium Oxides

## Current State (2026-01-30)

- All viewers updated with latest fixes (commit e7cac1f)
- Mercadier2011 has chart data extracted with smart extraction
- **comparison.html** added to ALL papers for visual chart validation:
  - https://psaboia.github.io/geocurator/Mercadier2011/comparison.html
  - https://psaboia.github.io/geocurator/S0883292716302670/comparison.html
  - https://psaboia.github.io/geocurator/Lach2013/comparison.html

## Comparison Pages

Each paper has `comparison.html` that shows side-by-side:
- **Left**: Original chart image from PDF
- **Right**: Replotted chart from extracted data
- **Below**: Raw JSON data (expandable)

Files needed for comparison:
- `comparison.html` - The comparison page (same for all papers)
- `charts_comparison_data.json` - Extracted chart data for that paper

## Updating Viewers

Each viewer.html has a comment with source commit hash for traceability:
```html
<!-- viewer_template.html from deepseek-ocr-experiments commit: e7cac1f (2026-01-30 01:17:53 UTC) -->
```

Update process:
```bash
cd /mnt/slow_data/TAI/Users/pmoreira/deepseek-ocr-experiments
HASH=$(git log --oneline -1 scripts/viewer_template.html | cut -d' ' -f1)

cd /mnt/slow_data/TAI/Users/pmoreira/geocurator
for paper in Mercadier2011 S0883292716302670 Lach2013; do
    cp /mnt/slow_data/TAI/Users/pmoreira/deepseek-ocr-experiments/scripts/viewer_template.html "$paper/viewer.html"
    sed -i "s|<!DOCTYPE html>|<!DOCTYPE html>\n<!-- viewer_template.html from deepseek-ocr-experiments commit: $HASH ($(date -u +\"%Y-%m-%d %H:%M:%S UTC\")) -->|" "$paper/viewer.html"
done
git add -A && git commit -m "Update viewers from commit $HASH" && git push
```

## Pending Tasks

1. Re-process S0883292716302670 and Lach2013 with smart chart extraction
2. Update papers.json with accurate chart counts after re-processing
