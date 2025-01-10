# The SmARTR Networks 
A series of **MeVisLab** networks to implement photorealistic renderings through the **MeVis Path Tracer** from: 

"[**The SmARTR pipeline: a modular workflow for the cinematic rendering of 3D scientific imaging data**](https://www.cell.com/iscience/fulltext/S2589-0042(24)02702-0)"

![SmARTR_GIF_ADJ](https://github.com/user-attachments/assets/4f82c9cc-06e3-4640-98c7-0b78a137b818)

---

**The SmARTR Pipeline**

Welcome to the **Sm**all **A**nimal **R**ealistic **T**hree-dimensional **R**endering Pipeline (**SmARTR**) GitHub repository!

The **SmARTR** Pipeline is a comprehensive multi-step workflow (**see figure below**) that guides users through sample preparation, imaging and visualization procedures. This project hosts a collection of comprehensive **MeVisLab** network files—referred to as **SmARTR networks**—designed to leverage the extraordinary capabilities of the **MeVis path tracer** in generating **photorealistic renderings** of 3D data. These networks integrate all steps from sample loading to rendering, volume modification, and the final processes required to produce high definition 2D images of your samples.


The **SmARTR Networks are available** [**HERE**](https://github.com/MeVisLab/SmARTR-Networks/raw/refs/heads/main/SmARTR%20Networks.zip?download=) and on [**Zenodo**](https://doi.org/10.5281/zenodo.12508131) as a zipped folder. The folder contains also a **step-by-step guide** to assist users in implementing and utilizing the **SmARTR** visualization framework, fully pre-configured versions of the networks, and all the relevant scan and mask files needed to replicate the visualizations described in the guide. The **step-by-step guide** is also available as [**Supplemental Data**](https://www.cell.com/cms/10.1016/j.isci.2024.111475/attachment/34225920-1cf3-4d9a-87ee-74dc8131a97f/mmc1.pdf) in our published article.

Although our primary focus has been on small animal microCT scanning, the pipeline is **versatile** and can be applied to **any biological specimen and 3D data**, including those derived from MRI and other imaging methodologies.

![G_ABS_3_RED_FINAL_GIT](https://github.com/user-attachments/assets/9613c040-93a3-4f04-a6cd-85ebb4a4dddc)
***


<p align="center"> <ins>Click on the thumbnail below to watch a short video on YouTube summarizing our work<ins>
</p>

<div align="center">
  <a href="https://www.youtube.com/watch?v=2hrkvZmuVxI"><img src="https://img.youtube.com/vi/2hrkvZmuVxI/0.jpg" alt="IMAGE ALT TEXT"></a>
</div>


---
 
 **The SmARTR networks at a glance**

The **SmARTR networks** integrate every step necessary for high-quality renderings and, though each network is designed with a particular scenario in mind, their applications are broad. As a general overview of the possibilities offered by each **SmARTR network**, please have a look at the **Table** below.


![FIG 2_FINAL_SUB](https://github.com/user-attachments/assets/95144ce4-db21-4e9a-bddd-fe56da263c25)

***


**1. <ins>SmARTR_Single_Volume network<ins>**

The SmARTR_Single_Volume network is designed for rendering a single, homogeneous, and non-segmented volume—such as a single organ or animal part. "Homogeneous" refers to both the exterior and interior composition of the volume, which can be well approximated by a single appearance profile (color, light interaction, etc.). This ensures that the rendering accurately represents the volume's natural aspect, even if volume cutting is performed.

•	_If the single volume has non-homogeneous structures you wish to highlight, consider using the **SmARTR_Nested_Multi-Volume network** for photorealistic cutaway views._
________________________________________

**2. <ins>SmARTR_Multi-Mask_Volume network<ins>**


The SmARTR_Multi-Mask_Volume network allows rendering of multiple subvolumes derived from the same scan volume within the same 3D scene. This is achieved by utilizing segmentation masks to "label" corresponding subvolumes on the whole scan volume. The network generates multiple instances (copies) of the entire scan volume, each displaying only the subvolume specified by its segmentation mask.

•	_Instances are less resource-demanding than loading new volumes, improving performance._

•	_The network features an internal circuit to automatically crop loaded volumes to size, reducing real-time rendering and image acquisition time._

•	_If independent manipulation of subvolumes is needed, consider the **SmARTR_Multi-Independent_Volume network**._
________________________________________
**3. <ins>SmARTR_Multi-Independent_Volume network<ins>**

The SmARTR_Multi-Independent_Volume network provides a method to render multiple subvolumes extracted from the same scan volume as independent structures within the same 3D scene. Subvolumes are extracted using segmentation masks in an accessory network (the SmARTR_Volume_Extraction network) and then rendered independently.

•	_The network includes an internal circuit for cropping loaded volumes to size, optimizing performance. In some cases, when the source volume is particularly large, it can be less demanding than the **SmARTR_Multi-Mask_Volume network**._

•	_The network allows generating cuts in multiple volumes using a single cutting module—a feature not possible in the **SmARTR_Multi-Mask_Volume network**._
________________________________________
**4.<ins> SmARTR_Nested_Multi-Volume network<ins>**

The SmARTR_Nested_Multi-Volume network enables photorealistic cutaway views when dealing with volumes nested within one another, such as the head with its skull and brain, or the body with its visceral organs. The strategy developed in this network saves time by avoiding the need for extensive segmentation of intermediate structures when creating photorealistic multi-organ cutaway views. Volume cutting operations in this network generate a supplementary volume at the interface between the exposed surface and the overlaying space. This new volume can be rendered independently to match the internal appearance of the sectioned volume, thereby enhancing scene realism.

•	_The network can be utilized when dealing with single non-homogeneous volumes and also to add an extra level of control and refinement when rendering single homogeneous volumes._
________________________________________
**5. <ins>SmARTR_Pattern_Drawing network<ins>**

The SmARTR_Pattern_Drawing network allows the creation of color patterns on volumes to approximate the natural coloration of samples. While complex color schemes may be unattainable due to limitations of internal imaging and DVR techniques, this network enables the generation of multiple patterns rendered as independent structures, enhancing realism and lifelikeness of rendered specimens.

•	_Detailed guidance on how to implement bilateral patterns or symmetric markings extending beyond the midline is provided in the Supplemental information accompanying the article._

•	_The binary masks generated during pattern drawing can be utilized in the **SmARTR_Advanced_Multi-Volume network** to create enhanced cutaway views._
________________________________________
**6. <ins>SmARTR_Advanced_Multi-Volume network<ins>**

The SmARTR_Advanced_Multi-Volume network is a modified version of the SmARTR_Nested_Multi-Volume network and serves as the endpoint of a workflow involving multiple networks. It allows enhanced cutaway views of multiple volumes that share the same internal structure but differ in surface color, such as the atrial and ventricular regions of the lizard’s heart or differently colored parts of a lizard's body.

•	_The network uses the binary masks generated in the **SmARTR_Pattern_Drawing network**. Alternatively, the structure of interest can be segmented with MeVisLab segmentation modules or in an external software._

•	_As for the **SmARTR_Multi-Independent_Volume network**, the individual volumes are extracted in the **SmARTR_Volume_Extraction network**._

________________________________________
For detailed instructions, please refer to the  **step-by-step guide** distributed together with the [**SmARTR Networks**](https://github.com/MeVisLab/SmARTR-Networks/raw/refs/heads/main/SmARTR%20Networks.zip?download=) and as [**Supplemental Data**](https://www.cell.com/cms/10.1016/j.isci.2024.111475/attachment/34225920-1cf3-4d9a-87ee-74dc8131a97f/mmc1.pdf) in our published article.
________________________________________
<ins> **Rendering examples** <ins>

To showcase the capabilities of the SmARTR pipeline powered by the MeVis path tracer, below are some examples of photorealistic 3D renderings generated using our networks



![MeVisLab_Web_Panel_1 copy](https://github.com/user-attachments/assets/95739f70-39ff-4787-9bca-eac37b5f1c85)

**(Top row)**: Images of a live specimen of the lizard *Anolis carolinensis* (left) and the dissected heart from the bearded dragon lizard, *Pogona vitticeps* (right). **(Bottom row)**: 3D renderings of the heart of *Pogona vitticeps* (top left), the sectioned head of *Anolis carolinensis* highlighting the skull and brain (top right), and an intact specimen of *Anolis carolinensis* (bottom). **$\textcolor{red}{SmARTR\ Networks\ used}$** : **SmARTR_Multi-Independent_Volume network** for the *Pogona vitticeps* heart; **SmARTR_Advanced_Multi-Volume network** for the sectioned head; **SmARTR_Pattern_Drawing** for the intact *Anolis carolinensis* specimen.
  **$\textcolor{red}{© Macrì\ S\ and\ Di-Poï \ N\ (University\ of\ Helsinki,\ Finland)}$** 


***
![MeVisLab_Web_Panel_2 copy](https://github.com/user-attachments/assets/330a9800-d633-45dc-89f3-8ba5d389986b)


**(Top row)**: Renderings of the head of the snake *Cerastes cerastes*—intact (left) and sectioned to highlight the venom system (right). **(Bottom row)**: Renderings of the anterior part of the hillstream loach, *Gastromyzon zebrinus*—sectioned to highlight the skeleton, brain, and gills (left) and intact (right).  **$\textcolor{red}{SmARTR\ Networks\ used}$** : **SmARTR_Pattern_Drawing network** for the intact specimens; **SmARTR_Advanced_Multi-Volume network** for the cutaway views.  **$\textcolor{red}{© Macrì\ S\ and\ Di-Poï \ N\ (University\ of\ Helsinki,\ Finland)}$** 

***
![MeVisLab_Web_Panel_3 copy](https://github.com/user-attachments/assets/028076e9-a54a-4e79-ac12-56f0fe44e694)


**(Top row)**: Renderings of the head of the lizard *Basiliscus vittatus* (left), and the heart (middle) and lungs (right) of the lizard *Pogona vitticeps*, both sectioned to reveal internal structures. **(Bottom row)**: Renderings of the lungs (left), head (middle), and trunk (right) of the house mouse, *Mus musculus*. **$\textcolor{red}{SmARTR\ Networks\ used}$** : **SmARTR_Pattern_Drawing network** for the intact specimen; **SmARTR_Nested_Multi-Volume network** for the mouse head, lungs, and trunk, and lizard lungs; **SmARTR_Advanced_Multi-Volume network** for the cutaway view of the lizard heart. **$\textcolor{red}{© Macrì\ S\ and\ Di-Poï \ N\ (University\ of\ Helsinki,\ Finland)}$** 

***
![MeVisLab_Web_Panel_4 copy](https://github.com/user-attachments/assets/ed48cebd-8265-4c9b-8e00-a13102015dbe)


**(Top row)**: Forelimbs of the tree frog *Agalychnis callidryas* (left) and the dwarf chameleon *Chamaeleo calyptratus* (right). **(Bottom row)**: Rendering of the skeleton and internal organs of the tree frog *Agalychnis callidryas* (left), the intact body of the cricket *Gryllus bimaculatus* (middle), and the ground beetle *Pterostichus oblongopunctatus* (right).  **$\textcolor{red}{SmARTR\ Networks\ used}$** : **SmARTR_Single-Volume network** for both species' forelimbs and the beetle rendering; **SmARTR_Multi-Independent_Volume network** for the frog's skeleton and organs; **SmARTR_Pattern_Drawing neywork** for the intact cricket specimen. **$\textcolor{red}{© Macrì\ S\ and\ Di-Poï \ N\ (University\ of\ Helsinki,\ Finland)}$** 

___________________________
**Contribute**

We welcome contributions from the community! Feel free to:

•	**Modify networks**: Adapt networks to new use cases and share your enhancements.

•	**Report issues**: Submit bug reports.

•	**Collaborate**: Join discussions and collaborate on future developments.

For questions, support, or to share your experiences, please open an issue in the repository or contact us by email at: simone.macri@helsinki.fi

***


Let's make the **SmARTR community** grow together! With our comprehensive networks exploiting the full power of MeVisLab visualization framework and integrating all steps from data loading to final image production, advanced 3D visualization has never been more accessible.

***
