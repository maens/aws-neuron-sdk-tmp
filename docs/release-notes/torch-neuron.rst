PyTorch Neuron release notes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This document lists the release notes for the Pytorch-Neuron package.

Known Issues and Limitations - Updated 09/22/2020
=================================================

The following are not torch-neuron limitations, but may impact models
you can successfully torch.neuron.trace

-  The current torchvision version has dropped support for Python 3.5
-  The current HuggingFace transformers version has dropped support for
   Python 3.5
-  There are known issues when customer use a mixture of conda and pip
   packages. We strongly recommend that you install aws neuron conda
   packages if you are using a conda environment, and use the pip
   installation if you are working in a base python environment (or a
   native python virtual environment) as recommended in our installation
   notes
   `here <../docs/neuron-install-guide.md#neuron-conda-packages>`__

.. _1017210:

[1.0.1721.0]
============

Date: 09/22/2020

Summary
-------

-  Various minor improvements to the Pytorch autopartitioner feature
-  Support for the operators aten::constant_pad_nd, aten::meshgrid
-  Improved performance on various torchvision models. Of note are
   resnet50 and vgg16

.. _1015320:

[1.0.1532.0]
============

Date: 08/08/2020

.. _summary-1:

Summary
-------

-  Various minor improvements to the Pytorch autopartitioner feature
-  Support for the aten:ones operator

.. _1015220:

[1.0.1522.0]
============

Date: 08/05/2020

.. _summary-2:

Summary
-------

Various minor improvements.

.. _1013860:

[1.0.1386.0]
============

Date: 07/16/2020

.. _summary-3:

Summary
-------

This release adds auto-partitioning, model analysis and PyTorch 1.5.1
support, along with a number of new operators

Major New Features
------------------

-  Support for Pytorch 1.5.1
-  Introduce an automated operator device placement mechanism in
   torch.neuron.trace to run sub-graphs that contain operators that are
   not supported by the neuron compiler in native PyTorch. This new
   mechanism is on by default and can be turned off by adding argument
   fallback=False to the compiler arguments.
-  Model analysis to find supported and unsupported operators in a model

Resolved Issues
---------------

.. _1011680:

[1.0.1168.0]
============

Date 6/11/2020

.. _summary-4:

Summary
-------

.. _major-new-features-1:

Major New Features
------------------

.. _resolved-issues-1:

Resolved Issues
---------------

Known Issues and Limitations
----------------------------

.. _1010010:

[1.0.1001.0]
============

Date: 5/11/2020

.. _summary-5:

Summary
-------

Additional PyTorch operator support and improved support for model
saving and reloading.

.. _major-new-features-2:

Major New Features
------------------

-  Added Neuron Compiler support for a number of previously unsupported
   PyTorch operators. Please see `Neuron-cc PyTorch
   Operators <./neuron-cc-ops/neuron-cc-ops-pytorch.md>`__ for the
   complete list of operators.
-  Add support for torch.neuron.trace on models which have previously
   been saved using torch.jit.save and then reloaded.

.. _resolved-issues-2:

Resolved Issues
---------------

.. _known-issues-and-limitations-1:

Known Issues and Limitations
----------------------------

.. _108250:

[1.0.825.0]
===========

Date: 3/26/2020

.. _summary-6:

Summary
-------

.. _major-new-features-3:

Major New Features
------------------

.. _resolved-issues-3:

Resolved Issues
---------------

.. _known-issues-and-limitations-2:

Known Issues and limitations
----------------------------

.. _107630:

[1.0.763.0]
===========

Date: 2/27/2020

.. _summary-7:

Summary
-------

Added Neuron Compiler support for a number of previously unsupported
PyTorch operators. Please see `Neuron-cc PyTorch
Operators <./neuron-cc-ops/neuron-cc-ops-pytorch.md>`__ for the complete
list of operators.

.. _major-new-features-4:

Major new features
------------------

-  None

.. _resolved-issues-4:

Resolved issues
---------------

-  None

.. _106720:

[1.0.672.0]
===========

Date: 1/27/2020

.. _summary-8:

Summary
-------

.. _major-new-features-5:

Major new features
------------------

.. _resolved-issues-5:

Resolved issues
---------------

-  Python 3.5 and Python 3.7 are now supported.

.. _known-issues-and-limitations-3:

Known issues and limitations
----------------------------

Other Notes
-----------

.. _106270:

[1.0.627.0]
===========

Date: 12/20/2019

.. _summary-9:

Summary
-------

This is the initial release of torch-neuron. It is not distributed on
the DLAMI yet and needs to be installed from the neuron pip repository.

Note that we are currently using a TensorFlow as an intermediate format
to pass to our compiler. This does not affect any runtime execution from
PyTorch to Neuron Runtime and Inferentia. This is why the neuron-cc
installation must include [tensorflow] for PyTorch.

.. _major-new-features-6:

Major new features
------------------

.. _resolved-issues-6:

Resolved issues
---------------

.. _known-issues-and-limitations-4:

Known issues and limitations
----------------------------

Models TESTED
~~~~~~~~~~~~~

The following models have successfully run on neuron-inferentia systems

1. SqueezeNet
2. ResNet50
3. Wide ResNet50

Pytorch Serving
~~~~~~~~~~~~~~~

In this initial version there is no specific serving support. Inference
works correctly through Python on Inf1 instances using the neuron
runtime. Future releases will include support for production deployment
and serving of models

Profiler support
~~~~~~~~~~~~~~~~

Profiler support is not provided in this initial release and will be
available in future releases

Automated partitioning
~~~~~~~~~~~~~~~~~~~~~~

Automatic partitioning of graphs into supported and non-supported
operations is not currently supported. A tutorial is available to
provide guidance on how to manually parition a model graph. Please see
`Manual partitioning of Resnet50 in a Jupyter
Notebook <../docs/pytorch-neuron/tutorial-manual-partitioning.md>`__

PyTorch dependency
~~~~~~~~~~~~~~~~~~

Currently PyTorch support depends on a Neuron specific version of
PyTorch v1.3.1. Future revisions will add support for 1.4 and future
releases.

Trace behavior
~~~~~~~~~~~~~~

In order to trace a model it must be in evaluation mode. For examples
please see `Using Neuron to run Resnet50
inference <../docs/pytorch-neuron/tutorial-compile-infer.md>`__

Six pip package is required
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Six package is required for the torch-neuron runtime, but it is not
modeled in the package dependencies. This will be fixed in a future
release.

Multiple NeuronCore support
~~~~~~~~~~~~~~~~~~~~~~~~~~~

If the num-neuroncores options is used the number of cores must be
manually set in the calling shell environment variable for compilation
and inference.

For example: Using the keyword argument
compiler_args=['—num-neuroncores', '4'] in the trace call, requires
NEURONCORE_GROUP_SIZES=4 to be set in the environment at compile time
and runtime

CPU execution
~~~~~~~~~~~~~

At compilation time a constant output is generated for the purposes of
tracing. Running inference on a non neuron instance will generate
incorrect results. This must not be used. The following error message is
generated to stderr:

::

   Warning: Tensor output are ** NOT CALCULATED ** during CPU execution and only
   indicate tensor shape

.. _other-notes-1:

Other notes
-----------

-  Python version(s) supported:

   -  3.6

-  Linux distribution supported:

   -  DLAMI Conda 26.0 and beyond running on Ubuntu 16, Ubuntu 18,
      Amazon Linux 2 (using Python 3.6 Conda environments)
   -  Other AMIs based on Ubuntu 16, 18
   -  For Amazon Linux 2 please install Conda and use Python 3.6 Conda
      environment
