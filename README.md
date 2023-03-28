<h1 align="center">NeuCLIR22 mT5</h1>
<div align="center">
  This repository includes the winning reranker model used to reproduce NeuCLIR 2022.
</div>

## Requirements

If you plan to run the model with weights in 8-bit (int8), you will need at least 40GB of GPU RAM. For 16-bit (fp16), you will need 80GB.

## Installation

To install the necessary packages, use the pip package manager to install InPars toolkit, jsonlines reader, and ir-measures:

```bash
pip install inpars jsonlines ir-measures
```

If you want to use int8 for inference, install the bitsandbytes library. Refer to their [installation documentation](https://github.com/TimDettmers/bitsandbytes#requirements--installation) for more information.

```bash
pip install bitsandbytes
```

## Usage

Clone this repository: 
```bash
git clone https://github.com/vjeronymo2/neuCLIR2022-mT5.git
```

On root directory, copy the `docs.jsonl` from each language to the approriate empty directories (`./fa`, `./ru`, and `./zh`)

Open `make_corpus&queries.ipynb` notebook and run all cells to generate the corpus and topics for each language.

For a given run (e.g. `runs/run.organizers.fa.txt`) you wish to rerank, use the following command from InPars

```bash
python -m inpars.rerank \
        --model="unicamp-dl/mt5-13b-mmarco-100k" \
        --corpus="fa/docs_parsed.jsonl" \
        --queries="fa/topics/topics_mt_desc_title.tsv" \
        --input_run="runs/run.organizers.fa.txt" \
        --output_run="runs/run.organizers.mt5_mt_desc_title.txt"
```

To inference with either fp16 or int8, pass their arguments along.
```bash
        --fp16 \
        --int8 \
```

For metrics, you can use the ir_measures library:
```bash
ir_measures qrels_modified.fa \
        runs/run.organizers.mt5_mt_desc_title.txt \
        'nDCG@10 nDCG@20 MAP RBP(rel=1) R@100 R@1000 Judged@10 Judged@20'
```

## Cite this work

Please cite the original [NeuCLIR paper published at TREC](https://trec.nist.gov/pubs/trec31/papers/NM.unicamp.N.pdf) if you use this repository.

```
Soon
```

