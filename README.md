# FlyRank ML Internship — Content Opportunity Scoring Capstone

Refresh / Content Opportunity Scoring (GSC search performance sub-lane).

## Repo structure

```
work/notebooks/          weekly assignment notebooks + capstone.ipynb
docs/index.html          deployed capstone research paper (GitHub Pages source)
submission/paper_url.txt deployed paper's direct URL (single line)
```

Drop your existing Week 1–4 notebooks into `work/notebooks/` alongside
`capstone.ipynb` if they aren't there already — this repo currently ships the
capstone notebook only, since that is what this task built end to end.

## Deployment (GitHub Pages)

This repo is set up to serve the paper straight from `/docs` on `main`:

1. Push this repo content to `main` on `github.com/zaidbinnaveed/FlyRank-ML-Internship`.
2. Settings → Pages → Source: **Deploy from a branch** → Branch: `main`, Folder: `/docs`.
3. Save. The paper goes live at:
   `https://zaidbinnaveed.github.io/FlyRank-ML-Internship/`

That URL is also recorded in `submission/paper_url.txt`.

## Data access

The capstone notebook reads directly from the gated Hugging Face dataset
`FlyRank/internship-warehouse`. Running it requires a Hugging Face account
with read access to that dataset and an active login
(`huggingface-cli login` or an `HF_TOKEN` environment variable) before
launching Jupyter.
