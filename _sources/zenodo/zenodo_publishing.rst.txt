.. _zenodo_guidelines:

***********************************************
MolSSI Publishing Guidelines on Zenodo Platform
***********************************************

* Source: |zenodo_badge|

This document presents a set of guidelines and recommendations for publishing software and educational contributions 
(collectively referred to as products) using the Zenodo platform and tagging them to one or more curated community
collections.

Requirements and Policies
=========================

Hosting platforms
-----------------
At this time, Zenodo only supports git (specifically, GitHub) as the distributed version control system for hosting
the products. As such, we recommend users to have their source codes hosted on GitHub for simplifying the publishing
process on Zenodo. Zenodo can be linked to GitHub anytime (not necessarily when setting up an account). To do so, 
first log into your Zenodo account. From the top-right corner of the screen, click on the drop-down button beside 
the username label and click on the linked accounts tab. Then, click on the connect button within the GitHub tab at 
the center-right side of the screen to allow access to your GitHub account and select the repositories you wish to give
access to Zenodo using your credentials.

Versioning system
-----------------
MolSSI recommends users to tag/version their products according to the `Semantic Versioning System <https://semver.org/>`_
as ``X.Y.Z`` where the numbers ``X``, ``Y``, and ``Z`` refer to ``major``, ``minor``, and ``patch``, respectively. 
`Calendar Versioning (CalVer) <https://calver.org/>`_ system can alternatively be used as ``YYYY.MM.DD.MICRO``, where 
the dot-separated numbers refer to ``year``, ``month``, ``day``, and ``MICRO`` which denotes the index of each release per day.
All numbers should be used without leading zeros, e.g., ``2021.8.9`` not ``2021.08.09``. The first micro-release 
(``MICRO = 0``) should not be included in the tag. For example, one should adopt ``2021.8.9`` not ``2021.8.9.0`` for 
the aforementioned micro release.

DOIs, indices and referencing
-----------------------------
The Digital Object Identifier (DOI) is a persistent and unique index assigned to each electronic or digital object. 
All services and registrations pertinent to DOIs are managed by `International DOI Foundation <https://www.doi.org/>`_.
Users are encouraged to register their products for a unique DOI.

Zenodo allows the assignment and management of two types of DOIs: (i) general, and (ii) specific. General DOI 
provides identification for products as an independent entity regardless of their version number(s). However, specific DOIs
always correspond to a particular version. **Note that the users can reserve DOIs for each product BEFORE manually publishing 
to Zenodo.** Unfortunately, the pre-publishing DOI reservation is not possible with the automated publishing process through 
connected GitHub repositories.

In addition, Zenodo allows the developers to link their ORCID ID to their Zenodo account in order to improve the visibility 
and searchability of their contributions through cross-referencing. The first step in this process is to log into your Zenodo
account. From the top-right corner of the screen, click on the drop-down button beside the username label and click on the 
linked accounts tab. Then, you can click on the connect button corresponding to ORCID to allow access to your ORCID account 
through your credentials.

Submission Process
==================

Publishing the Source Files
---------------------------

*Source files with Zenodo DOIs*
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
There are two methods for publishing source files on Zenodo. The preferred method is to sign up to Zenodo through your GitHub 
account and allow access to those repositories that you wish to publish their sources on Zenodo. After publishing the source files
corresponding to each repository, Zenodo starts tracking its changes and creates snapshots with each GitHub release. In other words,
Zenodo publishes the source files whenever a new release is pushed on GitHub.

By default, Zenodo uses metadata from each GitHub release to populate its main publication page. For example, the name of the authors
are extracted from the list of contributors from the repository *etc.* . The default behavior can be modified using the `.zenodo.json` 
script that should be placed in the root directory of the source GitHub repository. For further details, please refer to Zenodo’s 
developer guide and documentation.

The second way is to manually upload files to Zenodo. This is done via the Upload tab at the top middle part of the Zenodo website. 
In the new page, click on the New Upload green button at the top right corner of the Zenodo website and populate all mandatory fields
in the publishing form. The advantage of this manual approach is the DOI can be pre-reserved so that it can be incorporated into the 
files before uploading, allowing e.g. the version specific DOI to be put in recommended citations. 

The latter approach is especially useful for single-source products without a hosting repository. For example, in order to publish a 
single educational document, the source file should be directly uploaded to Zenodo and also tagged to the MolSSI-education community,
should the author(s) wish to have it peer-reviewed. Each time the source files get modified and subsequently uploaded by the author, 
Zenodo will update its publication version and corresponding version-specific DOI. Text-based documents are a practical example in 
this category, for which MolSSI recommends uploading the source file in the *OpenDocument Format (.odt)* accompanied by its
*Portable Document Format (.pdf)* copy.

*Source files with non-Zenodo DOIs*
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Source files with non-Zenodo DOIs cannot be updated within the Zenodo system, conveniently. For updating source files with non-Zenodo 
DOIs, the authors have to contact the Zenodo support team through a `contact form <https://zenodo.org/support>`_ provided by Zenodo 
as explained `here <https://help.zenodo.org/>`_.

Curated communities
-------------------

*Software*
^^^^^^^^^^
When publishing the software packages, they can be tagged to one of MolSSI’s curated communities to be peer-reviewed by one or more MolSSI
Software Scientists. Upon approval, each software package becomes a part of the MolSSI curated software community.

*Educational materials (MolSSI-Education)*
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Educational materials such as tutorials and workshops, if tagged to the MolSSI-education curated community, will be peer-reviewed by one or 
more MolSSI educators. Upon approval, these tutorials become available under MolSSI curated communities on Zenodo. In either case the record
is immediately available on Zenodo but will not be listed in the curated collection until approved.

Upload restrictions and limitations
-----------------------------------
At this time, Zenodo has a limit of 50GB for uploading each dataset. For larger datasets, the authors need to contact Zenodo’s support team. 
There is no limit on the size of Zenodo communities. For further information, refer to Zenodo’s `FAQ page <https://help.zenodo.org/>`_.

Funding and Grant Acknowledgements
----------------------------------
Zenod provides a Funding field in its publication form to search for funding agencies such as *National Science Foundation* and *OpenAIRE*. 
This capability was mainly designed for OpenAIRE-supported projects only. However, If you cannot find your funding agency through search, 
you can use the Additional Notes field for acknowledgement.

Withdrawal
----------
Although it is possible to delete the uploaded source files and communities on Zenodo, withdrawal must be considered as a dire change and should
be avoided at all costs. The main page of each community or published product provides means for their omission from Zenodo platform. The user has
to be logged into their Zenodo account, has the ownership of the product and be in edit mode in order to have access to the delete buttons.

.. citation badges

.. |zenodo_badge| image:: https://zenodo.org/badge/DOI/10.5281/zenodo.5290617.svg
   :target: https://doi.org/10.5281/zenodo.5290617