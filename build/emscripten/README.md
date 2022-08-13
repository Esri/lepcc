# How to build with Emscripten in Linux (we used Ubuntu)

A quick guide how to
* run the C++ Lepcc decoder in a web browser
* from the Lepcc C API, build a Lepcc decode API for web assembly or wasm. 

## Run the Lepcc decoder in a webpage

- install [Emscripten](https://emscripten.org/)
- open a terminal or cmd shell
- in emsdk/
  - source ./emsdk_env.sh
- In the Lepcc main folder (has the CMakeLists.txt), 
  - emcc --clear-cache
  - emcmake cmake .
  - emmake make
  - (should have created liblepcc.a)
  - emcc liblepcc.a src/Test_C_Api.cpp -o lepcc.html --preload-file testData -s ALLOW_MEMORY_GROWTH=1
  - (should have created lepcc.html)
  - python3 -m http.server 8000
- open a web browser and go to http://localhost:8000
  - open lepcc.html
  - (should run the Lepcc test program, say it decoded 106 points with 0 errors)
  - close the browser
  - in the terminal, use Ctrl-C to quit

## Build a wasm Lepcc decode API

- in include/lepcc_c_api.h, uncomment #define USE_EMSCRIPTEN
- follow the same steps as above till "emmake make", then
  - emcc liblepcc.a src/lepcc_c_api_impl.cpp -o lepcc-wasm.js -s MODULARIZE=1 -O3 -s ALLOW_MEMORY_GROWTH=1 -s EXPORTED_FUNCTIONS="['_malloc','_free']"
  - (should create .js and .wasm files that expose the lepcc decode functions from the Lepcc C API callable from JS)
