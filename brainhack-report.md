---
event: '2015 OHBM Hackathon (HI)'

title: 'DIPY: Brain tissue classificationn'

author:

- initials: JEVR
  surname: Villalon-Reina
  firstname: Julio E.
  email: julio.villalon@ini.usc.edu
  affiliation: aff1
  corref: aff1
- initials: EG
  surname: Garyfallidis
  firstname: Eleftherios
  email: garyfallidis@gmail.com 
  affiliation: aff2
	
affiliations: 

- id: aff1
  orgname: 'Imaging Genetics Center, Mark and Mary Stevens Neuroimagng and Informatics Institute, Keck School of Medicine of University of Southern California'
  street: 4676 Admiralty Way
  postcode: 90292
  city: Marina del Rey
  state: California
  country: USA
- id: aff2
  orgname: "Département d'informatique, Université de Sherbrooke"
  street: 2500 boulevarde de l'Université
  postcode: J1K2R1
  city: Sherbrooke
  state: Québec
  country: Canada
  
url: https://github.com/villalonreina

coi: None

acknow: The authors would like to thank the organizers and attendees of the 2015 OHBM Hackathon.

contrib: JEVR and EG performed the project and wrote the report.
  
bibliography: brainhack-report

gigascience-ref: REFXXX
...

#Introduction
To implement an image segmentation algorithm in DIPY \cite{Garyfallidis2014} for classifying the different tissue types of the brain using structural T1 images and diffusion MRI images (dMRI) as well as to incorporate tissue probability maps for Anatomically-constrained tractography (ACT) \cite{Smith20121924}.

DMRI is used for creating visual representations of the structural connectivity of the brain, also known as tractography. Research has shown that using a tissue classifier can be of great benefit to create more accurate representations of the underlying connections \cite{Girard2014}.

#Approach
We used a Bayesian approach for the segmentation \cite{Zhang2001,Avants2011} by applying the Maximum-A-Posteriori (MAP) procedure. The prior probability was modeled with Markov Random Fields (MRF). The MRF distribution was modeled as a Gibbs distribution. We used the Expectation Maximization (EM) algorithm to update the tissue labels at each site and to update the parameters of the log-likelihood in all iterations. 

#Results
The first row of the figure shows an example T1 structural image, the initial segmentation and the final segmentation after 12 iterations and beta=0.01. Beta determines the weight of the neighborhood in the MRF model. The second row shows the probability maps of the three main tissue classes of the brain. These maps were used in the ACT algorithm and improved fiber tracking. 


\begin{figure}[h!]
  \includegraphics[width=.48\textwidth]{brainseg.png}
  \caption{\label{centfig} Example segmentations.}
\end{figure}



# Conclusions
We developed a segmentation algorithm based on a Bayesian framework by using the MAP-MRF approach and EM. The algorithm was tested on T1-weighted images as well as on dMRI derived maps, such as the Diffusion Power Maps (DPM) \cite{Dell2014}. The tissue specific probability maps from both the T1 and the DPMs were then used for ACT.