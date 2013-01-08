Using oclint
============

When you invoke OCLint, it normally does rule loading, compilation, analysis, and report generation. The options allow you to change the behavior of each step to certain ways that meet your requirement.

See all supported options in OCLint |release| by typing ``oclint -help``::

    USAGE: oclint [options] <source0> [... <sourceN>]

    OPTIONS:
      -R=<directory>              - Add directory to rule loading path
      -fatal-assembler-warnings   - Consider warnings as error
      -help                       - Display available options (-help-hidden for more)
      -max-priority-1=<threshold> - The max allowed number of priority 1 violations
      -max-priority-2=<threshold> - The max allowed number of priority 2 violations
      -max-priority-3=<threshold> - The max allowed number of priority 3 violations
      -o=<path>                   - Write output to <path>
      -p=<string>                 - Build path
      -rc=<paramemter>=<value>    - Override the default baheviour of rules
      -stats                      - Enable statistics output from program
      Choose report type:
        -text                     - Plain text report
        -html                     - HTML formatted report
      -version                    - Display the version of this program

    -p <build-path> is used to read a compile command database.

        For example, it can be a CMake build directory in which a file named
        compile_commands.json exists (use -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
        CMake option to get this output). When no build path is specified,
        a search for compile_commands.json will be attempted through all
        parent paths of the first input file . See:
        http://clang.llvm.org/docs/HowToSetupToolingForLLVM.html for an
        example of setting up Clang Tooling on a source tree.

    <source0> ... specify the paths of source files. These paths are
        looked up in the compile command database. If the path of a file is
        absolute, it needs to point into CMake's source tree. If the path is
        relative, the current working directory needs to be in the CMake
        source tree and the file must be in a subdirectory of the current
        working directory. "./" prefixes in the relative files will be
        automatically removed, but the rest of a relative path must be a
        suffix of a path in the compile command database.

    For more information, please visit http://oclint.org
