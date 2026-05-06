# Municipal Gazettes — PT-BR Corpus

Cleaned PT-BR text corpus extracted from Brazilian municipal official gazettes (*Diários Oficiais dos Municípios*) of two development territories in Piauí state: Serra da Capivara and Vale do Canindé.

Produced by [corpus-prep](https://github.com/heitor-am/corpus-prep) and consumed by training notebooks in this repo.

## Contents

| Source | Documents |
|---|---|
| Serra da Capivara | 243 |
| Vale do Canindé | 23 |
| **Total** | **266** |

- **Total characters:** 2,473,647
- **Shards:** 3 (max 100 docs per shard)
- **Format:** Apache Parquet (zstd)

## Schema

| Field | Type | Description |
|---|---|---|
| `id` | string | UUID assigned at ingestion |
| `text` | string | Cleaned plain text |
| `source_path` | string | Original file path |
| `mime` | string | Detected MIME type (Magika) |
| `parser` | string | Parser used (`pymupdf4llm`, `docling`, etc.) |
| `extracted_at` | timestamp | Extraction time (UTC) |
| `char_count` | int64 | Length in characters |
| `language` | string | ISO 639-3 + script (e.g. `por_Latn`) |
| `language_confidence` | float | GlotLID v3 confidence score |
| `sha256` | string | Hash of raw text (binary dedup key) |
| `metadata` | struct | Parser-specific extras (page count, etc.) |

## Generation Parameters

Generated with corpus-prep on 2026-05-04. Key config:

- **Pre-dedup:** SHA-256 exact match
- **Post-dedup:** MinHash LSH (threshold 0.8, 128 permutations, 5-gram)
- **Quality filter:** disabled for this run (raw extraction)
- **Max documents per shard:** 100
- **Output codec:** Parquet + zstd

Full manifest with shard hashes available in `manifest.json`.

## Source

Raw PDFs of municipal gazettes scraped from `diarioficialdosmunicipios.org` covering 2025 publications across the following municipalities:

- **Serra da Capivara territory:** Coronel José Dias, João Costa, São Raimundo Nonato, others
- **Vale do Canindé territory:** subset of municipalities in the territory

Raw PDFs are not redistributed in this repo — only the cleaned text corpus.

## Loading

```python
import pyarrow.parquet as pq
from pathlib import Path

shards = sorted(Path("data/municipal-gazettes").glob("shard-*.parquet"))
table = pq.ParquetDataset([str(s) for s in shards]).read()
df = table.to_pandas()
texts = df["text"].tolist()
```
