#Random Forest for Multiple Sclerosis Lesion Segmentation - MS-challenge-2016

Author: Francisco Javier Vera Olmos
mail:javier.vera@urjc.es

This project is based on Python 2.7 and Matlab Compiler Runtime to use SPM toolbox. 

This paper explain how this software works:
https://www.overleaf.com/read/jjkhxzszpdhv

To use this software you need the followings python package.

MedPy
NumPy
scikit-learn
SciPy
matplotlib
XlsxWriter

The easiest way to install them is using Conda, wich install most of the package, and then use pip to install MedPy, scikit-learn and XlsxWriter.

Also it is mandatory needed to have installed the Matlab Compiler Runtime(MCR) and a SPM standalone installation compatible with that MCR.

To execute the program you need to parse the path of your SPM standalone isntallation and( only if you use a Linux or a MacOS systems) you have to parse the path to your MCR.

The inputs are the followings:

positional arguments:
  t1_raw                path of the T1-w volume
  flair_raw             path of the FLAIR volume
  t1_pp                 path of the T1-w volume
  flair_pp              path of the FLAIR volume
  spm_path              path to spm.sh if linux or spm.exe if windows
  output_folder         path where outputs and intermediate files will be
                        stored

optional arguments:
  -h, --help             show this help message and exit
  -mcr_path MCR_PATH     matlab compiler runtime path
  -t2_raw T2_RAW         path of the T2-w volume
  -dp_raw DP_RAW         path of the DP volume
  -gado_raw GADO_RAW     path of the T1-Gado volume
  -t2_pp T2_PP           path of the T2-w volume
  -dp_pp DP_PP           path of the DP volume
  -gado_pp GADO_PP       path of the T1-Gado volume
  -brain_mask BRAIN_MASK path of the brain-mask volume


For now two modes are implemented :

1- Using T1 and FLAIR sequence 
2- Using T1, T2, FLAIR, Proton Density (DP) and Gadoline T1 (GADO)

It is mandatory to provide the paths of the raw images and the preprocessed volumes of every sequence.


The outputs generated are stored in two folders: "intermediates" and "results".

In "intermediates" you have all the files and vols that must be generating during the running of the software.
This intermediates files depends on the inputs provided and they can be the followings:
  
Folder descriptors --> It contains the descriptor generated to use the Random Forest.
Folder results_csf_ext --> It contains the segmentation of the CSF exterior.
Folder results_rf --> It contains the probabilistic mask generated by the Random Forest.
File brain_mask.nii.gz --> brain mask it is generated only if not provided.
File c1[nameofyourT1].nii --> CSF segmentation.
File c2[nameofyourT1].nii --> WM segmentation.
File c3[nameofyourT1].nii --> GM segmentation.
File [nameofyourT1]_corrected.nii.gz --> T1 with intensity corrected.
File [nameofyourT2]_corrected.nii.gz --> T2 with intensity corrected.
File [nameofyourFLAIR]_corrected.nii.gz --> FLAIR with intensity corrected.
File [nameofyourDP]_corrected.nii.gz --> DP with intensity corrected.
File [nameofyourGADO]_corrected.nii.gz --> GADO with intensity corrected.
File [nameofyourT1]_seg8.mat --> mat generated by SPM.
File [nameofyourT1].nii --> uncompressed T1. 
File gen_batch.m --> batch generated to run in SPM.



In "results" you have the final lesion MS mask generated.


Example of usage:
python ms_run.py 3DT1.nii.gz 3DFLAIR.nii.gz T1_preprocessed.nii.gz FLAIR_preprocessed.nii.gz  spm12_r6685\spm12\spm12_win64.exe output_path


#Summary


Multiple Sclerosis (MS) is a chronic, inflammatory and demyelinating disease that primarily affects the white matter of the central nervous system. Automatic segmentation of MS lesions in brain MRI has been widely investigated in recent years with the goal of helping MS diagnosis and patient follow-up. It offers an attractive alternative to manual segmentation, which remains a time-consuming task and suffers from intra- and inter-expert variability. We propose a new approach that uses a Random Forest (RF) classifier. Its input has been filtered with a threshold based on the gray matter (GM) distribution and uses several features that take into account voxel and context information. A Markov Random Field (MRF) post processing algorithm has been applied to make lesions grow through probable neighborhoods. Our approach will be used in the MS challenge 2016, that will take place in October during MICCAI 2016. Therefore, in order to train and test the method we use the database provided from the challenge, which consists in 15 subject from 4 different centers, imaged on 1.5T or 3T scanners.The provided MR sequences include: 3D FLAIR, 3D T1-w, 3D T1-w GADO, 2D DP and 2D T2. In this data set each patient has being manually annotated by seven experts. We found that segmentation results are maximized by using all available sequences, but the FLAIR volume provides most of the information. Thus our method can work only with the T1-w volume to segment the tissues and the FLAIR volume to extract the most important features, still, its performance improves slightly if more types of sequences are available.


#FAQ

In the future I will add support for just raw images and implement the skull stripping and the bias correction, but FSL wich is the most used in skull stripping is only native for linux and I want to keep this project in mostly python code and for all plataforms, so it's going to take time. 



