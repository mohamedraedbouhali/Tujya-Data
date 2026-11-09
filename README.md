# Tujya-Data

The datasets for **[Tujya-1](https://github.com/mohamedraedbouhali/Tujya-1)**.

This repository holds only the data, versioned with [DVC](https://dvc.org). The application code (backend, frontend, vision model, RAG agent) and the scripts that build these datasets live in Tujya-1.

## Datasets

| Path | What it is | Tracked by |
|---|---|---|
| `data/tujya/` | Pill ingredients and drug–drug interactions (`pill_ingredients.csv`, `interactions_between_classes.csv`, `interactions_with_any_drug.csv`) | `data/tujya.dvc` |
| `data/tox21/` | Tox21 toxicity data (MoleculeNet copy) | `data/tox21.dvc` |
| `data/parquet/` | Drug synergy tables: drugs, cell lines, expression, synergy pairs, abstracts | `data/parquet.dvc` |
| `data/vision/c3pi/images/` | 4,206 pill photos from the NLM C3PI collection | `images.dvc` |
| `data/vision/c3pi/metadata/` | C3PI image metadata | `metadata.dvc` |
| `data/vision/c3pi/labels/` | Auto-generated labels for the pill images | `dvc.yaml` (`prepare` stage) |
| `data/vision/datasets/` | Pill classification (train/val/test) and detection datasets | `dvc.yaml` (`prepare` stage) |
| `data/rag/raw/`, `data/rag/interim/` | openFDA drug labels and PubMed abstracts | `raw.dvc`, `interim.dvc` |
| `data/rag/corpus/` | RAG corpus: 9,695 chunks from 3,922 documents | `dvc.yaml` (`rag_corpus` stage) |

## Getting the data

```bash
git clone https://github.com/mohamedraedbouhali/Tujya-Data.git
cd Tujya-Data
dvc pull
```

`dvc pull` needs a DVC remote. If none is set up yet, add one first with `dvc remote add -d <name> <url>`.

## Rebuilding derived datasets

The two pipeline stages in `dvc.yaml` (`prepare` and `rag_corpus`) run code from Tujya-1, not from this repository. To rebuild them with `dvc repro`, put this data next to a Tujya-1 checkout.

## Licences

Each source keeps its own licence: C3PI, DDInter, openFDA, PubMed, Tox21, DrugComb, NCI ALMANAC and DepMap. Check the `license` / `source_url` columns in the CSVs and each source's terms before you redistribute anything.
