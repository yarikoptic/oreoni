Research data management
=========================================================

```{admonition} Issue
Good research data management (RDM), i.e. how data are organized, maintained, annotated, tracked, stored, and accessed throughout a research project, forms the basic foundations of result reproducibility, data reusability, and research efficiency {cite:p}`Borghi2021-go,Gorgolewski2016-iy,Nosek2012-lx,Nosek2014-pg,Nosek2018-yr,Poldrack2017-xt,Poldrack2019-fn,Poldrack2020-vp,Poline2022-li,Wilkinson2016-fm`. Consequently, Data Management Plans (DMPs) are widely required by funders even at the application phase (e.g., NIH and NSF in the U.S., ERC in Europe), increasingly expected by scientific peers, and holds considerable benefits for individual researchers.
```

```{admonition} What do we provide
It is good practice to develop, review and execute DMPs for every experiment, whether or not it is required by the funding agency. While specific RDM requirements vary across subdisciplines, **this section highlights RDM standards and tools applicable across neuroimaging, ranging from data organization to annotation and publication.**
```

```{figure} ../figures/fig3.png
---
name: fig3
---
Research data management [^footnote3].
```

:::{dropdown} {fa}`folder` 4.1 Data organization and standards
:class-title: bg-ch4 font-weight-bold
:animate: fade-in
(s41)=
Neuroimaging experiments result in complicated data that can be arranged in many different ways. Historically, data were organized differently between institutions and within labs. This lack of consensus (or a standard) could lead to misunderstandings and suboptimal usage of various resources: human (e.g., time wasted on rearranging data or rewriting scripts expecting certain structure), infrastructure (e.g., data storage space, duplicates), and financial (e.g., disorganized data has limited longevity and value after first publication, because it is hard or even impossible for other researchers to understand and use it). Finally, and most importantly, it produces poor reproducibility of results, even within the lab where data were collected, because it is more likely to include errors and less likely to be accessible to future lab members (or even to the original researcher who obtained the data, months or years after they worked on it). Therefore, the need for a data standard in the neuroimaging community became essential.

The Brain Imaging Data Structure (BIDS) is a community-led standard for organizing, describing, and sharing neuroimaging data [RRID:SCR_016124]. BIDS is an evolving standard, which supports multiple neuroimaging modalities including MRI {cite:p}`Gorgolewski2016-dl`, MEG {cite:p}`Niso2018-wq`, EEG {cite:p}`Pernet2019-wa`, intracranial EEG {cite:p}`Holdgraf2019-bb`, PET {cite:p}`Norgaard2019-su`, Microscopy {cite:p}`Bourget:2022tf`, and imaging genetics {cite:p}`Moreau2020-fe`. Many more extensions are under active development, for example, fNIRS, motion capture, and animal neurophysiology. The BIDS specification documents how to organize the data, generally based on simple file formats (such as NIfTI for tomographic data {cite:p}`Cox2004-rn`, and JSON for metadata) and folder structures. This specification can be extended through community-driven processes to incorporate new neuroimaging modalities or sets of data types.

Multiple applications and tools have been released to make it easy for researchers to incorporate BIDS into their current workflows, maximizing reproducibility, enabling effective data sharing, and supporting good data management practices. For example, BIDS converters make it easier to convert data into BIDS format (e.g., MNE-BIDS {cite:p}`Appelhoff2019-kg` for MEG and EEG, dcm2bids, ReproNim’s HeuDiConv {cite:p}`Halchenko2021-ue` and ReproIn {cite:p}`Visconti_di_Oleggio_Castello2020-pm` for MRI and PET2BIDS for PET; see many more on the [resources table](../09/table.md)). The BIDS validator can help researchers make sure their dataset is BIDS-valid following conversion.

