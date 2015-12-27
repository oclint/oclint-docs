Scaffolding
===========

Rules and reporters classes are designed by contract, meaning they need to inherit their base classes, and implement pure virtual methods, and their source code follow certain structures. So we could scaffold new rules and reporters by copying their templates and replacing the placeholders. In addition, the scaffolding scripts can ease your work by adding the new rule and reporter to the OCLint build pipeline.

This document provides information on how to create rules and reporters with scaffold scripts.

Creating Rules with Scaffolding
-------------------------------

Creating a custom rule can be done with ``scaffoldRule`` script under ``oclint-scripts`` folder.

We could get a list of its options by typing ``./scaffoldRule -h``::

    usage: scaffoldRule [-h] [-t {Generic,SourceCodeReader,ASTVisitor,ASTMatcher}]
                        [-c RULE_CATEGORY] [-n RULE_NAME] [-p {1,2,3}] [--test]
                        [--no-test]
                        class_name

    positional arguments:
      class_name            class name of the rule

    optional arguments:
      -h, --help            show this help message and exit
      -t {Generic,SourceCodeReader,ASTVisitor,ASTMatcher}, --type {Generic,SourceCodeReader,ASTVisitor,ASTMatcher}
      -c RULE_CATEGORY, --category RULE_CATEGORY
      -n RULE_NAME, --name RULE_NAME
      -p {1,2,3}, --priority {1,2,3}
      --test                Generate a test for the new rule (default)
      --no-test             Do not generate a test for the new rule

From where, we could specify the class name, along with the name, type, category and priority of the rule.

Class name is the only required argument. Without explicitly given a rule name, it could be generated according to the class name. The default values of type, category and priority are ``Generic``, ``custom`` and ``3`` respectively.

.. seealso::
    Learn how to choose the proper rule interface from `Rule Module Internals <../internals/rules.html>`_ document.

For example, if we want to create a controversial rule that extracts all switch statements with abstract syntax tree (AST) matcher, we can enter this command in the terminal:

.. code-block:: bash

    ./scaffoldRule AllSwitchStatements -c controversial -t ASTMatcher

Notice we would like scaffold script to populate the rule name and assign the default priority to this rule for us.

The scaffold script will create ``AllSwitchStatementsRule.cpp`` file, and store it in ``controversial`` folder under ``oclint-rules/rules``. The rule will be generated like the following:

.. code-block:: cpp

    #include "oclint/AbstractASTMatcherRule.h"
    #include "oclint/RuleSet.h"

    class AllSwitchStatementsRule : public AbstractASTMatcherRule
    {

    private:
        static RuleSet rules;

    public:
        virtual const string name() const
        {
            return "all switch statements";
        }

        virtual int priority() const
        {
            return 3;
        }

        virtual void callback(const MatchFinder::MatchResult &result)
        {
        }

        virtual void setUpMatcher()
        {
        }

    };

    RuleSet AllSwitchStatementsRule::rules(new AllSwitchStatementsRule());

In addition, related ``CMakeLists.txt`` files will be edited to ensure the new rule will be built along with other existing rules.

A unit test file for this rule is scaffolded along with this process for testing purposes.

Now, the scaffolding is finished, we can refer to `Writing Custom Rules <rules.html>`_ document to fill in the logic for the rule.

Creating Reporters with Scaffolding
-----------------------------------

Scaffolding a reporter is very similar to the rule, but much easier, since it only requires the reporter's class name with an optional argument for specifying the reporter's name. We could also get these options by typing ``./scaffoldReporter -h``::

    usage: scaffoldReporter [-h] [-n REPORTER_NAME] [--tests] [--no-tests]
                            class_name

    positional arguments:
      class_name            class name of the reporter

    optional arguments:
      -h, --help            show this help message and exit
      -n REPORTER_NAME, --name REPORTER_NAME
      --tests               Generate a test for the new reporter (default)
      --no-tests            Do not generate a test for the new reporter

Let's say we want to create a new ColorfulTextReporter, with this script, we could do

.. code-block:: bash

  ./scaffoldReporter ColorfulText -n color

The generated ``ColorfulTextReporter.cpp`` will look like the following:

.. code-block:: cpp

  #include "oclint/Reporter.h"

  class ColorfulTextReporter : public Reporter
  {
  public:
      virtual const string name() const
      {
          return "color";
      }

      virtual void report(Results *results, ostream &out)
      {
      }
  };

  extern "C" Reporter* create()
  {
    return new ColorfulTextReporter();
  }

Sequentially, the ``CMakeLists.txt`` file under ``reporters`` folder will be edited by appending the new reporter.

A unit test file for this reporter is scaffolded along with this process for testing purposes.

Now, we can refer to the `Writing Custom Reporters <reporters.html>`_ document to print out the analysis results.

