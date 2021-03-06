### This work is being rewritten in this repo: https://github.com/chho-work/biolab 

# Computer Vision in Microbiology

## Overview

**_Detect, measure and classify Antibiogram. A training pipeline with synthetic images and Mask RCNN._**

**Antibiogram Test**, is a widely used tool in microbiology to find the level of [antimicrobial susceptibility](https://en.wikipedia.org/wiki/Disk_diffusion_test).  Part of this process consists of measuring "zone of inhibition"(see below for explanation), which is currently performed by clinicians manually using a "ruler" or "digital calliper".

![](/data/images/readme/measure_manual.png) 


In some way this is impractical and prone to error.  For example, the tiny ruler number could lead to misreading. Nevertheless, given the current available computer vision technologies, we are able to improve this measuring process.

![](/data/images/readme/measure_inference.jpg) 

In this repo, I used Deep Learning techniques to detect and measure the "zone of inhibition".  

1. Generate Synthetic Images

    - **Notebook Name**: [Synthetic_Images_Antibiogram.ipynb](/nb/Synthetic_Images_Antibiogram.ipynb)(Open in Colab!)
    - Download [53 images](https://drive.google.com/file/d/1sIeCJ2YuEzYAexzx-be7Fd7x-CQrFKjt/view?usp=sharing) and [JSON annotation files](https://drive.google.com/file/d/1DZ7YvQS04T0DdkagDsGZsPhFIrj97Z_C/view?usp=sharing) created with this notebook.  I will use them as sample to train Mask RCNN. 

    This first notebook generates synthetic images([more sample here](/data)) for training.  I created synthetic images due to lack of real images.  This notebook goes through a step-by-step process of how to create synthetic images by pasting foreground and background images into antibiogram look-alike image.  I was also able to create automatically image annotations for segmentation and bbox(COCO format). 

**Note: how to create foreground or background images is not part of the code.  For more information on how to create these images, please refer to the reference section at the end of the repo.**

|Real Image Sample                                  | [Generated Synthetic Image](/data)           | [Generate Annotation](/data)          |
|:-------------------------------------------------:|:---------------------------------------------:|:--------------------------------------:|
![](/data/images/readme/9_antibiogram_raw.jpg)|![](/data/images/readme/synthetic_image.jpg)|![](/data/images/readme/synthetic_annotation.jpg)

---------------------------------------------------------------------------------------------------------------------------------------------

2. Convert JSON Files to COCO Format:  
    
    - **Notebook Name**: [Convert2JSON(COCO).ipynb](/nb/Convert2JSON(COCO).ipynb)(Open in Colab!)

    This second notebook contains code that converts all the annotation(JSON format) files generated in the first notebook into a single COCO format file.  With this COCO format file and the synthetic images, we can start training object recognition in Mask RCNN.   
    
    
---------------------------------------------------------------------------------------------------------------------------------------------    
3. Train & Inference w/Mask-RCNN and Detect & Measure Zone of Inhibition: 

    - **Notebook Name**: [AntimicrobialDisk-Detectron2.ipynb](https://github.com/chho-work/biovision/blob/main/nb/AntimicrobialDisk_Detectron2.ipynb)(Open in Colab!)
    
    In this third notebook, I used a pretrained Mask RCNN model in Detectron2 to detect and measure zone of inhition in antibiogram images.

---------------------------------------------------------------------------------------------------------------------------------------------

**ToDo**:
 - [ ] Convert notebooks to script format
 - [ ] Connect with Weights & Biases for tracking metrics

---------------------------------------------------------------------------------------------------------------------------------------------
## More Information on Antibiogram

**Antibiogram** is a toolkit widely used in hospital and medical laboratories to aid clinicians, epidemiologists, pharmacists and alike healthcare practitioners to detect and monitor trends in antimicrobial resistance and prevent infections.

Antibiogram profiles antibiotic resistance, it tests if a specific type or sub-types of pathogens is vulnerable to antibiotics. Antibiotics eliminates pathogens, different pathogens requires different antibiotics. Bacteria, viruses, fungi and parasites are pathogens that cause diseases.  These microorganisms can also mutate in ways that will render antibiotics used to cure the infections they cause ineffective.   Antibiogram report helps doctors to choose the correct antimicrobial treatment for the patient.  And in the event of urgent public health threat, antibiogram enable pathogen researchers in identifying and combating the spread of drug-resistant organisms. 
  

The following image depicts a simplified antibiogram testing process for quick illustration(for additional information see reference below):

| Simplified Antibiogram Process         |
:----------------------------------------:
![](/data/images/readme/antibiogram-process.jpg)



>"At the patient level, a drug susceptibility report can be provided to the doctor to help choose the correct antibiotic. A sample from the patient is sent to the lab, where a technician tests it against a panel of antibiotics at various levels of concentration (to see how much of the drug is needed to kill the pathogen). Finally, the samples are observed for visible growth of the pathogen. They are >looking for the Minimum Inhibitory Concentration (MIC), the lowest concentration of the drug that shows no pathogen growth.

>Depending on the pathogen/antibiotic combination, there are predetermined levels of concentration (think of this as a "dose") required to have the pathogen labeled as "susceptible". These are called breakpoints and serve as a boundary between the four possible labels: Susceptible, Susceptible - Dose Dependent, Intermediate, and Resistant. The final report will give the healthcare team vital information to help them choose the best antibiotic for their patient."                              -[<img src="https://render.githubusercontent.com/render/math?math=EOS^{cu}">](http://blog.eoscu.com/blog/what-is-an-antibiogram)


| Antibiogram (Diffusion Test)               |  Different Types of Results                                   |
| :----------------------------------------: | :----------------------------------------: |
![](/data/images/readme/Agar_Diffusion_Method_1.jpg)     | ![](/data/images/readme/Agar_Diffusion_Method_2.jpg)



**This repo was built using the mighty "fastai nbdev".  I strongly recommend everyone to try it out!**  
**For additional information please see below reference.**

## References:
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
- Image Sources:<br> 
    https://www.ecdc.europa.eu/en/publications-data/eucast-instruction-video-reading-inhibition-zone-diameters<br>
    https://commons.wikimedia.org/wiki/File:Zone_of_Inhibition.jpg<br>
    https://www.youtube.com/watch?v=-TZn3ie-iFk<br>
    https://asm.org/getattachment/2594ce26-bd44-47f6-8287-0657aa9185ad/Kirby-Bauer-Disk-Diffusion-Susceptibility-Test-Protocol-pdf.pdf<br>
    https://en.wikipedia.org/wiki/Disk_diffusion_test<br>
    http://blog.eoscu.com/blog/what-is-an-antibiogram<br>
    https://www.tgw1916.net/antibiogram.html<br>
