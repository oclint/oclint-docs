Reporters Module
================

After the analysis process, for each of the violations detected, we know the detail information of the node, the rule, and sometimes the diagnostic message. Reporters will take the information, and convert them into human readable reporters.

.. note::

    In some cases, the outputs are not directly read by people, instead they will be rendered by other tools for better representation. For example, continuous integration systems can understand a specific type of output, and convert it into graphic interface on its dashboard.
