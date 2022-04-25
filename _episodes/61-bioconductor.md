---
source: Rmd
title: "Bioconductor"
teaching: XX
exercises: XX
questions:
- "Bioconductor"
objectives:
- Give an overview of the Bioconductor project including its website
- Introduce concepts of reproducibility, coherence, interoperability and stability
keypoints:
- "Tabular data in R"
---






## Bioconductor



In the previous lesson we have already learned a little bit about the  **Bioconductor**[^Bioconductor] project. In this class we will formalize our
understanding of the **Bioconductor**[^Bioconductor] project. 

**Important:** Remember that Bioconductor packages are downloaded via the function
`BiocManager::install()`. 

Bioconductor is a repository that collects open-source software that facilitates 
rigorous and reproducible analysis of data from current and emerging 
biological assays in R. In addition, 
Bioconductor supports development, education and a thriving community. The
The broad goals of the Bioconductor project are:

* To provide widespread access to a broad range of powerful statistical and graphical methods for the analysis of genomic data.
* To facilitate the inclusion of biological metadata in the analysis of genomic data, e.g. literature data from PubMed, annotation data from Entrez genes.
* To provide a common software platform that enables the rapid development and deployment of extensible, scalable, and interoperable software.
* To further scientific understanding by producing high-quality documentation and reproducible research.
* To train researchers on computational and statistical methods for the analysis of genomic data.

One of the best ways to explore the Bioconductor project is its website.

## The Bioconductor website 

<img src="../fig/bioconductor_website.png" title="Bioconductor website" alt="Bioconductor website" width="100%" style="display: block; margin: auto;" />

The website tells us that there are over **2,000** packages. This is obviously
way too many packages to explore individually. So how would you find potentially useful packages for the analysis of
your dataset?

### Exploring different topics with biocViews

In Bioconductor, each package is classified as belonging to different categories. 
These different categories are called `biocViews` and they are structured
as follows:

* Software: Packages that provide functions for statistical or graphical methods. 
* AnnotationData: Packages that store annotations (i.e genome annotation) and respective access functions.
* ExperimentData: Packages that store example datasets.
* Workflow: Packages that assemble html tutorials using multiple packages for an analysis.

Each category is further divided into additional sub-categories, which are
divided into sub-sub-categories that refer to specific assays, techniques, and
research fields.

