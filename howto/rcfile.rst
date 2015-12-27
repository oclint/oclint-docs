Preserve Configurations
=======================

OCLint can load configuration files (``/etc/oclint``, ``~/.oclint`` and ``.oclint``) and populates arguments from there.

There are three levels of configurations files-

System Configuration File
    is saved into ``$(/path/to/bin/oclint)/../etc/oclint``, when ``oclint`` main binary is installed into ``/bin/oclint`` for the most common case, then this is the regular ``/etc/oclint`` file. The configurations saved into this file change the behaviors of OCLint throughout the entire system.
User Configuration File
    is preserved to ``~/.oclint``, which is under the home directory of the current user. User preferences can be saved into this file, and only scope the current user. Configurations in this file can override the existing ones in the system configuration file.
Project Configuration File
    is usually placed at the root folder of the project, where ``oclint`` is usually invoked from. This file is scanned and configurations are only for the current project. Configurations in this file can override the ones in user configuration file, and in sequence, override the ones in system configuration file.

Arguments passing to the command line invocation would override the ones in the configuration file.


The acceptable configuration file is written in YAML format, with the following available options:

============================ ============================ =============================
Option                       Type                         Mapping Command Option
============================ ============================ =============================
rules                        List of strings              -rule
disable-rules                List of strings              -disable-rule
rule-paths                   List of strings              -R
rule-configurations          List of associative arrays   -rc
output                       String                       -o
report-type                  String                       -report-type
max-priority-1               Integer                      -max-priority-1
max-priority-2               Integer                      -max-priority-2
max-priority-3               Integer                      -max-priority-3
enable-global-analysis       Boolean                      -enable-global-analysis
enable-clang-static-analyzer Boolean                      -enable-clang-static-analyzer
============================ ============================ =============================


An example of a ``.oclint`` file might looks like this::

    disable-rules:
      - LongLine
    rulePaths:
      - /etc/rules
    rule-configurations:
      - key: CYCLOMATIC_COMPLEXITY
        value: 15
      - key: NPATH_COMPLEXITY
        value: 300
    output: oclint.xml
    report-type: xml
    max-priority-1: 20
    max-priority-2: 40
    max-priority-3: 60
    enable-clang-static-analyzer: false


.. seealso::

    `OCLint manual <../manual/oclint.html>`_
        Manual for OCLint main binary

    `Customizing Thresholds <thresholds.html>`_
        Documentation of changing the thresholds in order to modify the behavior of the tool

    `Rule Selection <selectrules.html>`_
        Documentation of picking up the right rules for analysis

    `Reporter Selection <selectreporters.html>`_
        Documentation of selecting the reporters for output
