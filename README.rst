=======
tinybgw
=======

Pure-Python implementation of a `comparison algorithm <https://nillion.pub/comparison.pdf>`__ based on secure multi-party computation (MPC).

|pypi| |readthedocs| |actions|

.. |pypi| image:: https://badge.fury.io/py/tinybgw.svg
   :target: https://badge.fury.io/py/tinybgw
   :alt: PyPI version and link.

.. |readthedocs| image:: https://readthedocs.org/projects/tinybgw/badge/?version=latest
   :target: https://tinybgw.readthedocs.io/en/latest/?badge=latest
   :alt: Read the Docs documentation status.

.. |actions| image:: https://github.com/NillionNetwork/tinybgw/workflows/lint-test-cover-docs/badge.svg
   :target: https://github.com/NillionNetwork/tinybgw/actions/workflows/lint-test-cover-docs.yml
   :alt: GitHub Actions status.

Installation and Usage
----------------------

This library is available as a `package on PyPI <https://pypi.org/project/tinybgw>`__:

.. code-block:: bash

    python -m pip install tinybgw

The library can be imported in the usual way:

.. code-block:: python

    import tinybgw
    from tinybgw import *

Basic Example
^^^^^^^^^^^^^

This implementation includes the emulation of a network comprised of computing nodes. We can either 
deploy a network with any Galois field we want. In this example, we will show an example with 3 
nodes and security threshold set to 1.

.. code-block:: python

    >>> N = 3; T = 1; field = Field(65267)

To kick things off, let's initialize the network:

.. code-block:: python

    >>> network = Network(N, T, field)

We can share a secret 7 named "my_secret":

.. code-block:: python

    >>> network.share([7], "my_secret")

For a deeper dive, please check the `demos` folder.

Development
-----------
All installation and development dependencies are fully specified in ``pyproject.toml``. The ``project.optional-dependencies`` object is used to `specify optional requirements <https://peps.python.org/pep-0621>`__ for various development tasks. This makes it possible to specify additional options (such as ``docs``, ``lint``, and so on) when performing installation using `pip <https://pypi.org/project/pip>`__:

.. code-block:: bash

    python -m pip install .[docs,lint]

Documentation
^^^^^^^^^^^^^
The documentation can be generated automatically from the source files using `Sphinx <https://www.sphinx-doc.org>`__:

.. code-block:: bash

    python -m pip install .[docs]
    cd docs
    sphinx-apidoc -f -E --templatedir=_templates -o _source ../src && make html

Testing and Conventions
^^^^^^^^^^^^^^^^^^^^^^^
All unit tests are executed and their coverage is measured when using `pytest <https://docs.pytest.org>`__ (see the ``pyproject.toml`` file for configuration details):

.. code-block:: bash

    python -m pip install .[test]
    python -m pytest

Style conventions are enforced using `Pylint <https://pylint.readthedocs.io>`__:

.. code-block:: bash

    python -m pip install .[lint]
    python -m pylint src/tinybgw

Contributions
^^^^^^^^^^^^^
In order to contribute to the source code, open an issue or submit a pull request on the `GitHub page <https://github.com/NillionNetwork/tinybgw>`__ for this library.

Versioning
^^^^^^^^^^
The version number format for this library and the changes to the library associated with version number increments conform with `Semantic Versioning 2.0.0 <https://semver.org/#semantic-versioning-200>`__.

Publishing
^^^^^^^^^^
This library can be published as a `package on PyPI <https://pypi.org/project/tinybgw>`__ by a package maintainer. First, install the dependencies required for packaging and publishing:

.. code-block:: bash

    python -m pip install .[publish]

Ensure that the correct version number appears in ``pyproject.toml``, and that any links in this README document to the Read the Docs documentation of this package (or its dependencies) have appropriate version numbers. Also ensure that the Read the Docs project for this library has an `automation rule <https://docs.readthedocs.io/en/stable/automation-rules.html>`__ that activates and sets as the default all tagged versions. Create and push a tag for this version (replacing ``?.?.?`` with the version number):

.. code-block:: bash

    git tag ?.?.?
    git push origin ?.?.?

Remove any old build/distribution files. Then, package the source into a distribution archive:

.. code-block:: bash

    rm -rf build dist src/*.egg-info
    python -m build --sdist --wheel .

Finally, upload the package distribution archive to `PyPI <https://pypi.org>`__:

.. code-block:: bash

    python -m twine upload dist/*
