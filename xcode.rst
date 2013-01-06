.. _xcode-oclint:

Xcode Project Inspection
========================

We have two experimental approaches to inspect on Xcode project. One works in an ugly way, the other is under development for user experiences improvement.

The UGLY approach
-----------------

In this approach, what we do here is simply assembling all parameters we need to invoke OCLint for a Xcode project. For a Xcode project, usually we need the target architecture, system root (target SDK), include search paths, and framework search paths, of course, plus the files we are going to inspect.

It looks like this when we get all of these parameters together.

.. code-block:: bash

    #! /bin/bash

    LANGUAGE=objective-c
    ARCH=armv7
    SYSROOT=/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS5.0.sdk
    CLANG_INCLUDE=/usr/lib/clang/3.0/include
    PCH_PATH=target-Prefix.pch
    FRAMEWORKS=''

    INCLUDES=''
    for folder in `find . -type d`
    do
      INCLUDES="$INCLUDES -I $folder"
    done

    FILES=''
    for file in `find . -name "*.m"`
    do
      FILES="$FILES $file"
    done

    oclint -x $LANGUAGE -arch $ARCH -isysroot=$SYSROOT -I $CLANG_INCLUDE $INCLUDES -include $PCH_PATH $FILES

You can create an executable bash file based on the template above, save it in your Xcode project folder, modify to fit your needs, and just call

.. code-block:: bash

    ./oclint-xcode.sh

to kick-off the inspection.

A Better Approach
-----------------

As all information we need to invoke OCLint is configured in Xcode project’s configuration file projectname.xcodeproj/project.pbxproj, the better approach is obviously get all these parameters from this configuration file.

Currently, we are working on this approach as a Ruby project. We use pbxproject gem to parse the information we need, and gli gem for command line options.
