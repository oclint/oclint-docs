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

OCLint is pre-installed on OS X images, however, not on linux images, so we provide a script to automate the installation and set it up for you. Feel free to review the `contents of the script <https://raw.githubusercontent.com/ryuichis/oclint-cpp-travis-ci-examples/master/oclint-ci-install.sh>`_ before using it.

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

C++/qmake
---------

Travis, qmake and OCLint go together fine.

Here is a complete `travis.yml` of a minimal project, consisting out of a single Qt Project (`.pro`) file and a single `main.cpp` file:

.. code-block:: yaml

    language: cpp
    compiler: gcc
    sudo: required

    install:
      # install prerequisites of OCLint
      - sudo add-apt-repository ppa:ubuntu-toolchain-r/test --yes
      - sudo apt-get update -qq 
      - sudo apt-get install -qq libstdc++6-4.7-dev  
      # install OCLint
      - wget https://github.com/oclint/oclint/releases/download/v0.10.3/oclint-0.10.3-x86_64-linux-3.13.0-74-generic.tar.gz
      - tar -zxf oclint-0.10.3-x86_64-linux-3.13.0-74-generic.tar.gz

    script: 
      # Build the only .pro file in the folder (not necessary for OCLint)
      - qmake
      - make
      # OCLint
      - ./oclint-0.10.3/bin/oclint main.cpp -- -c

The example above can be found 
`here <https://github.com/richelbilderbeek/travis_qmake_gcc_cpp98_oclint>`_, where it is explained in more detail.

Other examples can be found in 
`a Travis C++ tutorial <https://github.com/richelbilderbeek/travis_cpp_tutorial>`_.
