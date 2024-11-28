# SmARTR-Networks
A series of networks to implement photorealistic renderings through the MeVis Path Tracer from: "[The Smartr Pipeline: a modular workflow for the cinematic rendering of 3D scientific imaging data"](https://www.cell.com/iscience/fulltext/S2589-0042(24)02702-0)

![SmARTR_GIF_ADJ](https://github.com/user-attachments/assets/4f82c9cc-06e3-4640-98c7-0b78a137b818)

**The SmARTR Pipeline and networks**

**Introduction**

Welcome to the **Sm**all **A**nimal **R**ealistic **T**hree-dimensional **R**endering Pipeline (**SmARTR**) GitHub repository! The **SmARTR** Pipeline is a comprehensive multi-step workflow that guides users through sample preparation, imaging and visualization procedures. This project hosts a collection of comprehensive **MeVisLab** network files—referred to as **SmARTR networks**—designed to leverage the extraordinary capabilities of the **MeVis path tracer** in generating **photorealistic renderings** of 3D data. These networks integrate all steps from sample loading to rendering, volume modification, and the final processes required to produce high definition 2D images of your samples.
To assist users in implementing and utilizing the **SmARTR** visualization framework, a [step-by-step guide](https://www.biorxiv.org/content/biorxiv/early/2024/07/05/2024.07.03.601651/DC1/embed/media-1.pdf?download=true) is provided as the Supplemental Data of our article. This guide details the implementation and use of the different **SmARTR networks**. While network files are already available in this GitHub repository, the scan and mask files plus fully pre-configured networks designed to replicate the visualizations described in the various sections of the guide have been uploaded to **Zenodo**  (https://doi.org/10.5281/zenodo.12508131).
Although our primary focus has been on small animal microCT scanning, the pipeline is versatile and can be applied to any biological specimen and 3D data, including those derived from MRI and other imaging methodologies. 
________________________________________
**The SmARTR networks**

The SmARTR networks integrate every step necessary for high-quality renderings and, though each network is designed with a particular scenario in mind, their applications are broad. As a general overview of the possibilities offered by each network, please have a look at **Figure 2** in the article.
***


**1. SmARTR_Single_Volume network**

The SmARTR_Single_Volume network is designed for rendering a single, homogeneous, and non-segmented volume—such as a single organ or animal part. "Homogeneous" refers to both the exterior and interior composition of the volume, which can be well approximated by a single appearance profile (color, light interaction, etc.). This ensures that the rendering accurately represents the volume's natural aspect, even if volume cutting is performed.

•	If the single volume has non-homogeneous structures you wish to highlight, consider using the SmARTR_Nested_Multi-Volume network for photorealistic cutaway views.
________________________________________

**2. SmARTR_Multi-Mask_Volume network**


The SmARTR_Multi-Mask_Volume network allows rendering of multiple subvolumes derived from the same scan volume within the same 3D scene. This is achieved by utilizing segmentation masks to "label" corresponding subvolumes on the whole scan volume. The network generates multiple instances (copies) of the entire scan volume, each displaying only the subvolume specified by its segmentation mask.

•	Instances are less resource-demanding than loading new volumes, improving performance.

•	The network features an internal circuit to automatically crop loaded volumes to size, reducing real-time rendering and image acquisition time.

•	If independent manipulation of subvolumes is needed, consider the SmARTR_Multi-Independent_Volume network.
________________________________________
**3. SmARTR_Multi-Independent_Volume network**

The SmARTR_Multi-Independent_Volume network provides a method to render multiple subvolumes extracted from the same scan volume as independent structures within the same 3D scene. Subvolumes are extracted using segmentation masks in an accessory network (the SmARTR_Volume_Extraction network) and then rendered independently.

•	The network includes an internal circuit for cropping loaded volumes to size, optimizing performance. In some cases, when the source volume is particularly large, it can be less demanding than the SmARTR_Multi-Mask_Volume network.

•	The network allows generating cuts in multiple volumes using a single cutting module—a feature not possible in the SmARTR_Multi-Mask_Volume network.
________________________________________
**4. SmARTR_Nested_Multi-Volume network**

The SmARTR_Nested_Multi-Volume network enables photorealistic cutaway views when dealing with volumes nested within one another, such as the head with its skull and brain, or the body with its visceral organs. The strategy developed in this network saves time by avoiding the need for extensive segmentation of intermediate structures when creating photorealistic multi-organ cutaway views. Volume cutting operations in this network generate a supplementary volume at the interface between the exposed surface and the overlaying space. This new volume can be rendered independently to match the internal appearance of the sectioned volume, thereby enhancing scene realism.

•	The network can be utilized when dealing with single non-homogeneous volumes and also to add an extra level of control and refinement when rendering single homogeneous volumes.
________________________________________
**5. SmARTR_Pattern_Drawing network**

The SmARTR_Pattern_Drawing network allows the creation of color patterns on volumes to approximate the natural coloration of samples. While complex color schemes may be unattainable due to limitations of internal imaging and DVR techniques, this network enables the generation of multiple patterns rendered as independent structures, enhancing realism and lifelikeness of rendered specimens.

•	Detailed guidance on how to implement bilateral patterns or symmetric markings extending beyond the midline is provided in the Supplemental information accompanying the article.

•	The binary masks generated during pattern drawing can be utilized in the SmARTR_Advanced_Multi-Volume network to create enhanced cutaway views.
________________________________________
**6. SmARTR_Advanced_Multi-Volume network**

The SmARTR_Advanced_Multi-Volume network is a modified version of the SmARTR_Nested_Multi-Volume network and serves as the endpoint of a workflow involving multiple networks. It allows enhanced cutaway views of multiple volumes that share the same internal structure but differ in surface color, such as the atrial and ventricular regions of the lizard’s heart or differently colored parts of a lizard's body.

•	The network uses the binary masks generated in the SmARTR_Pattern_Drawing network. Alternatively, the structure of interest can be segmented with MeVisLab segmentation modules or in an external software.

•	As for the SmARTR_Multi-Independent_Volume network, the individual volumes are extracted in the SmARTR_Volume_Extraction network.

________________________________________
For detailed instructions, please refer to the [step-by-step guide](https://www.biorxiv.org/content/biorxiv/early/2024/07/05/2024.07.03.601651/DC1/embed/media-1.pdf?download=true) provided as Supplemental Data of the article.
________________________________________
**Visual Examples**

To showcase the capabilities of the SmARTR pipeline powered by the MeVis path tracer, here are some examples of photorealistic 3D renderings generated using our networks:


![MeVisLab_Web_Panel_1 copy](https://github.com/user-attachments/assets/95739f70-39ff-4787-9bca-eac37b5f1c85)

***
![MeVisLab_Web_Panel_2 copy](https://github.com/user-attachments/assets/330a9800-d633-45dc-89f3-8ba5d389986b)

***
![MeVisLab_Web_Panel_3 copy](https://github.com/user-attachments/assets/028076e9-a54a-4e79-ac12-56f0fe44e694)

***
![MeVisLab_Web_Panel_4 copy](https://github.com/user-attachments/assets/ed48cebd-8265-4c9b-8e00-a13102015dbe)

___________________________
**Contribute**

We welcome contributions from the community! Feel free to:

•	Modify networks: Adapt networks to new use cases and share your enhancements.

•	Report issues: Submit bug reports or feature requests.

•	Collaborate: Join discussions and collaborate on future developments.

For questions, support, or to share your experiences, please open an issue in the repository or contact us by email at: simone.macri@helsinki.fi

***


Let's make the SmARTR Pipeline community grow together! With our comprehensive networks exploiting the full power of MeVisLab visualization framework and integrating all steps from data loading to final image production, advanced 3D visualization has never been more accessible.

***

