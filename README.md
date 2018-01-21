# Mandel_HLS

![screenshot](https://github.com/delhatch/Mandel_HLS/blob/master/system_diagram_8_engines.JPG)

Author

Del Hatch

** Exploring HLS

This project was to use custom IP generated by Vivado HLS. This Xilinx tool creates HDL from C code.

I also wanted to explore passing, processing and receiving floating point values. My default number system is fractional integers, so I wanted to see how performance is impacted by processing floats.

The result is that Vivado HLS did a good job in creating IP with a small footprint. The problem (a speed problem) comes from the resulting large number of cycles (3 or 4 cycles at 100 MHz) required to do a fp multiply.

I would normally write Verilog HDL directly instead using a higher-level language. But using the HLS tool did allow me to create floating point IP very quickly and easily.

** Memory-mapped VGA display

The project uses the memory-mapped VGA display I used in other projects. See those for more details. 

** Performance

As you can see, the sythesized floating point engine requires 24 cycles for each loop. In comparison, the fixed-point implementation I wrote (see the Zedboard_Mandel project) requires just 4 cycles per loop. Quite a penalty for floating point, and perhaps for using C code to generate the IP as well.

![screenshot](https://github.com/delhatch/Mandel_HLS/blob/master/cycles.JPG)

Therefore, even with 8 engines, the Mandelbrot image takes 1.4 seconds to create. This is better than the pure-ARM version that required 2.2 seconds to compute a frame, but not improvement as I expected.

The integer version, written in Verilog, and writing directly to the VGA frame buffer (no ARM processor involved) was able to achieve 18.6 frames per second.

** Improvements

This project is mainly a demonstration of how to use Vivado HLS to create IP, and it was successful in that regard.

One area for focus would be to try to speed up the floating-point engine, but this might not be possible given how many cycles floating-point calculations require.

However, even with the relatively slow engines compared to fixed-point engines, the Zynq processor's C code is the bottleneck. The engines need to be able to access the VGA frame buffer directly, as seen in the Zedboard_Mandel project.




