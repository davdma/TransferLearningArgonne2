# Transfer Learning Continued

At the end of the summer internship, I felt there were certain approaches to the problem of PFAS modeling I did not get a chance to fully explore. For example, I had not tried changing the composition of the underlying dataset in which we attempted to transfer knowledge from towards the task of PFAS prediction. Given that the chemicals in the general dataset have very different physico-chemical properties from PFAS, it was likely that the lack of knowledge transfer in my prior experiments was due to the source domain being too far off from the target domain - **in short, nothing useful could be transferred because neutral lipophilic compounds bioaccumulate very differently from PFAS.**

![image](https://github.com/davdma/TransferLearningArgonne2/assets/42689743/694acd0f-f990-4986-a887-59eee160b89c)
**Figure:** In reduced 3D feature space, the PFAS datapoints form a distinct cluster away from the cluster of neutral lipohilic compounds that represent most of the substances in the general BCF dataset.

### Methodology

1. To try to tackle this shortcoming, I collected PFAS chemicals and their corresponding chemical structures from the [OECD Global Database of Per- and Polyfluoroalkyl Substances](https://comptox.epa.gov/dashboard/chemical-lists/PFASOECD).
2. I then used PCA and UMAP dimensionality reduction methods to see where the PFAS formed a cluster in the feature space. By calculating the distance of each datapoint from the PFAS cluster, I could sample chemicals nearest to the cluster to form a training set of "PFAS-like" substances.
3. Similar to before, I trained a base model on these "PFAS-like" substances, and transferred the weights to a new model for learning on the smaller PFAS dataset. 

![thumbnail_IMG_0968](https://github.com/davdma/TransferLearningModularized/assets/42689743/6de9ea91-eb48-4ec2-9750-de216e0c2cb6)
