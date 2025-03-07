# TFlite-builds

TF lite runtimes to use with birdnet-pi

[![publish-tflite-runtime-wheels](https://github.com/alexbelgium/TFlite-bookworm/actions/workflows/main.yml/badge.svg)](https://github.com/alexbelgium/TFlite-bookworm/actions/workflows/main.yml)

## TFlite runtimes
- Base : Debian bookworm
- Architectures : x86_64 ; aarch64 ; x86_64_non_avx
- Python versions : 3.9 ; 3.10 ; 3.11 ; 3.12

## Flags : architecture specific

| Name of Flag                                | What Does It Do?                                                                 | Impact on TFLite Performance                          | Impact on TFLite Runtime Size                        | Architecture                |
|---------------------------------------------|----------------------------------------------------------------------------------|------------------------------------------------------|-----------------------------------------------------|-----------------------------|
| `--cpu=k8`                                  | Specifies the CPU architecture for x86_64.                                       | No direct impact.                                     | No direct impact.                                    | x86_64                      |
| `--cpu=aarch64 --config=elinux_aarch64`     | Specifies the CPU architecture and configuration for aarch64.                    | No direct impact.                                     | No direct impact.                                    | aarch64                     |
| `--cpu=core2 --copt=-mno-avx --copt=-mno-avx2 --copt=-msse4.2 --copt=-msse4.1` | Specifies the CPU architecture for x86_64 without AVX support. | No direct impact.                                     | No direct impact.                                    | x86_64_noavx                |

## Flags : general

| Name of Flag                                      | What Does It Do?                                                          | Impact on TFLite Performance                          | Impact on TFLite Runtime Size                        | Architecture|
|---------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------|------------------------------------------------------|-------------|
| `--define=tflite_enable_xnnpack=true`             | Enables XNNPACK, a highly optimized library for neural network inference. | Improves performance for floating-point models.       | Slight increase in binary size.                      | All         |
| `--define=xnnpack_enable_subgraph_reshaping=true` | Enables subgraph reshaping in XNNPACK.                                    | Enhances performance by optimizing subgraph execution.| Minimal impact on binary size.                       | All         |
| `--define=no_tensorflow_py_deps=true`             | Excludes TensorFlow Python dependencies.                                  | No direct impact.                                     | Reduces binary size by excluding Python dependencies.| All         |
| `--config=monolithic`                             | Builds TensorFlow Lite as a single monolithic binary.                     | Potentially improves performance.                     | Increases binary size.                               | All         |
| `--copt=-DNDEBUG`                                 | Disables debugging information.                                           | May slightly improve performance.                     | Reduces binary size by excluding debug symbols.      | All         |
| `--copt=-fdata-sections`                          | Places each data item into its own section.                               | No direct impact.                                     | Reduces binary size when used with `--gc-sections`.  | All         |
| `--linkopt=-Wl,--gc-sections`                     | Enables garbage collection of unused sections.                            | No direct impact.                                     | Reduces binary size by removing unused code.         | All         |
| `--copt=-O3`                                      | Enables high-level optimizations.                                         | Improves performance.                                 | May increase binary size.                            | All         |
| `--copt=-flto`                                    | Enables link-time optimization.                                           | Improves performance.                                 | May increase binary size.                            | All         |
| `--linkopt=-flto`                                 | Enables link-time optimization during linking.                            | Improves performance.                                 | May increase binary size.                            | All         |
| `--strip=always`                                  | Strips all symbols from the binary.                                       | No direct impact.                                     | Significantly reduces binary size.                   | All         |
