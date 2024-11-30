# About
This repository works as a toolset and guide for a free open-source way of converting VHDL to Verilog code using [yosys](https://github.com/YosysHQ/yosys) and [GHDL](https://github.com/ghdl/ghdl).


# Installation instructions

## Dependencies
The needed dependencies for a Ubuntu 20.04 Server is given in *dependencies.sh*. This can be done in a terminal `./dependencies.sh`

## Installing yosys and GHDL
yosys and ghdl are added as submodules. Be sure to run `git submodule update --init` from within this folder.

	$ export MAKEFLAGS=-jn
where n is the number of cores you want to use. This allows for using parallel compilation.

	$ ./install_yosys.sh
	$ ./install_ghdl.sh

编译yosys可能遇到如下问题：

```bash
passes/sat/freduce.cc:457:55: error: ‘numeric_limits’ is not a member of ‘std’
  457 |                                 out_depth[idx] = std::numeric_limits<int>::max();
      |                                                       ^~~~~~~~~~~~~~
passes/sat/freduce.cc:457:70: error: expected primary-expression before ‘int’
  457 |                                 out_depth[idx] = std::numeric_limits<int>::max();
      |                                                                      ^~~
```

需要在文件 `./yosys/passes/sat/freduce.cc` 的开头添加`#include <limits>`

# Test
Run `./test.synth.sh` to test a synthesis of a test example. This should generate a file called *synth.v* in the current folder.
