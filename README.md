# Computer Vision in Microbiology

## Detect Measure & Classify Antibiogram Using CNN

**Antibiogram Test**, a widely used tool in microbiology to find the level of [antimicrobial susceptibility](https://en.wikipedia.org/wiki/Disk_diffusion_test) is currently performed by clinicians manually, using a ruler or digital caliper.  In some way this is impractical, prone to misread the results and outdated given the current available technology.

In this repo, we use Deep Learning and Computer Vision techniques to improve antibiogram testing process.

1. Generate synthetic antibiogram images for training.  Create synthetic image w/annotation for segmentation and bbox(COCO format). 
    
    - **NB Name**: 1_Synthetic_Images_Antibiogram.ipynb 
    - [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)]()

|Real Image Sample                                  | Synthetic Image                               | Generate Annotation |
|:-------------------------------------------------:|:---------------------------------------------:|:----------------------------------------------------:|
![](/data/images/readme/9_antibiogram_raw.jpg)|![](/data/images/readme/synthetic_image.jpg)|![](/data/images/readme/synthetic_annotation.jpg) 
 
Source Real Image: https://www.tgw1916.net/antibiogram.html

---------------------------------------------------------------------------------------------------------------------------------------------- 
2. Convert files to COCO format.  Concatenate JSON files obtained in "1_Synthetic_Images_Antibiogram.ipynb" into a COCO format file.
    
    - **NB Name**: 2_Convert2COCO.ipynb
    - [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)]()

    **Note: how to create foreground or background images is not part of the code.  For more information on how to create these images, please refer to the reference section at the end of the repo.**
    
---------------------------------------------------------------------------------------------------------------------------------------------    
3. Detect and measure zone of inhibition with Mask-RCNN. The presence of "zone of inhibition" in an antibiogram image and measures the total diameter of "no growth bacteria zone".  The size of the inhibition zone will decide the bactericide effectiveness. In the absence of inhibition zone, we conclude that the bacteria is resistant to the antibiotic.  Traditionally, to measure zone of inhibition, researchers used ruler or digital caliper.  In this nb, we will detect and measure zone of inhibition using Mask-RCNN.

    - **NB Name**: 3_AntimicrobialDisk-Detectron2.ipynb 
    - [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)]()

| Measure Zone of Inhibition w/Ruler          |  Detect Zone of Inhibition and Disks w/MaskRCNN   | Measure Size of Zone of Inhibition |
| :------------------------------------------:|:-------------------------------------------------:|:---------------------------------: |
| ![](/data/images/readme/measure-ruler.jpg)  | ![](/data/images/readme/.jpg)                     | ![](/data/images/readme/.jpg)   |

---------------------------------------------------------------------------------------------------------------------------------------------

4. Antimicrobial disks name detection and recognition.  The name of antimicrobial disk is printed at the top of each disk.  The names are abbreviated like, for example: GEN(acronym for Gentamicin), CB100(acronym for Clarithromycin), or ENO15(acronym for Enrofloxacin).  This nb rotates the letters into its right position for text recognition using tessearct.
    
    - **NB Name**: 4_CRAFT-Text-Detect.ipynb (completion: 80%)
    - [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)]()

| Skew Images                               |  Deskew Images with Rotation              |
| :----------------------------------------:|:----------------------------------------: |
| ![](/data/images/readme/.png)             | ![](/data/images/readme/.jpg)             |



![](/data/images/readme/process_flow.png)

---------------------------------------------------------------------------------------------------------------------------------------------

## More Details on Antibiogram

**Antibiogram** is a toolkit widely used in hospital and medical laboratories to aid clinicians, epidemiologists, pharmacists and alike healthcare practitioners to detect and monitor trends in antimicrobial resistance and prevent infections.

Antibiogram profiles antibiotic resistance, it tests if a specific type or sub-types of pathogens is vulnerable to antibiotics. Antibiotics eliminates pathogens, different pathogens requires different antibiotics. Bacteria, viruses, fungi and parasites are pathogens that cause diseases.  These microorganisms can also mutate in ways that will render antibiotics used to cure the infections they cause ineffective.   Antibiogram report helps doctors to choose the correct antimicrobial treatment for the patient.  And in the event of urgent public health threat, antibiogram enable pathogen researchers in identifying and combating the spread of drug-resistant organisms. 
  

The following image depicts a simplified antibiogram testing process for quick illustration(for additional information see reference below):

| Simplified Antibiogram Process         |
:----------------------------------------:
![](/data/images/readme/antibiogram-process.jpg)
Source: http://blog.eoscu.com/blog/what-is-an-antibiogram


>"At the patient level, a drug susceptibility report can be provided to the doctor to help choose the correct antibiotic. A sample from the patient is sent to the lab, where a technician tests it against a panel of antibiotics at various levels of concentration (to see how much of the drug is needed to kill the pathogen). Finally, the samples are observed for visible growth of the pathogen. They are >looking for the Minimum Inhibitory Concentration (MIC), the lowest concentration of the drug that shows no pathogen growth.

>Depending on the pathogen/antibiotic combination, there are predetermined levels of concentration (think of this as a "dose") required to have the pathogen labeled as "susceptible". These are called breakpoints and serve as a boundary between the four possible labels: Susceptible, Susceptible - Dose Dependent, Intermediate, and Resistant. The final report will give the healthcare team vital information to help them choose the best antibiotic for their patient."                              -[<img src="https://render.githubusercontent.com/render/math?math=EOS^{cu}">](http://blog.eoscu.com/blog/what-is-an-antibiogram)


| Antibiogram (Diffusion Test)               |  Different Types of Results                                   |
| :----------------------------------------: | :----------------------------------------: |
![](/data/images/readme/Agar_Diffusion_Method_1.jpg)     | ![](/data/images/readme/Agar_Diffusion_Method_2.jpg)
Source: https://en.wikipedia.org/wiki/Disk_diffusion_test


**This repo was built using the mighty "fastai nbdev".  I strongly recommend everyone to try it out!**  
**For additional information please see below reference.**

## Reference:
- fastai nbdev colab:<br>
    https://nbdev.fast.ai/<br>
    https://pete88b.github.io/nbdev_colab_helper/tutorial_github.html<br>
- Antibiogram & Antimicrobial Resistance:<br>
    https://www.who.int/news-room/q-a-detail/antimicrobial-resistance<br>
    https://www.youtube.com/watch?v=-TZn3ie-iFk&feature=emb_logo<br>
    https://en.wikipedia.org/wiki/Antibiotic_sensitivity_testing<br>
    http://cdstest.net/wordpress/wp-content/uploads/2015/05/CDS-ASM-2009.pdf<br>
    https://asm.org/getattachment/2594ce26-bd44-47f6-8287-0657aa9185ad/Kirby-Bauer-Disk-Diffusion-Susceptibility-Test-Protocol-pdf<br>
- Build foreground and background images with GIMP:<br>
    https://www.youtube.com/watch?v=uhRGix-x5Mg<br>
    https://www.immersivelimit.com/tutorials/cutting-out-image-foregrounds-with-gimp<br>



