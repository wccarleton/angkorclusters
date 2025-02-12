---
title: "Interrogating low-density urbanism at Angkor via quantitative spatial comparison with Medieval Hampshire"
author: 
  - name: "W. Christopher Carleton"
    affiliation: "Department of the Co-evolution of Land-use and Urbanism, Max Planck Institute of Geoanthropology, Jena, Germany"
  - name: "Sarah Klassen"
    affiliation: "To be determined"
  - name: "John Murphy"
    affiliation: "To be determined"
  - name: "Patrick Roberts"
    affiliation: "Department of the Co-evolution of Land-use and Urbanism, Max Planck Institute of Geoanthropology, Jena, Germany"
date: "2024-12-05"
---

# Abstract
Since the concept of low-density urbanism was introduced to urban archaeology, it has become a widely accepted but loosely defined label applied to diverse sites and ancient cultures around the world. It broadly refers to settlements that have certain features or evidence considered indicative of urban processes---like civic ceremonial monuments, heterogeneous economic activity, and formal public spaces---but a spatial structure that differs from familiar preindustrial cities. Unlike compact, walled cities, low-density forms appear to have had more diffuse building patterns, integrated agro-urban land-use, no appreciable density clines, and they lacked formal boundaries distinguishing urban from rural space. The type-site for low-density urban settlement is Angkor, the eponymous political, economic, and religious centre of the Angkorian World located in modern-day Cambodia (c. 800-1500 CE). Frequently, Angkor is juxtaposed with pre-modern compact urbanism, frequently represented by walled medieval European settlements, for example. But, these labels have never been given concrete quantitative definitions and low-density urban centres have never been directly, quantitatively compared with the complimentary, high-density types in a systematic way beyond rough estimates of overall building density. Using a newly developed Python package for temporally aware spatial archaeological research called ChronoCluster, we employed pairwise distance density functions to directly compare Angkor's spatial structure to that of Medieval Hampshire as recorded in the Domesday survey of the mid-11th century CE. Our analysis revealed some differences, but also a striking similarity that suggests perhaps the two seemingly different settlement patterns may be scaled versions of the same underlying urban process. This finding raises new questions about the mechanisms affecting urban form and challenges the prevailing dichotomy between low-density and compact premodern urbanism.

# Introduction

Low-density urbanism has become a widely used label in urban archaeology, but it has never been subject to rigorous systematic evaluation.

Despite its prevalence, the term remains loosely defined, and distinctions between 'low-density' and classical, compact urbanism have relied on visual impressions and single density estimates rather than formal quantitative tests.
-going to introduce a term like 'urbs-ex-rural' here so we have a descriptive label rather than a potentially laden one like 'classic' for the 'other' kind of urbanism

Angkor, as the type-site of low-density urbanism, is frequently contrasted with sites in the 'urbs-ex-rural' category.

Medieval Hampshire provides a valuable comparative case because, like Angkor, it represents a spatially distributed system of socioeconomic institutional centers embedded in an agrarian landscape.

- Although Angkor has been classified as low-density urbanism and Hampshire has not, this distinction is largely a product of heuristic labels rather than empirical spatial analysis.

| **Comparative Aspect**                     | **Manorial Estates (Medieval Europe)**      | **Community Temples (Angkor)**                                                                 |
|--------------------------------|---------------------------------------------|------------------------------------------------------------------------------------------------|
| **Primary Function**           | Feudal economic and social organization     | Religious worship, community integration, agircultural production                              |
| **Key Contribution to Rulers** | Military service, rents, and dues           | Rice and labor contributions                                                                   |
| **Core Role**                  | Local production and redistribution; religious for church-owned estates         | Local production and redistribution, along with ritual and spiritual services                   |
| **Connection to State**        | Feudal hierarchy linking lords and vassals  | Centralized administration under the king (degree of centralization varying through time) |
| **Symbolism**                  | Feudal order legitimised by divine right    | Sacred cosmology and royal divine mandate                                                      |
| **Autonomy**                   | Local judicial and administrative autonomy  | Centralized integration into royal networks                                                    |
| **Economic Foundation**        | Mixed agriculture/livestock, markets        | Rice agriculture, craft production, some external trade                                        |
| **Infrastructure Supported**   | Castles, manorial courts, and local defense | Temples, irrigation systems, and state projects                                                |
| **Cultural Context**           | Secular with some religious undertones; overtly religious for church-owned estates      | Deeply rooted in Hindu-Buddhist traditions                                                     |
| **Type of Obligation**         | Military and economic                       | Religious and agricultural         |

