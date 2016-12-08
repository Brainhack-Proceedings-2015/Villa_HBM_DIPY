---
event: '2015 OHBM Hackathon (HI)'

title: 'DIPY: Brain tissue classification'

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
  
url: https://github.com/villalonreina/dipy/tree/pve

coi: None

acknow: The authors would like to thank the organizers and attendees of the 2015 OHBM Hackathon. Julio E. Villalon-Reina was funded by Google Summer of Code 2015.

contrib: Julio E. Villalon-Reina and Eleftherios Garyfallidis performed the project and wrote the report.

bibliography: brainhack-report

gigascience-ref: \href{http://gigadb.org/dataset/100238}{doi:10.5524/100238}
...

#Introduction
DMRI is used for creating visual representations of the structural connectivity of the brain, also known as tractography. Research has shown that using a tissue classifier can be of great benefit to create more accurate representations of the underlying connections \cite{Girard2014}.

The aim of this project was to implement an image segmentation algorithm in DIPY \cite{Garyfallidis2014} for classifying the different tissue types of the brain using structural T1 weighted images (T1-w) and diffusion MRI images (dMRI), and to  incorporate the resulting tissue probability maps for Anatomically-Constrained Tractography (ACT) \cite{Smith20121924}. We used Diffusion Power Maps (DPMs), which are scalar maps that are calculated from dMRI data and have a tissue contrast similar to the T1-w. By performing the tissue classification on dMRI derived scalar maps, the T1-w to dMRI registration step can be avoided. 

#Approach
We used a Bayesian approach for the segmentation in a similar fashion than the methods proposed in \cite{Zhang2001} and \cite{Avants2011} by applying the Maximum-A-Posteriori (MAP) procedure. The prior probability was modeled with Markov Random Fields (MRF). The MRF distribution was modeled as a Gibbs distribution. We used the Expectation Maximization (EM) algorithm to update the tissue labels at each site and to update the parameters of the log-likelihood in all iterations.

#Results
The first row of figure 1 shows the tissue classification on T1-w, the initial segmentation  based on maximum likelihood and the final segmentation after 10 iterations and beta=0.1. Beta determines the weight of the neighborhood in the MRF model. These two parameters were tuned and validated by permuting 42 different combinations and calculating the Jaccard index between the segmentation of the proposed method against manually segmented brains from the IBSR dataset [[http://www.nitrc.org/projects/ibsr](http://www.nitrc.org/projects/ibsr)]. The second row of figure 1 shows the probability maps of the three main tissue classes of the brain. The top row of Figure 2 shows on the left the Diffusion Power Map (DPM), followed by its tissue classification and the streamlines from the corpus callosum reconstructed with ACT. The bottom row of figure 2 shows the tissue probability maps of the segmentation performed on a DPM. 

\begin{figure}[h!]
  \includegraphics[width=.48\textwidth]{brainseg.png}
  \caption{\label{centfig} Example segmentations on T1 images.}
\end{figure}

\begin{figure}[h!]
  \includegraphics[width=.46\textwidth]{Power_map_fig.png}
  \caption{\label{centfig} Example segmentations on Difussion Power Maps (DPM).}
\end{figure}

# Conclusions

We developed a segmentation algorithm based on a Bayesian framework by using the MAP-MRF approach and EM. The algorithm was tested on T1-w as well as on DPMs \cite{Dell2014}. The tissue specific probability maps from both the T1-w and the DPMs were then used for ACT. We were able to successfully run ACT with the tissue probability maps derived from the DPMs.
