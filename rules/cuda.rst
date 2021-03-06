Cuda
====

BranchDivergence
----------------

**Since: 0.15**

**Name: branch divergence**

Branch divergence is quite expensive and needs to be avoided as much as possible.

This rule is defined by the following class: `oclint-rules/rules/cuda/CudaBranchDivergenceRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/cuda/CudaBranchDivergenceRule.cpp>`_

**Example:**


.. code-block:: cuda

    if (threadIdx.x == 0) {
        foo();
    } else {
        bar();
    }
    // This would cause branch divergence,
    // as while the first thread working on `foo()`,
    // the rest of the threads sit idle;
    // similarly, when the others running `bar()`,
    // the first thread now stall.
    // Go https://bit.ly/2ZxYJVR to read more.

    


.. Generated on Sat Mar  6 11:00:31 2021

