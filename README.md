### Running Platform
Ubuntu 20.04 in Virtual Machine Software `VMware Workstation 16 PRO`.  
FPGA: Arty A7 35T  
### Recur perf_get_mcycle64() Issue  
1. Clone this repository and move it into `CFU-Playground/proj`.  
2. Enter directory `CFU-Playground` and run `make enter-sf`.  
3. Enter directory `proj/my_kws`.

As `Makefile` line 48 shows, we can uncomment or comment `DEFINES += PRINT_CONV_INNERMOST_CYCLE` to utilize perf counters or not.  
In `src/tensorflow/lite/kernels/internal/reference/integer_ops/conv.h` line 105, we can find out how the macro above is used.  

4. After changing `Makefile`, run `make clean && make prog` to program the bitstream onto the board.
5. Run `make load` to build the RISCV program and load it onto the board.
6. Run golden tests to get total cycles.

### Possible Result  
The following result is what I got by following the above steps.  

total cycles without perf count:  
pdti8: 215M  
mnv2:  1104M  
kws:   84M  

total cycles with perf count:  
pdti8: 175M  
mnv2:  965M  
kws:   75M
