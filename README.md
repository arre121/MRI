This project is part of a master's thesis titled Quality Assessment of Brain Magnetic Resonance Imaging Using Machine Learning. It focuses on
developing and comparing machine learning models for automatic quality assessment of brain MRI scans. Manual quality control is often 
time-consuming and subjective—this project aims to provide an efficient and consistent alternative using AI-based approaches.

The codebase includes implementations of four different methods: 3D Convolutional Neural Networks (3D CNN), 2D Convolutional Neural Networks (2D CNN),
PCA-based techniques, and a custom method called deepMI, which introduces a novel scoring system with penalty functions to better reflect subtle 
distortions in MRI data.

For the CNN-based models, the project explores how different sampling strategies, namely importance sampling and uniform sampling affect model performance. 
In the PCA-based approach, two classic models, linear regression and support vector machines (SVM), are compared to evaluate their effectiveness 
in predicting image quality based on principal components.

High-quality MRI data is essential for both clinical diagnostics and research. However, datasets often contain noisy or corrupted scans 
that can bias downstream analyses. This project provides automated tools that can help researchers, radiologists, and medical imaging 
teams quickly filter out low-quality scans or flag them for further inspection—saving time and reducing human error.

To run the code, you'll need preprocessed MRI scans generated using FreeSurfer. Specifically, the project expects brainmask.mgz files, 
which contain skull-stripped volumes focusing on brain tissue only. These files are used as input for all model pipelines.

The MRI preprocessing is handled within the method-specific scripts. A common load_and_preprocess_MRI function is responsible for 
standardizing all input scans. This includes: 

Loading volumes using Nibabel (nib.load) from brainmask.mgz files.
Resampling the 3D volumes to a consistent shape of 128×128×128, ensuring compatibility across the dataset.
Normalizing voxel intensities to the [0,1] range to reduce variability and improve model convergence.

After preprocessing, the dataset is split into an 80/20 train-test split, and the appropriate model is trained and evaluated. You can run each method 
individually by navigating to the relevant script folder, e.g. 3D CNN, PCA, etc.

For the deepMI method you need csv files of the MRI scans which needs to have been preprocessed by FreeSurfer. The csv files need to have the following data:
wm snr orig
gm snr orig 
wm snr norm
gm snr norm
cc size
lh holes
rh holes 
lh defects
rh defects
rot tal x 
rot tal y
rot tal z

These are the metrics used for the scoring system. When inputting the csv file into code 
the method produces quantitative and visual summaries. 



