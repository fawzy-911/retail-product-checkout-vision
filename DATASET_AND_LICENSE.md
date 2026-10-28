# Dataset card and usage notes

## Source

The project uses the [Retail Product Checkout (RPC) dataset](https://rpc-dataset.github.io/), made available by the dataset authors through [Kaggle](https://www.kaggle.com/datasets/diyer22/retail-product-checkout-dataset).

The official split design is central to this project:

| Split | Images | Scene type | Objects per image |
|---|---:|---|---:|
| Train | 53,739 | Single-product exemplar images | 1 |
| Validation | 6,000 | Checkout scenes | 12.27 average |
| Test | 24,000 | Checkout scenes | 12.26 average |

The training set and checkout splits are intentionally different. Do not merge the data and make a random split; doing so changes the benchmark question and risks leakage.

## License and access

The RPC project page lists the dataset license as **CC BY-NC-SA 4.0** and states that the data/code are for academic use. The project authors request contact for other uses. Read the [RPC project page](https://rpc-dataset.github.io/) and license before using the dataset.

This repository does not redistribute the images, annotations, cached files, or trained weights. Attach the dataset through Kaggle or download it under the terms provided by its authors. Do not assume that a public Kaggle dataset can be reused commercially.

## Privacy and intended data handling

The notebook expects the user to attach or download the dataset in their own Kaggle/Jupyter environment. The dataset is not copied into this Git repository. Generated images, labels, and checkpoints are written to a local/Kaggle working directory and are ignored by Git where applicable.