To evaluate whether Angkor and Hampshire exhibit fundamentally different spatial structures justifying their placement in mutually exclusive categories, we compared the two cases using pairwise distance density (PDD) functions available in the `ChronoCluster` Python package. The `ChronoCluster` package was developed following a spacetime archaeology paradigm, explicitly designed to account for chronometric uncertainty. Each point in a `ChronoCluster` point set is assigned both spatial and temporal coordinates, with probability distributions reflecting temporal uncertainties. The package uses these distributions to calculate the probability that a given point existed in the relevant point-set at any given time, enabling temporally-weighted spatial statistics and the propagation of temporal uncertainty into spatial analyses. Using these tools, we produced PDD functions for comparison between the two settlement areas. Building a PDD involves computing all pairwise inter-point distances for a given point-set and then approximating the distribution of those distances with a density function. These distributions reveal multiscale structure in the point set, including clustering and repulsion, across inter-point distances. These patterns, in turn, provide insight into the underlying spatial logic of settlement organization. Importantly, `ChronoCluster` allowed us to propagate chronological uncertainties about the start and end times of the points in our point sets. This was most relevant for Angkor because, unlike the Domesday Book with well-known historical provenience, the Angkorian temple foundation dates have primarily been estimated using Bayesian modelling and machine learning approaches, which have temporal uncertainties associated with them that need to be considered and propagated along the analytical pipeline. We reasoned that if the PDDs in the two cases revealed different spatial structures, the finding would support the prevailing assumptions that Angkor represents a distinct kind of low-density premodern urbanism. If, however, the results revealed similar underlying spatial structures, the finding would challenge the idea that premodern low-density urbanism differed significantly from other forms, suggesting that these two seemingly distinct urban traditions represent variations on a common spatial logic.

# Methods
## Data Acquisition
Our analysis involved two sets of point data. The first dataset consisted of 1431 community temple locations in the Greater Angkor area, 105 of which have foundation dates estimated directly using epigraphy and/or art and architectural assessments. We acquired the point data from the supplementary material of Carleton et al. and followed the methods of that study to estimate posterior age estimates for the foundation dates of the 1326 undated temples. We then estimated a mean and standard deviation from the posterior samples for each modelled foundation date. These parameter estimates were subsequently used to define normal distributions for the start times of the corresponding world-lines in the spacetime framework. The directly dated temples, in contrast, were assigned Dirac delta densities (constant dates, effectively) for their start times. Since no direct chronological information about temple or community abandonment are available for Angkor, we used Dirac delta densities to represent the end date distributions of all temples with the distributions centred on the historically defined political abandonment of Angkor at 1435 CE.

The second dataset consisted of 435 manorial estates located in Medieval Hampshire listed in the Domesday Book. Shortly after his victory over Harold II at the Battle of Hastings in 1066 CE, William the Conqueror commissioned a survey of England's lands, aiming to strengthen Norman control and lay the foundations for his administrative reforms. The survey concluded in 1086 CE and results were compiled into the multi-volume Domesday Book. Entries in the book pertain to manorial estates---economic, social, and administrative units of land, organized under the feudal system and directly controlled by a lord or the Catholic Church. The contents of the book were translated and digitalized in 2015 by scholars at the University of Hull and the National Archives, a process that included deducing the locations or manorial estates (down to 100m by 100m UK Ordinance Survey grid squares). We downloaded the raw data, including point locations, from the University of Hull website. We then isolated the points listed as within the county of Hampshire and cleaned a couple instances of points well outside the county having been duplicated and mislabelled as belonging to 'Hampshire'---this problem was first noticed because the maximum inter-point distances calculated during our anlaysis were initially far larger than expected and subsequent plotting in QGIS revealed two 'Hampshire' points in other, distant counties that had identical coordinates to points with different (locally appropriate) county labels. Next, we used Dirac delta functions to represent the densities associated with start and end dates for each location and set the relevant parameters corresponding to the period between the Battle of Hastings in 1066 CE and the conclusion of the Domesday survey in 1086 CE.

