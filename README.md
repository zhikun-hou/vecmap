VecMap (cross-lingual word embedding mappings)
==============
## map_embeddings.py
- 缩写：`sim=similarity`
- 参数组：`aaai2018,acl2017,acl2017_seed,emnlp2016`会通过`parser.set_defaults`直接设置一个参数组
  - `emnlp2016`是有监督学习，可以顺着它的参数走：`self_learning=False`,`init_unsupervised=False`
  - 由于init_*均为None，它的字典是213-222行通过读取一个外部文件来构造的
- 注意：`xw,zw`不是翻译模型的参数W！
  - 在eval_translation.py中，直接`embeddings.read`之后就在第121行计算相似度了，说明`xw,zw`直接就是latent space embedding
  - 所以在第285/286行才将xw和z进行输出

  

## 理论基础
- map_embedding.py中涉及到`svd`分解的部分，理论基础来自：***[Offline bilingual word vectors, orthogonal transformations and the inverted softmax](https://arxiv.org/abs/1702.03859)***
- 这篇文章提出了直接进行SVD分解，一次性得到结果，而不是像之前的工作一样先对W做随机梯度下降再做SVD分解

## 原始论文
- Mikel Artetxe, Gorka Labaka, and Eneko Agirre. 2018. **[A robust self-learning method for fully unsupervised cross-lingual mappings of word embeddings](https://aclweb.org/anthology/P18-1073)**. In *Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)*.
- Mikel Artetxe, Gorka Labaka, and Eneko Agirre. 2018. **[Generalizing and improving bilingual word embedding mappings with a multi-step framework of linear transformations](https://www.aaai.org/ocs/index.php/AAAI/AAAI18/paper/view/16935/16781)**. In *Proceedings of the Thirty-Second AAAI Conference on Artificial Intelligence (AAAI-18)*, pages 5012-5019.
- Mikel Artetxe, Gorka Labaka, and Eneko Agirre. 2017. **[Learning bilingual word embeddings with (almost) no bilingual data](https://aclweb.org/anthology/P17-1042)**. In *Proceedings of the 55th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)*, pages 451-462.
- Mikel Artetxe, Gorka Labaka, and Eneko Agirre. 2016. **[Learning principled bilingual mappings of word embeddings while preserving monolingual invariance](https://aclweb.org/anthology/D16-1250)**. In *Proceedings of the 2016 Conference on Empirical Methods in Natural Language Processing*, pages 2289-2294.
