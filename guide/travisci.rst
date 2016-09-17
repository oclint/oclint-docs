Using OCLint with Travis CI
===========================

Objective-C/Xcode
-----------------

The script you have for `running OCLint for Xcode <xcodebuild.html>`_ can be reused here.

.. code-block:: yaml

    language: objective-c
    osx_image: xcode7.2
    before_install:
    - brew cask uninstall oclint
    - brew tap oclint/formulae
    - brew install oclint
    script:
      - xcodebuild | tee xcodebuild.log
      - oclint-xcodebuild
      - oclint-json-compilation-database

An example can be found at this `github repository <https://github.com/ryuichis/oclint-objc-travis-ci-examples>`_.

C++/CMake
---------

OCLint is pre-installed on macOS images, however, not on linux images, so we provide a script to automate the installation and set it up for you. Feel free to review the `contents of the script <https://raw.githubusercontent.com/ryuichis/oclint-cpp-travis-ci-examples/master/oclint-ci-install.sh>`_ before using it.

.. code-block:: yaml

    os:
    - linux
    - osx
    language: cpp
    sudo: required
    dist: trusty
    osx_image: xcode7.2
    before_install:
    - if [ $TRAVIS_OS_NAME == osx ]; then brew update && brew install cmake; fi
    - if [ $TRAVIS_OS_NAME == linux ]; then eval "$(curl -sL https://raw.githubusercontent.com/ryuichis/oclint-cpp-travis-ci-examples/master/oclint-ci-install.sh)"; fi
    script:
      - mkdir build
      - cd build
      - cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=ON ..
      - cd ..
      - cp build/compile_commands.json .
      - oclint-json-compilation-database

An example can be found at this `github repository <https://github.com/ryuichis/oclint-cpp-travis-ci-examples>`_.

