Under Construction<br>
Completion: 60


# Computer Vision in Microbiology

## Detect Measure & Classify Antibiogram Using CNN

**Antibiogram Test**, a widely used tool in microbiology to find the level of [antimicrobial susceptibility](https://en.wikipedia.org/wiki/Disk_diffusion_test) is currently performed by clinicians manually, using a ruler or digital caliper.  In some way this is impractical, prone to misread the results and outdated given the current available technology.

In this repo, we use Deep Learning and Computer Vision techniques to improve antibiogram testing process.



1. Generate synthetic antibiogram images for training.

	- NB Name: Synthetic_Images_Antibiogram.ipynb [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)]()
	- Description: create synthetic image w/segmentation and bbox(COCO format)

Real Image Sample                                  | Synthetic Image 1                                    | Synthetic Image 2 
:-------------------------------------------------:|:----------------------------------------------------:|:----------------------------------------------------:
![](/data/images/README/9_antibiogram_raw.jpg)     | ![](/data/images/README/synthetic_antibiogram_1.jpg) | ![](/data/images/README/synthetic_antibiogram_11.jpg) 
 
Source Real Image: https://www.tgw1916.net/antibiogram.html
 


2. Detect the presence of "zone of inhibition" in an antibiogram image and measures the total diameter of "no growth bacteria zone". 
The size of the inhibition zone will decide the bactericide effectiveness. In the absence of inhibition zone, we conclude that the bacteria is resistant to the antibiotic. 

	Traditionally, to measure zone of inhibition, researchers used ruler or digital caliper.  In this repo, we will detect and measure zone of inhibition using Mask RCNN. 

| Measure Zone of Inhibition w/Ruler        |  Detect/Measure Zone of Inhibition w/CV    |
| :----------------------------------------:|:----------------------------------------:  |
![](/data/images/README/measure-ruler.jpg)  | ![](/data/images/README/.jpg)

Note: recommended image size for inference min of 912 x 684 pixels.

3. Classify the different types of Antibiotic Disks.  The names of each antibiotic are visible in the disk.  We will classify them using a Softmax Classifier.
 
    For example: 
    - GEN 10 = Gentamicin 
    - CB 100 = Clarithromycin 
    - ENO 15 = Enrofloxacin

Name of Antibiotic printed in the disks   |  Classify Disk Type
:----------------------------------------:|:----------------------------------------:
![](/data/images/README/antimicrobial_disks.png)      | ![](/data/images/README/.jpg) 

Source: 

![](/data/images/README/process_flow_1.png)


## More Details on Antibiogram

**Antibiogram** is a toolkit widely used in hospital and medical laboratories to aid clinicians, epidemiologists, pharmacists and alike healthcare practitioners to detect and monitor trends in antimicrobial resistance and prevent infections.

Antibiogram profiles antibiotic resistance, it tests if a specific type or sub-types of pathogens is vulnerable to antibiotics. Antibiotics eliminates pathogens, different pathogens requires different antibiotics. Bacteria, viruses, fungi and parasites are pathogens that cause diseases.  These microorganisms can also mutate in ways that will render antibiotics used to cure the infections they cause ineffective.   Antibiogram report helps doctors to choose the correct antimicrobial treatment for the patient.  And in the event of urgent public health threat, antibiogram enable pathogen researchers in identifying and combating the spread of drug-resistant organisms. 
  

The following image depicts a simplified antibiogram testing process for quick illustration(for additional information see reference below):

| Simplified Antibiogram Process         |
:----------------------------------------:
![](/data/images/README/antibiogram-process.jpg)
Source: http://blog.eoscu.com/blog/what-is-an-antibiogram
 

 


>"At the patient level, a drug susceptibility report can be provided to the doctor to help choose the correct antibiotic. A sample from the patient is sent to the lab, where a technician tests it against a panel of antibiotics at various levels of concentration (to see how much of the drug is needed to kill the pathogen). Finally, the samples are observed for visible growth of the pathogen. They are >looking for the Minimum Inhibitory Concentration (MIC), the lowest concentration of the drug that shows no pathogen growth.

>Depending on the pathogen/antibiotic combination, there are predetermined levels of concentration (think of this as a "dose") required to have the pathogen labeled as "susceptible". These are called breakpoints and serve as a boundary between the four possible labels: Susceptible, Susceptible - Dose Dependent, Intermediate, and Resistant. The final report will give the healthcare team vital information to help them choose the best antibiotic for their patient."                              -[<img src="https://render.githubusercontent.com/render/math?math=EOS^{cu}">](http://blog.eoscu.com/blog/what-is-an-antibiogram)


| Antibiogram (Diffusion Test)               |  Different Types of Results                                   |
| :----------------------------------------: | :----------------------------------------: |
![](/data/images/README/Agar_Diffusion_Method_1.jpg)     | ![](/data/images/README/Agar_Diffusion_Method_2.jpg)
Source: https://en.wikipedia.org/wiki/Disk_diffusion_test

 


* This repo was built using the mighty "fastai nbdev".  For additional information please see below reference section.





## Reference

	- https://www.who.int/news-room/q-a-detail/antimicrobial-resistance
	- https://www.youtube.com/watch?v=-TZn3ie-iFk&feature=emb_logo
	- https://en.wikipedia.org/wiki/Antibiotic_sensitivity_testing
	- http://cdstest.net/wordpress/wp-content/uploads/2015/05/CDS-ASM-2009.pdf
	- https://asm.org/getattachment/2594ce26-bd44-47f6-8287-0657aa9185ad/Kirby-Bauer-Disk-Diffusion-Susceptibility-Test-Protocol-pdf.pdf



