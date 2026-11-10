# Myntra Image Downloader

Bulk-downloads high-resolution product images from Myntra product pages and records the image URLs back into a spreadsheet. Built in 2023 for catalogue work, where product images had to be collected for hundreds of SKUs at a time.

## How it works

1. Reads an Excel sheet of products (`Myntra PID.xlsx`).
2. Opens each product page and pulls the product data JSON that Myntra embeds in the page (`window.__myx`), instead of parsing the HTML.
3. Takes every image in the product's media album and requests it at 2000×2000.
4. Saves the images to `images/` as `<PID>_<n>.<ext>`.
5. Writes `results.csv`: the input sheet plus `Image 1`, `Image 2`, … columns holding the image URLs.

## Input

`Myntra PID.xlsx` in the same folder, with these columns:

| PID | Myntra Link |
|---|---|
| 13507600 | https://www.myntra.com/.../13507600/buy |

## Usage

```bash
pip install requests requests-html pandas openpyxl tqdm
python main.py
```

`test.ipynb` is the scratch notebook used to explore the page JSON.

## Notes

- Written against Myntra's 2023 page structure. If Myntra has changed how it embeds product data, the regex in `scraper()` will need updating.
- For personal and educational use. Respect Myntra's terms of use and keep request volumes low.
