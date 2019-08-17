# uRank_uMart
WSDM 2020 submission

## Convert learning-to-rank datasets to tfrecords
Set up environment variables `RAW_RANK_DATA` and `TF_RANK_DATA`, which correspond to the path for your learning-to-rank datasets (e.g., `absolute-path-to/learning_to_rank_data_sets_OHSUMED`) and the path for your folder to store converted tfrecords. Please check `src/prepare_data.py` for details.

```bash
cd src
python prepare_data.py
```

## Training
```bash
cd src
python main.py
```
## Test
```bash
cd src
python evaluate.py
```

## Hyper-parameters
`experiments/base_model/params.json`

When `num_learners` is larger than 1, uRank becomes uBoost. `pooling` amd `rnn` are used for urBoost only.


## Five-fold cross-validation
This is an example for running uRank or uBoost using a GPU. By using this script, the NDCG and ERR results for the test datasets will be calculated and saved into file `OHSUMED_uRank.txt`.
```bash
cd src
./run_OHSUMED_uRank.sh
```
If you want to obtain the raw prediction scores and calculate the NDCG and ERR metrics separately, set `save_predictions` to true, then you obtain two files `prediction_output` and `label_output` and use the perl script `src/mslr-eval-score-mslr.pl`. (Note that Tensorflow can shuffle the order of candidate documents in each batch/query, therefore, the shuffled `label_output` is also saved in this case.)


## Notice
This repo will be read-only until the end of the review period. Test cases and the rest of scripts will be released after the review period. Please feel free to reach out if you have any questions.