## Spacetime Modelling of PDDs with Chronological Uncertainty
Our primary focus was on estimating and comparing the PDD functions between the case studies based on the point data representing hierarchically nested socioeconomic nodes embedded in managed agrarian landscapes. As we mentioned, PDD functions are densities that represent the relative frequency of pairwise distances in a given point set. They are a staple of spatial analysis in geography and have been used in archaeology for many decades. The function characterizes multiscalar (across all possible pairwise distances) structure in point process distributions, enabling the kind of direct comparisons between patterns at the centre of the present study. In general, estimating a PDD involves measuring inter-point distances for all possible point dyads and then representing the resulting distribution with a historgram or smooth density estimate. Here we used a standard Gaussian Kernel Density Estimate (KDE) for each set of $n$ inter-point distances, $(x_1, x_2, \ldots, x_n), which was given by:

$$
\hat{f}(x) = \frac{1}{n h \sqrt{2\pi}} \sum_{i=1}^{n} \exp \left( -\frac{(x - x_i)^2}{2h^2} \right)
$$

where:

- $\hat{f}(x)$ is the estimated probability density function at $x$,
- $n$ is the number of inter-point distances,
- $x_i$ are the observed inter-point distances,
- $h$ is the bandwidth parameter, controlling the degree of smoothing,
- The kernel function $K(u)$ is given by the standard Gaussian kernel:

$$
K(u) = \frac{1}{\sqrt{2\pi}} e^{- \frac{1}{2} u^2}
$$

which corresponds to the probability density function of a standard normal distribution.

The bandwidth parameter $h$ was selected using the heuristic from the `KernelDensity` module in `sklearn`, given by:

\[
h_{\text{opt}} = 1.06 \, \sigma \, n^{-1/5}
\]

where \( \sigma \) is the **standard deviation** of the inter-point distances. This method, commonly referred to as **Silverman’s rule of thumb**, provides an automatic bandwidth selection that balances bias and variance.

Thus, KDE was implemented using the `sklearn.neighbors.KernelDensity` function:

\[
\texttt{KernelDensity(kernel="gaussian", bandwidth=h)}
\]

This approach provides a **continuous probability density estimate** for inter-point distances, avoiding the discretization bias of histograms while retaining a smooth representation of the distribution.



In order to account for chronological uncertainty and potential change over time in an archaeological point pattern, we we used a new python package---as we noted---called `ChronoCluster`. The package adopts a spacetime perspective for modelling archaeological data, which means that both space and time are considered dimensions that make up a spacetime volume---imagine a 3D plot area where spatial coordinates are represented by the x- and y-axes while time is represented by a vertical z-axis. Each point in the volume is considered an abstract 'event' and has some temporal persistence, or extent, represented by line connecting its start- and end-times. The line is commonly called a "world line." A cornerstone of spacetime modelling with the `ChronoCluster` package is the calculation of "inclusion probabilities" given uncertain start- and end-date distributions for each point's world line. The package can calculate the probability that a given point existed---i.e., should be included in the point set---at any time (or "time slice") inside the spacetime volume. To perform the calculation, the package has to assign a random variable with a valid probability density function ($PDF(x)$), a valid cumulative probability density function ($CDF(x)$), and a valid survival function ($S(x)$) to the start- and end-coordinates of the point on the time-axis. Then, the probability that the point existed at any given time, $p(t)$, is the probability that the event's world line has started, $p_\alpha(t)$, multiplied by the probability that it has not yet ended, $\neg{p_\omega(t)}$. The former is given by the $CDF(t)$ of the start-date distribution while the latter is given by the survival function, $S(t)$, of the end-date distribution. 

These 


