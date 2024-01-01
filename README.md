# Transfer Learning Continued

At the end of the summer internship, I felt there were certain approaches to the PFAS modeling problem I did not get a chance to fully explore. For example, I had not tried changing the composition of chemical classes in the underlying dataset for training my models. Given that the chemicals in the general dataset have very different physico-chemical properties from PFAS, it was likely that the lack of knowledge transfer in my prior experiments was due to not enough learning in the target domain - **in short, nothing useful could be transferred because neutral lipophilic compounds bioaccumulate very differently from PFAS.** I needed my model to learn from datapoints closer in characteristic to PFAS.

![image](https://github.com/davdma/TransferLearningArgonne2/assets/42689743/694acd0f-f990-4986-a887-59eee160b89c)
**Figure 1:** In reduced 3D feature space, the PFAS datapoints form a distinct cluster away from the cluster of neutral lipohilic compounds that represent most of the substances in the general BCF dataset.

### Methodology

1. To try to tackle this shortcoming, I collected PFAS chemicals and their corresponding chemical structures from the [OECD Global Database of Per- and Polyfluoroalkyl Substances](https://comptox.epa.gov/dashboard/chemical-lists/PFASOECD).
2. I then used PCA and UMAP dimensionality reduction methods to see where the PFAS formed a cluster in the feature space. By calculating the distance of each datapoint from the PFAS cluster, I could sample chemicals nearest to the cluster to form a training set of "PFAS-like" substances.
3. Another way I formed a group of "PFAS-like" substances was by using an automated chemical classification algorithm (I used [ClassyFire](https://jcheminf.biomedcentral.com/articles/10.1186/s13321-016-0174-y)) to classify each chemical in my dataset, and filtering for alcohols, phenols, ketones, surfactants, aldehydes, carboxylic acids, sulfonic acids, esters etc. which were more structurally similar to PFAS.
4. Similar to before, I trained a base model on the general compounds, but augmented the transfer model training data set with the "PFAS-like" substances, so that more learning occurred near the PFAS domain.

![thumbnail_IMG_0968](https://github.com/davdma/TransferLearningModularized/assets/42689743/6de9ea91-eb48-4ec2-9750-de216e0c2cb6)
**Figure 2:** A sketch I did of the workflow. Each box is a phase of the implementation which can be found as a separate jupyter notebook.

### Results

![download](https://github.com/davdma/TransferLearningArgonne2/assets/42689743/bba6d06c-9edb-41a3-9a7c-892024d3586a)

Comparing `DNN-Base-Target` to `DNN-Transfer-Target` plots we see an improvement in the prediction in the target task of "PFAS-like" substances in our model from the transfer. However, if we look at `DNN-Base-PFAS` and `DNN-Transfer-PFAS` we see that the transfer seems to have made the model averse to categorizing PFAS as bioaccumulative and underpredict when before it had been overpredicting. It seems from the experiment that our PFAS-like substances were not enough for meaningful learning to occur in the PFAS domain, further highlighting the difficulties of overcoming the PFAS data gap.


