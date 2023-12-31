# Transfer Learning Continued

At the end of the summer internship, I felt there were certain approaches to the problem of PFAS modeling I did not get a chance to fully explore. For example, I had not tried changing the composition of the underlying dataset in which we attempted to transfer knowledge from towards the task of PFAS prediction. Given that the chemicals in the general dataset have very different physico-chemical properties from PFAS, it was likely that the lack of knowledge transfer in my prior experiments was due to the source domain being too far off from the target domain - **in short, nothing useful could be transferred because neutral lipophilic compounds bioaccumulate very differently from PFAS.**

### Methodology

1. To try to tackle this shortcoming, I collected PFAS chemicals and their corresponding chemical structures from the [OECD Global Database of Per- and Polyfluoroalkyl Substances](https://comptox.epa.gov/dashboard/chemical-lists/PFASOECD).
2. I then used PCA and UMAP dimensionality reduction methods to see where the PFAS formed a cluster in the feature space. By calculating the distance of each datapoint from the PFAS cluster, I could sample chemicals nearest to the cluster to form a training set of "PFAS-like" substances.
3. These "PFAS-like" substances would then be used for training the source task, and the knowledge transferred on the small PFAS dataset. used for training the base model of the transfer learning model. by tweaking the chemical substances used for training to find chemicals structurally similar to PFAS so that training on those samples would allow for more appropriate transfer of knowledge based on how close their chemical domains were.

![thumbnail_IMG_0968](https://github.com/davdma/TransferLearningModularized/assets/42689743/6de9ea91-eb48-4ec2-9750-de216e0c2cb6)
