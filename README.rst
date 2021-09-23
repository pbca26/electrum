Electrum - Lightweight Bitcoin client
=====================================

::

  Licence: MIT Licence
  Author: Thomas Voegtlin
  Language: Python (>= 3.6)
  Homepage: https://electrum.org/


.. image:: https://api.cirrus-ci.com/github/spesmilo/electrum.svg?branch=master
    :target: https://cirrus-ci.com/github/spesmilo/electrum
    :alt: Build Status
.. image:: https://coveralls.io/repos/github/spesmilo/electrum/badge.svg?branch=master
    :target: https://coveralls.io/github/spesmilo/electrum?branch=master
    :alt: Test coverage statistics
.. image:: https://d322cqt584bo4o.cloudfront.net/electrum/localized.svg
    :target: https://crowdin.com/project/electrum
    :alt: Help translate Electrum online





Getting started
===============

(*If you've come here looking to simply run Electrum,* `you may download it here`_.)

.. _you may download it here: https://electrum.org/#download

Electrum itself is pure Python, and so are most of the required dependencies,
but not everything. The following sections describe how to run from source, but here
is a TL;DR::

    sudo apt-get install libsecp256k1-0
    python3 -m pip install --user .[gui,crypto]


Not pure-python dependencies
----------------------------

If you want to use the Qt interface, install the Qt dependencies::

    sudo apt-get install python3-pyqt5

For elliptic curve operations, `libsecp256k1`_ is a required dependency::

    sudo apt-get install libsecp256k1-0

Alternatively, when running from a cloned repository, a script is provided to build
libsecp256k1 yourself::

    sudo apt-get install automake libtool
    ./contrib/make_libsecp256k1.sh

Due to the need for fast symmetric ciphers, `cryptography`_ is required.
Install from your package manager (or from pip)::

    sudo apt-get install python3-cryptography


If you would like hardware wallet support, see `this`_.

.. _libsecp256k1: https://github.com/bitcoin-core/secp256k1
.. _pycryptodomex: https://github.com/Legrandin/pycryptodome
.. _cryptography: https://github.com/pyca/cryptography
.. _this: https://github.com/spesmilo/electrum-docs/blob/master/hardware-linux.rst

Running from tar.gz
-------------------

If you downloaded the official package (tar.gz), you can run
Electrum from its root directory without installing it on your
system; all the pure python dependencies are included in the 'packages'
directory. To run Electrum from its root directory, just do::

    ./run_electrum

You can also install Electrum on your system, by running this command::

    sudo apt-get install python3-setuptools python3-pip
    python3 -m pip install --user .

This will download and install the Python dependencies used by
Electrum instead of using the 'packages' directory.
It will also place an executable named :code:`electrum` in :code:`~/.local/bin`,
so make sure that is on your :code:`PATH` variable.


Development version (git clone)
-------------------------------

Check out the code from GitHub::

    git clone git://github.com/spesmilo/electrum.git
    cd electrum
    git submodule update --init

Run install (this should install dependencies)::

    python3 -m pip install --user -e .


Create translations (optional)::

    sudo apt-get install python-requests gettext
    ./contrib/pull_locale

Finally, to start Electrum::

    ./run_electrum



Creating Binaries
=================

Linux (tarball)
---------------

See :code:`contrib/build-linux/sdist/README.md`.


Linux (AppImage)
----------------

See :code:`contrib/build-linux/appimage/README.md`.


Mac OS X / macOS
----------------

See :code:`contrib/osx/README.md`.


Windows
-------

See :code:`contrib/build-wine/README.md`.


Android
-------

See :code:`contrib/android/Readme.md`.


Contributing
============

Any help testing the software, reporting or fixing bugs, reviewing pull requests
and recent changes, writing tests, or helping with outstanding issues is very welcome.
Implementing new features, or improving/refactoring the codebase, is of course
also welcome, but to avoid wasted effort, especially for larger changes,
we encourage discussing these on the issue tracker or IRC first.

Besides `GitHub`_, most communication about Electrum development happens on IRC, in the
:code:`#electrum` channel on Libera Chat. The easiest way to participate on IRC is
with the web client, `web.libera.chat`_.


.. _web.libera.chat: https://web.libera.chat/#electrum
.. _GitHub: https://github.com/spesmilo/electrum

AuxPow support
-------
https://github.com/namecoin/electrum-nmc/commits/auxpow?after=840cdc07988c232a1d988bfceecdb815af25aad3+34&branch=auxpow


HW wallet integration results
-------
(1) Legacy address - pass, no issues, both send and receive
(2) P2SH Segwit - fail, receive is working but an attempt to send a transaction yields the following error 'the transaction was rejected by network rules.\n\n64: no-witness-yet\n[0200000000010128a6e071b524e2af67ae3d91af5d7997427a2867b0547a05e25923b710c70c35010000001716001491387df0268e77a84928e2700875dd74d2d81690fdffffff02102700000000000017a914394c53a52f512b5af0d3b144e891973f51766ad487102700000000000017a914da971ee07682b57315ad30ab1becfeb8125da1c38702483045022100c2e217c49de620502e4f7f3effea89b8fe69d8f5234f3712f48687ab473eafe802206d73bb49f8f4a1706c27e97947a507561c79b1fb7ba0bfa49e9aed55369d2ff70121020eb18e95fd3bf6b4f6a61623277a02a1a16b3f841e26f7cf41cb79af3ca24e01c5090300'
Quick search in Google points to a possible witness not enabled on-chain yet
https://www.google.com/search?q=error+no-witness-yet&oq=error+no-witness-yet&aqs=chrome..69i57j33i160.2894j0j7&sourceid=chrome&ie=UTF-8
After closely looking at SFUSD code there's no Segwit height or timestamp activation set in https://github.com/pbcllc/sfusd-core/blob/master/src/chainparams.cpp#L161
e.g. https://github.com/bitcoin/bitcoin/blob/master/src/chainparams.cpp#L74
(3) Native Segwit - not tested due to missing on-chain witness activation params

Note: addresses displayed on HW device screen are different than what a user sees in GUI. Change in HW vendor firmware are required in order to properly derive and display correct addresses on device screen. Otherwise users will be unable to verify what are they signing.