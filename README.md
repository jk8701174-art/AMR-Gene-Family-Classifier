# Explainable AMR Gene Family Classifier

A runnable proof of concept for classifying antimicrobial-resistance (AMR) gene families from nucleotide sequences. It turns each sequence into overlapping k-mers, trains an interpretable multinomial Naive Bayes baseline, evaluates it on a held-out set, and saves a reusable prediction model.

## What it demonstrates

- Bioinformatics: FASTA parsing, sequence-quality checks, and k-mer representation.
- ML: stratified train/test split, cross-validation, macro-F1, and batch inference.
- Research practice: reproducible settings, honest evaluation outputs, and a report template.

## Scientific boundary

The files in `data/demo_*` are synthetic software demonstrations. They prove the pipeline works but are not biological evidence and must never be used as a résumé performance claim. Replace them with curated, licence-compliant data before presenting findings.

This tool classifies the labels used during training. It does not diagnose antimicrobial resistance, identify a clinical organism, or replace alignment-based confirmation and expert review.

## Quick start

Requires Python 3.10+.

```powershell
cd outputs/amr-gene-classifier
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -e .
python -m amr_classifier.train --fasta data/demo_sequences.fasta --labels data/demo_labels.csv --output-dir artifacts/demo
python -m amr_classifier.predict --model artifacts/demo/model.pkl --fasta data/demo_sequences.fasta --output artifacts/demo/predictions.csv
python -m unittest discover -s tests -v
```

Training creates `model.pkl`, `metrics.json`, `held_out_predictions.csv`, and `run_config.json`.

## Use real research data

Obtain data permitted for your use from a curated source such as CARD, NCBI AMRFinderPlus reference data, or an approved institutional dataset. Supply a FASTA with unique IDs and a CSV with `sequence_id,label`. Keep the test set isolated, document data provenance and de-duplication, and compare this baseline against an alignment or profile-HMM approach before making research claims.

## Resume wording after real data collection

> Developed a reproducible Python pipeline to classify curated AMR gene families from nucleotide k-mer features; evaluated an interpretable baseline on a held-out dataset and achieved **[actual macro-F1]**.

> Built a reusable FASTA-to-prediction workflow with sequence validation, cross-validation, model persistence, and per-class error analysis.

Replace the bracketed value only with a result measured on non-synthetic data.
