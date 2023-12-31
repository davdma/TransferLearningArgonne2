# Transfer Learning Continued

At the end of the summer internship, I felt there were certain approaches to the problem of PFAS modeling I did not get a chance to fully explore. For example, I had not tried changing the composition of the underlying dataset in which we attempted to transfer learned knowledge from towards the task of PFAS bioaccumulation prediction. Given the evidence that the chemicals in the general dataset have very different physico-chemical properties from PFAS, it was likely that the lack of knowledge transfer was due to the source domain being too far off from the target domain. 

To test out this possibility, I decided to try out more combinations, specifically by tweaking the chemical substances used for training to find chemicals structurally similar to PFAS so that training on those samples would allow for more appropriate transfer of knowledge based on how close their chemical domains were.

![thumbnail_IMG_0968](https://github.com/davdma/TransferLearningModularized/assets/42689743/6de9ea91-eb48-4ec2-9750-de216e0c2cb6)
