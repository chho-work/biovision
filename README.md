# Computer Vision in Microbiology

## Detect Measure & Classify Antibiogram Using CNN

### Overview

**Antibiogram Test**, is a widely used tool in microbiology to find the level of [antimicrobial susceptibility](https://en.wikipedia.org/wiki/Disk_diffusion_test).  Part of its process consists of measuring "zone of inhibition"(see below for explanation), which is currently performed by clinicians manually using a ruler or digital calliper.

![](/data/images/readme/measure-ruler-1.jpg) ![](/data/images/readme/measure-callipher.jpg)![](/data/images/readme/measure-ruler-2.jpg) 

Image Source: 
* https://www.ecdc.europa.eu/en/publications-data/eucast-instruction-video-reading-inhibition-zone-diameters


In some way this is impractical and prone to error.  For example, the small sizes of the ruler and petri dish could lead to misreading. Nevertheless, given the current available computer vision technologies, we are able to improve this measuring process.

![](/data/images/readme/test_image_inference.jpg) ![](/data/images/readme/zone_measure.jpg)

In this repo, I used Deep Learning techniques to detect and measure the "zone of inhibition".

1. Generate synthetic antibiogram images
    We by generating synthetic images for training.  Create synthetic image w/annotation for segmentation and bbox(COCO format). 
    
    - **Notebook Name**: [Synthetic_Images_Antibiogram.ipynb](/nb/Synthetic_Images_Antibiogram.ipynb)(Open in Colab!)
    - Download [53 images](https://drive.google.com/file/d/1sIeCJ2YuEzYAexzx-be7Fd7x-CQrFKjt/view?usp=sharing) and [JSON annotation files](https://drive.google.com/file/d/1DZ7YvQS04T0DdkagDsGZsPhFIrj97Z_C/view?usp=sharing) created with this notebook.  I will use them as sample to train Mask RCNN. 

|Real Image Sample                                  | [Generated Synthetic Image](/data)           | [Generate Annotation](/data)          |
|:-------------------------------------------------:|:---------------------------------------------:|:--------------------------------------:|
![](/data/images/readme/9_antibiogram_raw.jpg)|![](/data/images/readme/synthetic_image.jpg)|![](/data/images/readme/synthetic_annotation.jpg) 
 
Source Real Image: https://www.tgw1916.net/antibiogram.html

---------------------------------------------------------------------------------------------------------------------------------------------- 
2. Convert files to COCO format.  Concatenate JSON files obtained in "1_Synthetic_Images_Antibiogram.ipynb" into a COCO format file.
    
    - **Notebook Name**: [Convert2JSON(COCO).ipynb](/nb/Convert2JSON(COCO).ipynb)(Open in Colab!)

    **Note: how to create foreground or background images is not part of the code.  For more information on how to create these images, please refer to the reference section at the end of the repo.**
    
---------------------------------------------------------------------------------------------------------------------------------------------    
3. Detect and measure zone of inhibition with Mask-RCNN. The presence of "zone of inhibition" in an antibiogram image and measures the total diameter of "no growth bacteria zone".  The size of the inhibition zone will decide the bactericide effectiveness. In the absence of inhibition zone, we conclude that the bacteria is resistant to the antibiotic.  Traditionally, to measure zone of inhibition, researchers used ruler or digital caliper.  In this nb, we will detect and measure zone of inhibition using Mask-RCNN.

    - **Notebook Name**: [AntimicrobialDisk-Detectron2.ipynb](/nb/AntimicrobialDisk-Detectron2.ipynb)(Open in Colab!)

| Measure Zone of Inhibition w/Ruler          |  Detect Zone of Inhibition and Disks w/MaskRCNN   | Measure Size of Zone of Inhibition |
| :------------------------------------------:|:-------------------------------------------------:|:---------------------------------: |
| ![](/data/images/readme/measure-ruler.jpg)  | ![](/data/images/readme/test_image_inference.jpg)| ![](/data/images/readme/measure_zone_inhibition.jpg)   |

---------------------------------------------------------------------------------------------------------------------------------------------

**ToDo**:
 - [ ] Convert notebooks to script format
 - [ ] Add feature: text recognition of the character on top of the disk
 - [ ] Connect with Weights & Biases for tracking metrics

---------------------------------------------------------------------------------------------------------------------------------------------
## More Information on Antibiogram

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



