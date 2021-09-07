.. _ml_guidelines:

**********************************************************
MolSSI Formatting Guidelines for Machine Learning Products
**********************************************************

* Source: |ml_badge|

This document presents a set of guidelines and best practices for formatting machine learning (ML) products (e.g., datasets, 
modules, models, *etc.*) before submitting them on the `Zenodo <https://zenodo.org/>`_  platform and tagging them to one or 
more curated MolSSI community collections.

Requirements and Policies
=========================

Prerequisites
-------------
Before getting started, please take a glance at the 
`MolSSI Publishing Guidelines on Zenodo Platform <https://doi.org/10.5281/zenodo.5290616>`_ to familiarize yourself with
the basic mechanics and recommended strategies for publishing your software products on Zenodo.

Dataset File Formats
--------------------
Datasets are tables of data hosting instances (chemical species such as atoms, molecules, macromolecules *etc.*) in rows and features
or descriptors in columns. Each label results from an experimental observation or theoretical calculation and corresponds to a feature.
As such, labels are stored at the intersection of each row and column. 

We recognize two main conceptual categories for featurizing the input data: (i) geometrical data (e.g., coordinates, connectivities,
atomic symbols, *etc.*), and (ii) chemical features (e.g., energetics, electronic properties *etc.*).

*Geometrical Data*
^^^^^^^^^^^^^^^^^^
Representation of geometrical data pertinent to individual chemical species such as molecules (or monomers, dimers, polymers, clusters, unit
cells, *etc.*) is dependent upon the task and adopted ML algorithm. In general, the raw information on individual molecular structures
should be stored as separate files within a subfolder of the root directory called geometries. The recommended file format for storing
geometrical data is the `Chemical Table Format (*.mol*) <https://en.wikipedia.org/wiki/Chemical_table_file>`_ which allows for a convenient
usage of popular and free chemical data conversion toolkits such as `Open Babel <http://openbabel.org/wiki/Main_Page>`_. This representation
is probably most useful before training each model since the majority of the ML models require a featurized version of these structures into
a numerical representation or embedding.

For molecules with no bonding information, it is acceptable to use the `XYZ file format (*.xyz*)
<https://en.wikipedia.org/wiki/XYZ_file_format>`_ while for periodic (crystalline) systems the `Crystallographic Information File (*.cif*)
<https://en.wikipedia.org/wiki/Crystallographic_Information_File>`_ would be appropriate, while for biomolecules the closely related
`Macromolecular Crystallographic Information File (*.cif* or *.mmcif*) <https://en.wikipedia.org/wiki/Crystallographic_Information_File>`_
is usually the best choice. 

The text-based molecular structure representations such as 
`Simplified Molecular-Input Line-Entry System (SMILES) <https://en.wikipedia.org/wiki/Simplified_molecular-input_line-entry_system>`_
provide an alternative to geometrical coordinates and are comparatively straightforward to be stored in the dataset tables. 
SMILES are often precursors for an embedded vector representation of the input structures. Software packages such as 
`RDKit <https://www.rdkit.org/>`_ cheminformatics program and `Open Babel <http://openbabel.org/wiki/Main_Page>`_ toolkit provide 
modules for the featurization of the SMILES into acceptable representations for ML algorithms. These representations, for example, 
can be based on graph convolutions, physical properties or *extended-connectivity fingerprints (ECFPs)*.

*Chemical Features*
^^^^^^^^^^^^^^^^^^^
MolSSI's recommendation for storing the features such as SMILES, energetics or property values is the *comma-separated value (CSV)*
format. This file should be stored in the root directory of the main dataset repository as ``<dataset_name>_meta.csv``. This provides a
coherent and convenient way for popular tools such as the `Pandas <https://pandas.pydata.org/>`_ library in python to perform the
input/output (I/O) operations and easily convert them between the popular storage formats such as `hierarchical data format (HDF)
<https://www.hdfgroup.org/>`_, JSON *etc.*.

Metadata File Formats
---------------------
MolSSI encourages all users to carefully record their metadata in a separate ``<dataset_name>_meta.csv`` file and store it in 
the root directory of the main dataset repository. Each row in the metadata table should correspond to a column label 
[the headline (first) row of the main dataset CSV file] and should at least, describe its type accompanied by a short 
description of what they are referring to. For example, molecular charge is often of integer type and reflects the electrical
charge on the molecule at its ground electronic state in vacuum.

Naming Conventions
------------------
In order to make both I/O, query and search operations more convenient, all geometrical files within geometries folder should
be named as ``<dataset_name>_<id>.mol`` where the name of the dataset in the all-lowercase form is appended by its dataset table
``id`` and separated by an underscore. Each ``id`` is an integer type value located at the first column of the dataset table and 
corresponds to an individual chemical species included in the geometry *.mol* files. 

For performance reasons, a large number of geometry files can be batched into separate subfolders of the geometries folder and 
sorted according to the ``geometries/<batch_number>`` naming convention. For the sake of consistency, all file names, feature 
titles, and labels should be in lowercase.

Data Types
----------
Depending on the nature of the data object, both features and labels can assume different data types.

*Scalar Quantities*
^^^^^^^^^^^^^^^^^^^
Numerical-type scalar properties such as molecular charge can be stored as integers or floats with different bit lengths.

*Vector Quantities*
^^^^^^^^^^^^^^^^^^^
By default, the elements of the dense vector quantities such as multiple moments should be stored in separate columns.
For dense vectors of variable length, however, multiple techniques can be adopted. Since the majority of ML models require
the input vectors of the same length, it is possible to find the dimension of the largest vector and pad the other smaller-size
vector instances with zeros. Popular ML frameworks such as TensorFlow provide data preprocessing tools to deal with these cases.
Nevertheless, zero padding wastes the storage resources. In some cases, we might choose to organize such variable length features
in separate ``<feature>.csv`` files in the root directory and deal with them differentlly alongside describing the details of the 
adopted approach in the corresponding ``<dataset_name>_meta.csv`` file. MolSSI’s recommendation, however, is to keep the number of
files in the root directory to its minimum.

Another way is to store the vector elements is to serialize the vector to a string or byte representation. The former representation
might not be economical for very large datasets while the latter might be more appropriate for I/O operations via limited bandwidths
over the network.

*Higher-order (>1) Tensor Quantities*
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Dense matrices and higher dimensional tensors can be flattened to their one dimensional counterparts and treated like vectors.
For sparse matrices and higher dimensional tensors, however, ML frameworks usually provide tools to use the sparsity or manipulate 
the representation such as converting it to a one-hot for classification tasks. There are also libraries that can handle the 
packing/unpacking operations for sparse matrices and tensors such as `Armadillo <http://arma.sourceforge.net/>`_ in C++ and 
`scipy.sparse <https://docs.scipy.org/doc/scipy/reference/sparse.html>`_ in python. Should the user decide to use a different 
approach that is not supported by the existing tools, the details of packing/unpacking of the tensor elements should be explicitly 
delineated in the metadata ``<dataset_name>_meta.csv`` or ``Readme.md`` file in the root directory of the main repository. MolSSI 
recommends the authors to provide scripts or utility modules in order to assist the data engineering process. The corresponding 
tools should be placed in the ``utility`` subfolder in the root directory.

*Non-numerical Quantities*
^^^^^^^^^^^^^^^^^^^^^^^^^^
Non-numerical quantities such as SMILES, by construction, can be stored in the string format for each instance entry and as a 
separate feature.

.. citation badges

.. |ml_badge| image:: https://zenodo.org/badge/DOI/10.5281/zenodo.5389982.svg
   :target: https://doi.org/10.5281/zenodo.5389982
