# TFlite-builds

## Builds :
- Base : Debian bookworm
- Architectures : x86_64 ; aarch64 ; x86_64_non_avx
- Python versions : 3.9 ; 3.10 ; 3.11 ; 3.12

## Flags :
| Name of Flag                                | What Does It Do?                                                                 | Impact on TFLite Performance                          | Impact on TFLite Runtime Size                        |
|---------------------------------------------|----------------------------------------------------------------------------------|------------------------------------------------------|-----------------------------------------------------|
| `--define=tflite_enable_xnnpack=true`       | Enables XNNPACK, a highly optimized library for neural network inference.        | Improves performance for floating-point models.       | Slight increase in binary size.                     |
| `--define=xnnpack_enable_subgraph_reshaping=true` | Enables subgraph reshaping in XNNPACK.                                           | Enhances performance by optimizing subgraph execution.| Minimal impact on binary size.                      |
| `--define=no_tensorflow_py_deps=true`       | Excludes TensorFlow Python dependencies.                                         | No direct impact.                                     | Reduces binary size by excluding Python dependencies.|
| `-config=monolithic`                        | Builds TensorFlow Lite as a single monolithic binary.                            | Potentially improves performance.                     | Increases binary size.                              |
| `--copt=-DNDEBUG`                           | Disables debugging information.                                                  | May slightly improve performance.                     | Reduces binary size by excluding debug symbols.      |
| `--copt=-fdata-sections`                    | Places each data item into its own section.                                      | No direct impact.                                     | Reduces binary size when used with `--gc-sections`.  |
| `--linkopt=-Wl,--gc-sections`               | Enables garbage collection of unused sections.                                   | No direct impact.                                     | Reduces binary size by removing unused code.         |
| `--copt=-O3`                                | Enables high-level optimizations.                                                | Improves performance.                                 | May increase binary size.                            |
| `--copt=-flto`                              | Enables link-time optimization.                                                  | Improves performance.                                 | May increase binary size.                            |
| `--linkopt=-flto`                           | Enables link-time optimization during linking.                                   | Improves performance.                                 | May increase binary size.                            |
| `--strip=always`                            | Strips all symbols from the binary.                                              | No direct impact.                                     | Significantly reduces binary size.                   |