BiocViews can help tremendously  with identifying packages that could be of use to
you in the analysis of your dataset. These are easily searchable once you have navigated 
to [the page that lists all packages](https://bioconductor.org/packages/release/BiocViews.html).

> ## Challenge
> In your groups, identify a research topic of interest and then use the search 
> function to find packages related to this topic.
> Think about the following:
> 
> * What keywords define your topic of interest?
> * What type of packages are good for beginners and why?
> * What other information on this website may be useful?
{: .challenge}

### Exploiting the detailed documentation of the Bioconductor project

<img src="../fig/bioconductor_help.png" title="Bioconductor help page" alt="Bioconductor help page" width="100%" style="display: block; margin: auto;" />

The other part of the Bioconductor website crucial for anyone's learning journey
is [the help page](https://bioconductor.org/help/). This page collects some
outstanding Bioconductor learning resources such as

* Comprehensive books introducing coverage of a research field
* Courses and conference materials
* Videos
* Community resources and tutorials.
* [Support site](https://support.bioconductor.org/)

Most importantly it introduces the concept of `vignettes`, which are part of
Bioconductor's mission to enhance **reproducibility** through **rigorous documentation**.
In Bioconductor almost every package (certainly every software package) has to 
include a vignette. Vignettes are small tutorials that explain common use cases
of a package. For example, let's explore the vignettes available for 
`SummarizedExperiment`:


~~~
browseVignettes(package = "SummarizedExperiment")
~~~
{: .language-r}

This should open a separate browser tab that will list availabe vignettes. By 
clicking on the `html` link you will open a nicely formatted tutorial that 
you should be easily able to follow. Vignettes are a great place to start when 
trying to get familar with a new package.

<img src="../fig/vignettes.png" title="Bioconductor website" alt="Bioconductor website" width="100%" style="display: block; margin: auto;" />

### Core Bioconductor principles

The Bioconductor is organized around some core principles:

* interoperablility with existing infrastructure to facilitate reuse and
avoid replication
* coherence in coding, documentation and use of existing infrastructure
* rigorous documentation
* reproducibility
* stability ensuring that there are limited clashes due to versions

While it is not absolutely necessary for the end-user to remember these, the
core principles explain some of the idiosyncrasies of Bioconductor that you
may come across.

#### S4 classes

> ## Challenge
>
> Use the function `str` on the SummarizedExperiment object you created during
> the last lession. What oddity do you notice? 
> Hint: Compare the output to output of `str` function applied to `rna`.
>
> > ## Solution
> > 
> > 
> > We can see certain elements of the object starting with an @.
> {: .solution}
{: .challenge}

S4 classes allow object-oriented programming in R and thus ensure **coherence,**
**stability, and interoperability**. In S4, certain
classes are defined with specific accessibility functions (called methods). 


~~~
# These two statements will result in the same output.

se@colData
~~~
{: .language-r}



~~~
DataFrame with 22 rows and 9 columns
                sample     organism       age         sex   infection      strain      time
           <character>  <character> <numeric> <character> <character> <character> <numeric>
GSM2545336  GSM2545336 Mus musculus         8      Female  InfluenzaA     C57BL/6         8
GSM2545337  GSM2545337 Mus musculus         8      Female NonInfected     C57BL/6         0
GSM2545338  GSM2545338 Mus musculus         8      Female NonInfected     C57BL/6         0
GSM2545339  GSM2545339 Mus musculus         8      Female  InfluenzaA     C57BL/6         4
GSM2545340  GSM2545340 Mus musculus         8        Male  InfluenzaA     C57BL/6         4
...                ...          ...       ...         ...         ...         ...       ...
GSM2545353  GSM2545353 Mus musculus         8      Female NonInfected     C57BL/6         0
GSM2545354  GSM2545354 Mus musculus         8        Male NonInfected     C57BL/6         0
GSM2545362  GSM2545362 Mus musculus         8      Female  InfluenzaA     C57BL/6         4
GSM2545363  GSM2545363 Mus musculus         8        Male  InfluenzaA     C57BL/6         4
GSM2545380  GSM2545380 Mus musculus         8      Female  InfluenzaA     C57BL/6         8
                tissue     mouse
           <character> <numeric>
GSM2545336  Cerebellum        14
GSM2545337  Cerebellum         9
GSM2545338  Cerebellum        10
GSM2545339  Cerebellum        15
GSM2545340  Cerebellum        18
...                ...       ...
GSM2545353  Cerebellum         4
GSM2545354  Cerebellum         2
GSM2545362  Cerebellum        20
GSM2545363  Cerebellum        12
GSM2545380  Cerebellum        19
~~~
{: .output}



~~~
colData(se) #colData is a method that allows access to the column meta data
~~~
{: .language-r}



~~~
DataFrame with 22 rows and 9 columns
                sample     organism       age         sex   infection      strain      time
           <character>  <character> <numeric> <character> <character> <character> <numeric>
GSM2545336  GSM2545336 Mus musculus         8      Female  InfluenzaA     C57BL/6         8
GSM2545337  GSM2545337 Mus musculus         8      Female NonInfected     C57BL/6         0
GSM2545338  GSM2545338 Mus musculus         8      Female NonInfected     C57BL/6         0
GSM2545339  GSM2545339 Mus musculus         8      Female  InfluenzaA     C57BL/6         4
GSM2545340  GSM2545340 Mus musculus         8        Male  InfluenzaA     C57BL/6         4
...                ...          ...       ...         ...         ...         ...       ...
GSM2545353  GSM2545353 Mus musculus         8      Female NonInfected     C57BL/6         0
GSM2545354  GSM2545354 Mus musculus         8        Male NonInfected     C57BL/6         0
GSM2545362  GSM2545362 Mus musculus         8      Female  InfluenzaA     C57BL/6         4
GSM2545363  GSM2545363 Mus musculus         8        Male  InfluenzaA     C57BL/6         4
GSM2545380  GSM2545380 Mus musculus         8      Female  InfluenzaA     C57BL/6         8
                tissue     mouse
           <character> <numeric>
GSM2545336  Cerebellum        14
GSM2545337  Cerebellum         9
GSM2545338  Cerebellum        10
GSM2545339  Cerebellum        15
GSM2545340  Cerebellum        18
...                ...       ...
GSM2545353  Cerebellum         4
GSM2545354  Cerebellum         2
GSM2545362  Cerebellum        20
GSM2545363  Cerebellum        12
GSM2545380  Cerebellum        19
~~~
{: .output}

> ## Challenge
>
> Why is it bad practice to use the @ to access parts of an object?
>
> > ## Solution
> > 
> > 
> > Using methods functions to access certain parts of the object enhances
> > readibility of your code. If the underlying class structure changes (i.e. the
> > name of the element) the method will still work.
> {: .solution}
{: .challenge}

If you want to know more about S4 classes you can find more information in
[these slides on their implementation in the Bioconductor package](https://bioconductor.org/packages/devel/bioc/vignettes/S4Vectors/inst/doc/S4QuickOverview.pdf).

#### The release cycle

Bioconductor has two releases each year, typically in April and October, where
all packages are updated to their next version in a way that they are 
**interoperable** (i.e. they do not clash when you load more than one). The releases
conincide with the releases of new R versions, which also happen twice a year. This has
two significant implications:

1) To ensure that packages on Bioconductor work flawlessly **always** use
`BiocManager::install` to install a package, even when it is not a technically
Bioconductor package. Biconductor mirrors most other R package repositories like
CRAN and so the package will be most likely available. This will avoid clashed
with packages being ahead of the Bioconductor release.
2) You will need to update your Bioconductor packages twice a year (after updating R) to have all the latest versions. Refer to [this guide for updating R qnd R-Studio](https://www.r-bloggers.com/2022/01/how-to-install-and-update-r-and-rstudio/)
and [this guide for updating Bioconductor](https://www.bioconductor.org/install/). 

