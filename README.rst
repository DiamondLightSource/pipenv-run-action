Pipenv Run Action
=================

Github action to install python and pipenv, checkout the repo, then pipenv
install and run

For example, to clone your repo, install python3.7, install pipenv and
use it to install from the lockfile checking hashes then run pytest:

.. code-block:: yaml

    name: Example action
    jobs:
    tests:
      name: Run pytest
      runs-on: ubuntu-latest
      steps:
        - name: Checkout, pipenv install and run
          uses: dls-controls/pipenv-run-action@v1
          with:
            python-version: "3.7"
            pipenv-install: --dev --deploy
            pipenv-run: pytest

Inputs
------

You can change the behaviour of the action by passing any of the following
arguments in a ``with:`` block.

fetch-depth
~~~~~~~~~~~

Default ``0``. The number of commits to fetch, ``0`` means everything. Passed to
https://github.com/marketplace/actions/checkout but note the different default
value.

submodules
~~~~~~~~~~

Default ``""``. Whether to fetch submodules, ``""`` means no, ``true`` means
yes, and ``recursive`` means yes recursively. Passed to
https://github.com/actions/checkout

python-version
~~~~~~~~~~~~~~

Default ``3.7``. Change the version of python that is installed. Passed to
https://github.com/marketplace/actions/setup-python

pipenv-install
~~~~~~~~~~~~~~

Default ``--dev --deploy``. The options to pass to ``pipenv install``.

pipenv-run
~~~~~~~~~~

Default ``""``. If given, run ``pipenv run`` with these arguments.

allow-editable-installs
~~~~~~~~~~~~~~~~~~~~~~~

Default ``true``. If ``false`` then change references to ``editable`` in
``Pipfile`` and ``Pipfile.lock`` to ``false``. This will make sure wheel builds
of these directories takes place instead of editable installs which are soft
links.
