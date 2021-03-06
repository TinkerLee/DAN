# Deep Adaptation Network (DAN)

This is a caffe repository for deep adaptation network (DAN). We fork the repository with version ID `29cdee7` from [Caffe](https://github.com/BVLC/caffe) and make our modifications. The main modifications are listed as follow:

- Add `mmd layer` described in paper "Learning Transferable Features with Deep Adaptation Networks".
- Emit `SOLVER_ITER_CHANGE` message in `solver.cpp` when `iter_` changes.

The value of the mmd loss could be *negative* since we used the *linear-time unbiased estimate* of the mmd, which lends us an O(n) time cost but may cause negative mmd values for some mini-batch. This negative mmd value however will not influence the final classification performance. Please refer to our paper for the technical details.

If you have any problem about this code, feel free to concact us with the following email:
- zhuhan10@gmail.com
- caozhangjie14@gmail.com
- longmingsheng@gmail.com


Change Note
---------------
We have moved the implementations of Residual Transfer Network (NIPS '16) and Joint Adaptation Network (ICML '17) to the [Xlearn](https://github.com/thuml/Xlearn) library, which is our actively-maintained library for deep transfer learning.

Data Preparation
---------------
In `data/office/*.txt`, we give the lists of three domains in [Office](https://cs.stanford.edu/~jhoffman/domainadapt/#datasets_code) dataset.

Training Model
---------------

In `models/DAN/amazon_to_webcam`, we give an example model based on Alexnet to show how to transfer from `amazon` to `webcam`. In this model, we insert mmd layers after fc7 and fc8 individually.

The [bvlc\_reference\_caffenet](http://dl.caffe.berkeleyvision.org/bvlc_reference_caffenet.caffemodel) is used as the pre-trained model. If the Office dataset and pre-trained caffemodel are prepared, the example can be run with the following command:
```
"./build/tools/caffe train -solver models/DAN/amazon_to_webcam/solver.prototxt -weights models/bvlc_reference_caffenet/bvlc_reference_caffenet.caffemodel"
```

Resnet pre-trainded model is [here](https://github.com/KaimingHe/deep-residual-networks). We use Resnet-50.

Parameter Tuning
---------------
In mmd-layer and jmmd-layer, parameter `loss_weight` can be tuned to give mmd loss different weights.

Citation
---------------
    @inproceedings{DBLP:conf/icml/LongC0J15,
      author    = {Mingsheng Long and
                   Yue Cao and
                   Jianmin Wang and
                   Michael I. Jordan},
      title     = {Learning Transferable Features with Deep Adaptation Networks},
      booktitle = {Proceedings of the 32nd International Conference on Machine Learning,
                   {ICML} 2015, Lille, France, 6-11 July 2015},
      pages     = {97--105},
      year      = {2015},
      crossref  = {DBLP:conf/icml/2015},
      url       = {http://jmlr.org/proceedings/papers/v37/long15.html},
      timestamp = {Tue, 12 Jul 2016 21:51:15 +0200},
      biburl    = {http://dblp2.uni-trier.de/rec/bib/conf/icml/LongC0J15},
      bibsource = {dblp computer science bibliography, http://dblp.org}
    }
