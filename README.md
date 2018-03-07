# LEPCC - Limited Error Point Cloud Compression

Based on LERC (see https://github.com/Esri/lerc)

This repository contains a 3D point cloud compression module written in C++. It has a C API, and a test program. For the C API, see src/include/lepcc_c_api.h. For the test program that uses the C API, see src/Test_C_Api.cpp. 


## Features

* Compression of 3D point cloud tiles.

* Caller specifies max error or tolerance for each x, y, and z.

* Compression ~10x for (x, y, z) for 1 cm accuracy. (On the datasets we have tested so far. It is data dependent.)

* Compression ~3x for RGB (if points come with color). Colors are clustered in RGB space and then quantized to 8 bit. 
  The 8 bit color indexes can get Huffman encoded. 

* Compression 1-2x for Las intensity, lossless. Better than gzip. Detect upscale factor if any, revert it, bit stuff. 

* Compression for Las return, class, or other flag bytes, lossless. Tries Huffman and bit stuff, takes the better. 

* Encoding speed ~1 ms per tile (for geometry).

* Encoding speed ~2 ms per tile (for geometry + color).

* Decoding speed ~1/4 ms per tile.

* Good for streaming.

* Shares low level code with Lerc raster compression.

* Has the other advantages of Lerc: No dependencies on other libraries or packages, 
  easy to port the decoder to other languages such as JS, Python, C# etc. 


## Issues 

Find a bug or want to request a new feature? Please let us know by submitting an issue. 


## Licensing 

Copyright 2016 Esri 
Licensed under the Apache License, Version 2.0 (the "License"); 
you may not use this file except in compliance with the License. 
You may obtain a copy of the License at 
http://www.apache.org/licenses/LICENSE-2.0 
Unless required by applicable law or agreed to in writing, software 
distributed under the License is distributed on an "AS IS" BASIS, 
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. 
See the License for the specific language governing permissions and 
limitations under the License. 
A copy of the license is available in the repository's [license.txt]( https://raw.github.com/Esri/lepcc/master/license.txt) file. 