Once data are in BIDS, tools are available to ease interaction with the data. Two commonly used software packages are PyBIDS \{cite:p}{Yarkoni2019-zm}, and BIDS-Matlab {cite:p}`Gau2022-ob`. These tools facilitate useful dataset queries—such as how many participants are part of a dataset or what tasks were performed— as well as programmatically retrieving specific files—such as all functional runs for a specific subject. Finally, BIDS apps are containerized analysis pipelines that use full BIDS datasets as their input and produce derivative data {cite:p}`Gorgolewski2017-xd`. Examples of BIDS apps include MRIQC {cite:p}`Esteban2017-ow`, for MRI quality control, fMRIPrep {cite:p}`Esteban2019-pm` for fMRI preprocessing, and PyMVPA {cite:p}`Hanke2009-gp` for statistical learning analyses of large datasets (see more at the [resources table](../09/table.md)).

BIDS is a community-led standard and strives to be open and inclusive. The BIDS specification is the result of the ongoing collaboration, shared knowledge, discussion, and consensus through the email discussion list, shared Google docs, and GitHub. Questions are also answered on the Neurostars forum and the Brainhack Mattermost channel. BIDS has a well-specified governance structure where everybody is welcome to participate ([Code of Conduct](https://github.com/bids-standard/bids-specification/blob/master/CODE_OF_CONDUCT.md)), and the BIDS Starter Kit is a growing resource intended to simplify the learning process for newcomers.
:::


:::{dropdown} {fa}`tags` 4.2 Metadata and data annotation
:class-title: bg-ch4 font-weight-bold
:animate: fade-in
(s42)=
Metadata and data annotation induce consistency and facilitate data replication and reuse. It improves the clarity of the dataset, the ability for collaborators to understand the conditions in which the data were collected, and the ability to effectively share and reuse them. Commonly, metadata files are data dictionaries that map key terms from an agreed-upon vocabulary to data values that contain detailed and standardized information about the key terms. For example, a key called “SampleFrequency” might map to a numerical value, or a key “TaskDescription” might map to a free-form text that describes the task used in a specific experiment. The BIDS standard has proposed a consistent metadata structure in its specification along with a set of specification terms and tags.

Data annotation is also crucial for most data analyses in neuroimaging. For example, when analyzing task-based data, an experiment's reproducibility is largely determined by the extent to which events are clearly documented. Beyond reproducing previous findings, exhaustively annotated events can allow researchers to re-use the data for means that were originally not thought of at data collection time {cite:p}`Bigdely-Shamlo2020-pt`. However, even if each study is fully annotated, without a standard to consistently describe facets of events, all annotations will remain cumbersome and error-prone to work with, and achieving a state of machine readability will require effortful labor.

To address this problem, the Hierarchical Event Descriptor (HED) standard has been continuously developed over the past years {cite:p}`Robbins2021-bm,Robbins2021-qt`. Drawing on a set of hierarchical vocabulary structures (the HED base schema) and application rules, the HED standard allows for both human- and machine readability, validation, and search of annotations across studies. HED is furthermore fully integrated with the BIDS standard (see {ref}`Section 4.1 <s41>`), and can be extended by researcher supplied schemas.

Additionally, the Neuroimaging Data Model {cite:p}`Keator2013-az,Maumet2016-zq` effort aims to build a core structure for neuroscience datasets to improve searching across publicly-available datasets. The initiative also provides tools to create and use NIDM documents from BIDS datasets {cite:p}`Appelhoff2019-ga`. To effectively describe neuroscience data, well-developed community-driven vocabularies are needed. NIDM is built using semantic web techniques and builds off the PROV (provenance) vocabulary {cite:p}`Moreau2015-ia`. Moreover, the NIDM-Terms effort has begun to collect and extend sets of community-developed controlled vocabularies and techniques for associating concepts with selected study variables of publicly-available neuroimaging datasets (i.e., OpenNeuro, ABIDE, ADHD200, and CoRR). This keeps a registry of the domain-relevant vocabularies and concepts used to annotate datasets, further facilitating concept reuse, and improved inter-dataset search. The NIDM team has developed a JavaScript web application, as well as Python-based command line annotation tools, that allow researchers to annotate their BIDS structured datasets and single tabular files (e.g., csv and tsv spreadsheets), and export BIDS JSON-formatted data dictionaries, NIDM JSON-LD data dictionaries, and NIDM semantic web documents, into sidecar files that accompany the data files. Currently, the NIDM-Terms annotation tools allow researchers to associate their study variables with concepts available in the Cognitive Atlas {cite:p}`Poldrack2011-bv`, the InterLex information resource, and those in the canonical NIDM terminology/ontology as well as encourage them to add descriptive information to improve the clarity of their variables. Such an effort harmonizes and improves the consistency of neuroimaging data and thus makes querying across neuroimaging datasets more efficient.
:::


:::{dropdown} {fa}`database` 4.3 Data management and tracking
:class-title: bg-ch4 font-weight-bold
:animate: fade-in
(s43)=
Raw data and derivatives (outputs from processed data) form the basis for scientific analyses and insights. Being able to efficiently store, retrieve, and update data, derivatives, and metadata across a variety of available storage options is crucial to enable further research {cite:p}`Borghi2021-fw`. As files change and evolve over the course of a project, there is a need to identify which data have been used in the generation of a result, and, in case the data were subject to change or updates, which exact version of the data has been used. The ability to manage data and metadata and track the data-analysis process provides a basis for rigor and reproducibility.

DataLad {cite:p}`Halchenko2021-op` is an open-source, community-developed, general purpose tool for managing and version controlling digital files in a decentralized manner. It tracks data of any type or size in a scalable, Git-repository-based overlay structure, called the dataset (practically, a structure of folders and files). DataLad allows tracking data and metadata files stored on local devices as well as remote or cloud infrastructure. DataLad can retrieve public data from major providers such as OpenNeuro, the Canadian Open Neuroscience Platform, the International Neuroimaging Data-sharing Initiative, the Healthy Brain Network Serial Scanning Initiative, Data sharing for Collaborative Research in Computational Neuroscience, the Human Connectome Project's open access dataset {cite:p}`Van_Essen2013-ty`, and many more. Beyond public data, with appropriate permissions or authentication, it can retrieve data from web-based storage providers including major cloud storage services, and local and remote paths {cite:p}`Halchenko2021-op,Hanke2021-un`. DataLad implements this decentralized data management functionality in order to ensure streamlined access to tracked data regardless of hosting service, and to expose datasets for easy access on repository hosting structure. It separates management of file content from lean metadata management by tracking pointers to the services that host managed files (i.e., local infrastructure, remote hosting services, or multiple storage solutions at once). Using these pointers, it enables streamlined on-demand file retrieval in uniquely identified versions from the registered source. Importantly, data retrieval works via streamlined commands regardless of where the data are hosted. Information about DataLad can be found in the DataLad Handbook ({cite:p}`Wagner2021-aq`, see the [resources table](../09/table.md)). Entire computing environments could be efficiently managed in DataLad using datalad-container extension {cite:p}`Meyer2021-hb` developed in collaboration between DataLad and ReproNim projects.

[Brainlife.io](https://brainlife.io) is another open science project that allows data management. Brainlife.io is a free and open community-oriented, non-commercial cloud platform that provides web services to support reproducible data management and analysis. Brainlife.io tracks data provenance automatically for the users. As data are analyzed using the Graphical User Interfaces (GUI) and the platform’s data processing applications, provenance metadata information is automatically generated and stored associated with the data derivatives. The users do not have to manually save data versions, the platform does that automatically and it allows visualizing data provenance graphs.

DataLad and brainlife.io are synergistic but not overlapping projects that address different user bases and needs. Indeed, DataLad and Brainlife.io interact nicely with one another and all published datasets retrieved by DataLad are readily accessible at brainlife.io datasets.
:::

[^footnote3]: Sources: Icons from the Noun Project: Structure by Adam Baihaqi from NounProject.com; Metadata by M. Oki Orlando; Data Management by ProSymbols; Logos: used with permission by the copyright holders.

:::{dropdown} References on this page
```{bibliography}
:filter: docname in docnames
:labelprefix: D
```
:::
