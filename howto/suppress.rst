Suppress OCLint Warnings
========================

There are two scenarios you might want to suppress an warning:

* the standard for certain code measurement is controversial
* it is a false positive

There are several methods you could consider to suppress OCLint rule violations:

* If the warning you need to suppress also appeals to other OCLint users, e.g. a false positive

  * Patch test cases, amend the rule to make tests pass, and submit a pull request. Your help would be greatly appreciated by everyone
  * Open an issue with your code snippet on github or discuss with us in the mailing list

* If the standard of your project is slightly different from OCLint default settings

  * Consider `change rules' thresholds <thresholds.html>`_ to best fit the current environment

* If certain rules are really annoying for your projects

  * `Remove them from the rule search path <selectrules.html>`_
  * `Add these rules into blacklist <selectrules.html>`_

* If it is a case-by-case thing, and only particular places need to be suppressed

  * `Use annotations <suppress.html#annotations>`_
  * `Use !OCLint comment <suppress.html#oclint-comment>`_

Annotations
-----------

By adding annotations to the source code, you can communicate with OCLint and order it to discard certain types of rule violations within a context-based range.

Annotation Syntax
^^^^^^^^^^^^^^^^^

You can suppress one rule like this::

  __attribute__((annotate("oclint:suppress[unused method parameter]")))


Or, you can suppress multiple rules at the same time, like this::

  __attribute__((annotate("oclint:suppress[high cyclomatic complexity]"), annotate("oclint:suppress[high npath complexity]"), annotate("oclint:suppress[high ncss method]")))

OCLint also allows you to suppress all rules with a shortcut::

  __attribute__((annotate("oclint:suppress")))


Effective Range
---------------

Annotations are added to a particular declaration of the source code, and each suppress has the impact on the same scope of the declaration, usually this scope covers the current declaration itself and all its children. 

For example, if an annotation is added to a method declaration, then the suppress effects the method, its entire content, including all its parameters, statements, expression, local variables, and so on.


Examples
^^^^^^^^

.. code-block:: objective-c

  bool __attribute__((annotate("oclint:suppress"))) aMethod(int aParameter)
  {
      // warnings within this method are suppressed at all
      // like unused aParameter variable and empty if statement
      if (1) {}

      return true;
  }

  - (IBAction)turnoverValueChanged:
      (id) __attribute__((annotate("oclint:suppress[unused method parameter]"))) sender
      // suppress sender variable
  {
      int i; // won't suppress this one
      [self calculateTurnover];
  }

  - (void)dismissAllViews:(id)currentView parentView:(id)parentView
     __attribute__((annotate("oclint:suppress"))) 
     // again, suppress the warnings for entire method
  {
      [self dismissTurnoverView];
      // plus 30+ lines of code of dismissing other views
  }

!OCLint Comment
---------------

Alternatively, the warnings of a specific line can be suppressed by appending ``//!OCLint`` comment, for example:

.. code-block:: objective-c

    void a() {
        int unusedLocalVariable; //!OCLINT
    }

As a good practice, it's highly recommend to add the reasoning for the comment, like:

.. code-block:: c++

    int Results::numberOfWarnings()
    {
        std::lock_guard<std::mutex> lock(_mutex); //!OCLint(FP - meant to be unused)
        //Everything after the letter 't' is ignored, but just for better readability
        return _compilerWarningSet->numberOfViolations();
    }

Note that comment-based suppress doesn't care the violation type nor number of violations, it simply ignore every warnings on that specific line. So the comment is expected to be on the same line as the violation. For example, when ``empty if statement`` is supposed to be suppressed, ``//!OCLint`` needs to be put on the line containing ``if`` statement, e.g.:

.. code-block:: c++

    if (true) //!OCLint goes here
    {
        // it is empty
    }
