<p align="center">
	<img src="https://github.com/daiquocnguyen/CapsE/blob/master/capse_logo.png">
</p>

# A Capsule Network-based Embedding Model for Knowledge Graph Completion and Search Personalization<a href="https://twitter.com/intent/tweet?text=Wow:&url=https%3A%2F%2Fgithub.com%2Fdaiquocnguyen%2FCapsE%2Fblob%2Fmaster%2FREADME.md"><img alt="Twitter" src="https://img.shields.io/twitter/url?style=social&url=https%3A%2F%2Ftwitter.com%2Fdaiquocng"></a>

<img alt="GitHub top language" src="https://img.shields.io/github/languages/top/daiquocnguyen/CapsE"><img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/daiquocnguyen/CapsE"><img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/daiquocnguyen/CapsE"><a href="https://github.com/daiquocnguyen/CapsE/network"><img alt="GitHub forks" src="https://img.shields.io/github/forks/daiquocnguyen/CapsE"></a><a href="https://github.com/daiquocnguyen/CapsE/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/daiquocnguyen/CapsE"></a><img alt="GitHub" src="https://img.shields.io/github/license/daiquocnguyen/CapsE">

This program provides the implementation of the capsule network-based model CapsE as described in [the paper](https://www.aclweb.org/anthology/N19-1226):

        @InProceedings{Nguyen2019CapsE,
          author={Dai Quoc Nguyen and Thanh Vu and Tu Dinh Nguyen and Dat Quoc Nguyen and Dinh Phung},
          title={{A Capsule Network-based Embedding Model for Knowledge Graph Completion and Search Personalization}},
          booktitle={Proceedings of the 2019 Annual Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies (NAACL-HLT)},
          year={2019},
          pages={2180--2189}
          }

<p align="center"> 
<img src="https://github.com/daiquocnguyen/CapsE/blob/master/CapsE.png">
</p>

## Usage

### Requirements
- Python 3
- Tensorflow >= 1.6

### Training
To run the program:

        $ python CapsE.py --embedding_dim <int> --num_filters <int> --learning_rate <float> --name <dataset_name> [--useConstantInit] --model_name <name_of_saved_model>

**Required parameters:** 

`--embedding_dim`: Dimensionality of entity and relation embeddings.  

`--num_filters`: Number of filters.

`--learning_rate`: Initial learning rate.

`--name`: Dataset name (WN18RR or FB15k-237).

`--useConstantInit`: Initialize filters by [0.1, 0.1, -0.1]. Otherwise, initialize filters by a truncated normal distribution.

`--model_name`: Name of saved models.

`--num_epochs`: Number of training epochs.

`--vec_len_secondCaps`: Number of neurons within the capsule in the second layer (Default: 10).

`--run_folder`: Specify directory path to save trained models.

`--batch_size`: Batch size.

To train a CapsE model to reproduce the experimental results published in the paper:      
                
        $ python CapsE.py --embedding_dim 100 --num_epochs 31 --num_filters 50 --learning_rate 0.0001 --name FB15k-237 --useConstantInit --savedEpochs 30 --model_name fb15k237
        
        $ python CapsE.py --embedding_dim 100 --num_epochs 31 --num_filters 400 --learning_rate 0.00001 --name WN18RR --savedEpochs 30 --model_name wn18rr
        
### Evaluation metrics

File `evalCapsE.py` provides ranking-based scores as evaluation metrics, including mean rank (MR), mean reciprocal rank (MRR), Hits@1 and Hits@10 in a setting protocol "Filtered".

See examples in `command.sh`. Depending on the memory resources, you should change the values of `--num_splits` to a suitable value to get a faster process. To get the results (supposing `num_splits = 8`):
        
        $ python evalCapsE.py --embedding_dim 100 --num_filters 50 --name FB15k-237 --useConstantInit --model_index 30 --model_name fb15k237 --num_splits 8 --decode
        
        $ python evalCapsE.py --embedding_dim 100 --num_filters 400 --name WN18RR --model_index 30 --model_name wn18rr --num_splits 8 --decode
   
### Note SEARCH17

As in an agreement, you "MUST" cite the paper [Search Personalization with Embeddings](https://arxiv.org/abs/1612.03597) whenever SEARCH17 is used to produce your published results. Unzip doc2vec.200.zip in the data/SEARCH17 folder. 

At the moment, I cannot release the text because of the privacy issues.
         
## License

Please cite the paper whenever CapsE is used to produce published results or incorporated into other software. As a free open-source implementation, CapsE is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. All other warranties including, but not limited to, merchantability and fitness for purpose, whether express, implied, or arising by operation of law, course of dealing, or trade usage are hereby disclaimed. I believe that the programs compute what I claim they compute, but I do not guarantee this. The programs may be poorly and inconsistently documented and may contain undocumented components, features or modifications. I make no guarantee that these programs will be suitable for any application.

CapsE is  is licensed under the Apache License 2.0. 

## Acknowledgments     

I would like to thank Huadong Liao naturomics for implementing the CapsNet(Capsules Net) in Hinton's paper Dynamic Routing Between Capsules.
