# Compression test


- [Compression test](#compression-test)
  - [Test setup](#test-setup)
  - [Results](#results)
    - [Non compressible data](#non-compressible-data)
    - [Lots of data with mixed types and sizes](#lots-of-data-with-mixed-types-and-sizes)
    - [A lot of many small text files](#a-lot-of-many-small-text-files)
    - [A few text files](#a-few-text-files)
    - [A few mixed files](#a-few-mixed-files)

I made some test on multiple of the compression algorithms and tools found on linux.

## Test setup
The algorithms were tested on the following situations:
 - **Lots of data with mixed types and sizes:** A lot of various types of files of varying sizes. The total size of all the files is 4.36 GiB
 - **Non-compressible data:** A lot of barely compressible files, in thes case jpeg images. The total size of all the files is 0.62 GiB
 - **A lot of many small text files:** A lot of small text files, all the files are under 1MB in size. The total size of all the files is 0.96 GiB
 - **A few text files:** A few text files. The total size of all the files is 9.54 MiB
 - **A few mixed files:** A few files varying in size and type. The total size of all the files is 6.66 MiB

The algorithms tested were the following:
 - XZ
 - LZMA
 - PGZIP (parallel gzip)
 - PBZIP2 (parallel bzip2)
 - LZ4
 - PLZIP (parallel lzip)
 - ZSTD
 - RAR
 - 7ZIP
 - ZIP

The tests were run on a system with the following specs
 - Ryzen 9 3900X CPU
 - 32 GB DDR4 2133 MT/s memory
 - nvme gen4 ssd
 - Arch linux kernel version 6.12.8
 - xfs file system

Notes: All the algorithms were run with the maximum compression mode.

## Results
### Non compressible data

Test with "Non compressible data" sorted by "Time"

| Compression Algorithm |    Time | Compression | Time normalized compression |
| :-------------------- | ------: | ----------: | --------------------------: |
| PGZIP                 | 1.26777 |     1.00505 |                    0.784826 |
| LZ4                   |  1.2858 |    0.999934 |                    0.777779 |
| PBZIP2                |  3.8217 |     1.02804 |                    0.254526 |
| RAR                   | 13.2534 |     1.00414 |                   0.0751413 |
| ZIP                   | 16.3882 |     1.00645 |                   0.0606285 |
| 7ZIP                  | 17.2523 |     1.01995 |                   0.0568293 |
| ZSTD                  | 26.1111 |     1.01446 |                   0.0377519 |
| PLZIP                 | 37.1494 |     1.01846 |                   0.0264305 |
| XZ                    | 104.294 |     1.02264 |                    0.009376 |
| LZMA                  | 351.912 |     1.02573 |                  0.00277034 |


Test with "Non compressible data" sorted by "Compression"

| Compression Algorithm |    Time | Compression | Time normalized compression |
| :-------------------- | ------: | ----------: | --------------------------: |
| PBZIP2                |  3.8217 |     1.02804 |                    0.254526 |
| LZMA                  | 351.912 |     1.02573 |                  0.00277034 |
| XZ                    | 104.294 |     1.02264 |                    0.009376 |
| 7ZIP                  | 17.2523 |     1.01995 |                   0.0568293 |
| PLZIP                 | 37.1494 |     1.01846 |                   0.0264305 |
| ZSTD                  | 26.1111 |     1.01446 |                   0.0377519 |
| ZIP                   | 16.3882 |     1.00645 |                   0.0606285 |
| PGZIP                 | 1.26777 |     1.00505 |                    0.784826 |
| RAR                   | 13.2534 |     1.00414 |                   0.0751413 |
| LZ4                   |  1.2858 |    0.999934 |                    0.777779 |


Test with "Non compressible data" sorted by "Time normalized compression"

| Compression Algorithm |    Time | Compression | Time normalized compression |
| :-------------------- | ------: | ----------: | --------------------------: |
| PGZIP                 | 1.26777 |     1.00505 |                    0.784826 |
| LZ4                   |  1.2858 |    0.999934 |                    0.777779 |
| PBZIP2                |  3.8217 |     1.02804 |                    0.254526 |
| RAR                   | 13.2534 |     1.00414 |                   0.0751413 |
| ZIP                   | 16.3882 |     1.00645 |                   0.0606285 |
| 7ZIP                  | 17.2523 |     1.01995 |                   0.0568293 |
| ZSTD                  | 26.1111 |     1.01446 |                   0.0377519 |
| PLZIP                 | 37.1494 |     1.01846 |                   0.0264305 |
| XZ                    | 104.294 |     1.02264 |                    0.009376 |
| LZMA                  | 351.912 |     1.02573 |                  0.00277034 |

### Lots of data with mixed types and sizes

Test with "Lots of data with mixed types and sizes" sorted by "Time"

| Compression Algorithm |    Time | Compression | Time normalized compression |
| :-------------------- | ------: | ----------: | --------------------------: |
| PGZIP                 | 21.8042 |     1.70312 |                   0.0269288 |
| PBZIP2                | 23.2807 |     2.08055 |                   0.0206456 |
| LZ4                   | 38.7711 |     1.61392 |                   0.0159812 |
| RAR                   | 70.6871 |     2.76305 |                     0.00512 |
| 7ZIP                  |   84.22 |     3.56446 |                  0.00333112 |
| ZIP                   | 116.646 |     1.69067 |                  0.00507074 |
| PLZIP                 | 135.211 |       3.343 |                  0.00221234 |
| ZSTD                  | 138.242 |     3.09079 |                   0.0023404 |
| XZ                    | 236.184 |     3.46817 |                  0.00122081 |
| LZMA                  | 1208.73 |     3.51061 |                 0.000235662 |


Test with "Lots of data with mixed types and sizes" sorted by "Compression"

| Compression Algorithm |    Time | Compression | Time normalized compression |
| :-------------------- | ------: | ----------: | --------------------------: |
| 7ZIP                  |   84.22 |     3.56446 |                  0.00333112 |
| LZMA                  | 1208.73 |     3.51061 |                 0.000235662 |
| XZ                    | 236.184 |     3.46817 |                  0.00122081 |
| PLZIP                 | 135.211 |       3.343 |                  0.00221234 |
| ZSTD                  | 138.242 |     3.09079 |                   0.0023404 |
| RAR                   | 70.6871 |     2.76305 |                     0.00512 |
| PBZIP2                | 23.2807 |     2.08055 |                   0.0206456 |
| PGZIP                 | 21.8042 |     1.70312 |                   0.0269288 |
| ZIP                   | 116.646 |     1.69067 |                  0.00507074 |
| LZ4                   | 38.7711 |     1.61392 |                   0.0159812 |


Test with "Lots of data with mixed types and sizes" sorted by "Time normalized compression"

| Compression Algorithm |    Time | Compression | Time normalized compression |
| :-------------------- | ------: | ----------: | --------------------------: |
| PGZIP                 | 21.8042 |     1.70312 |                   0.0269288 |
| PBZIP2                | 23.2807 |     2.08055 |                   0.0206456 |
| LZ4                   | 38.7711 |     1.61392 |                   0.0159812 |
| RAR                   | 70.6871 |     2.76305 |                     0.00512 |
| ZIP                   | 116.646 |     1.69067 |                  0.00507074 |
| 7ZIP                  |   84.22 |     3.56446 |                  0.00333112 |
| ZSTD                  | 138.242 |     3.09079 |                   0.0023404 |
| PLZIP                 | 135.211 |       3.343 |                  0.00221234 |
| XZ                    | 236.184 |     3.46817 |                  0.00122081 |
| LZMA                  | 1208.73 |     3.51061 |                 0.000235662 |

### A lot of many small text files

Test with "A lot of many small text files" sorted by "Time"

| Compression Algorithm |    Time | Compression | Time normalized compression |
| :-------------------- | ------: | ----------: | --------------------------: |
| PGZIP                 | 3.20727 |     4.95067 |                   0.0629797 |
| LZ4                   | 4.07333 |     4.21619 |                   0.0582278 |
| PBZIP2                |  4.4668 |     6.37939 |                   0.0350933 |
| ZIP                   | 23.2824 |     3.73557 |                   0.0114978 |
| RAR                   | 34.9045 |     4.04528 |                  0.00708224 |
| 7ZIP                  | 46.3945 |     7.21744 |                  0.00298642 |
| ZSTD                  | 47.4384 |     7.19689 |                  0.00292904 |
| PLZIP                 | 49.5483 |     7.60392 |                   0.0026542 |
| XZ                    | 95.9468 |     7.61049 |                  0.00136948 |
| LZMA                  | 380.253 |     7.65804 |                 0.000343407 |


Test with "A lot of many small text files" sorted by "Compression"

| Compression Algorithm |    Time | Compression | Time normalized compression |
| :-------------------- | ------: | ----------: | --------------------------: |
| LZMA                  | 380.253 |     7.65804 |                 0.000343407 |
| XZ                    | 95.9468 |     7.61049 |                  0.00136948 |
| PLZIP                 | 49.5483 |     7.60392 |                   0.0026542 |
| 7ZIP                  | 46.3945 |     7.21744 |                  0.00298642 |
| ZSTD                  | 47.4384 |     7.19689 |                  0.00292904 |
| PBZIP2                |  4.4668 |     6.37939 |                   0.0350933 |
| PGZIP                 | 3.20727 |     4.95067 |                   0.0629797 |
| LZ4                   | 4.07333 |     4.21619 |                   0.0582278 |
| RAR                   | 34.9045 |     4.04528 |                  0.00708224 |
| ZIP                   | 23.2824 |     3.73557 |                   0.0114978 |


Test with "A lot of many small text files" sorted by "Time normalized compression"

| Compression Algorithm |    Time | Compression | Time normalized compression |
| :-------------------- | ------: | ----------: | --------------------------: |
| PGZIP                 | 3.20727 |     4.95067 |                   0.0629797 |
| LZ4                   | 4.07333 |     4.21619 |                   0.0582278 |
| PBZIP2                |  4.4668 |     6.37939 |                   0.0350933 |
| ZIP                   | 23.2824 |     3.73557 |                   0.0114978 |
| RAR                   | 34.9045 |     4.04528 |                  0.00708224 |
| 7ZIP                  | 46.3945 |     7.21744 |                  0.00298642 |
| ZSTD                  | 47.4384 |     7.19689 |                  0.00292904 |
| PLZIP                 | 49.5483 |     7.60392 |                   0.0026542 |
| XZ                    | 95.9468 |     7.61049 |                  0.00136948 |
| LZMA                  | 380.253 |     7.65804 |                 0.000343407 |

### A few text files

Test with "A few text files" sorted by "Time"

| Compression Algorithm |      Time | Compression | Time normalized compression |
| :-------------------- | --------: | ----------: | --------------------------: |
| PGZIP                 | 0.0423446 |     1.13541 |                     20.7993 |
| LZ4                   |  0.137808 |     1.13707 |                     6.38176 |
| ZIP                   |  0.241944 |     1.08497 |                     3.80951 |
| PBZIP2                |  0.258476 |     1.37485 |                       2.814 |
| RAR                   |  0.322799 |     1.10265 |                     2.80952 |
| 7ZIP                  |  0.433445 |     2.15245 |                     1.07185 |
| ZSTD                  |  0.993853 |     2.15193 |                    0.467573 |
| XZ                    |   1.64646 |     2.15047 |                    0.282433 |
| LZMA                  |    1.6571 |     2.14211 |                    0.281714 |
| PLZIP                 |   2.65034 |     2.14365 |                    0.176013 |


Test with "A few text files" sorted by "Compression"

| Compression Algorithm |      Time | Compression | Time normalized compression |
| :-------------------- | --------: | ----------: | --------------------------: |
| 7ZIP                  |  0.433445 |     2.15245 |                     1.07185 |
| ZSTD                  |  0.993853 |     2.15193 |                    0.467573 |
| XZ                    |   1.64646 |     2.15047 |                    0.282433 |
| PLZIP                 |   2.65034 |     2.14365 |                    0.176013 |
| LZMA                  |    1.6571 |     2.14211 |                    0.281714 |
| PBZIP2                |  0.258476 |     1.37485 |                       2.814 |
| LZ4                   |  0.137808 |     1.13707 |                     6.38176 |
| PGZIP                 | 0.0423446 |     1.13541 |                     20.7993 |
| RAR                   |  0.322799 |     1.10265 |                     2.80952 |
| ZIP                   |  0.241944 |     1.08497 |                     3.80951 |


Test with "A few text files" sorted by "Time normalized compression"

| Compression Algorithm |      Time | Compression | Time normalized compression |
| :-------------------- | --------: | ----------: | --------------------------: |
| PGZIP                 | 0.0423446 |     1.13541 |                     20.7993 |
| LZ4                   |  0.137808 |     1.13707 |                     6.38176 |
| ZIP                   |  0.241944 |     1.08497 |                     3.80951 |
| PBZIP2                |  0.258476 |     1.37485 |                       2.814 |
| RAR                   |  0.322799 |     1.10265 |                     2.80952 |
| 7ZIP                  |  0.433445 |     2.15245 |                     1.07185 |
| ZSTD                  |  0.993853 |     2.15193 |                    0.467573 |
| XZ                    |   1.64646 |     2.15047 |                    0.282433 |
| LZMA                  |    1.6571 |     2.14211 |                    0.281714 |
| PLZIP                 |   2.65034 |     2.14365 |                    0.176013 |

### A few mixed files

Test with "A few mixed files" sorted by "Time"

| Compression Algorithm |      Time | Compression | Time normalized compression |
| :-------------------- | --------: | ----------: | --------------------------: |
| PGZIP                 | 0.0472157 |      2.8845 |                     7.34247 |
| PBZIP2                | 0.0996904 |      3.3937 |                     2.95579 |
| LZ4                   |  0.178676 |     2.56754 |                     2.17979 |
| RAR                   |  0.187353 |     3.48817 |                     1.53018 |
| ZIP                   |  0.240878 |     2.77821 |                      1.4943 |
| 7ZIP                  |   0.53761 |     4.15235 |                    0.447959 |
| LZMA                  |   1.36919 |      4.1687 |                      0.1752 |
| XZ                    |   1.56128 |     4.16868 |                    0.153646 |
| ZSTD                  |   1.64639 |     3.75015 |                    0.161965 |
| PLZIP                 |   2.20772 |     4.18295 |                    0.108287 |


Test with "A few mixed files" sorted by "Compression"

| Compression Algorithm |      Time | Compression | Time normalized compression |
| :-------------------- | --------: | ----------: | --------------------------: |
| PLZIP                 |   2.20772 |     4.18295 |                    0.108287 |
| LZMA                  |   1.36919 |      4.1687 |                      0.1752 |
| XZ                    |   1.56128 |     4.16868 |                    0.153646 |
| 7ZIP                  |   0.53761 |     4.15235 |                    0.447959 |
| ZSTD                  |   1.64639 |     3.75015 |                    0.161965 |
| RAR                   |  0.187353 |     3.48817 |                     1.53018 |
| PBZIP2                | 0.0996904 |      3.3937 |                     2.95579 |
| PGZIP                 | 0.0472157 |      2.8845 |                     7.34247 |
| ZIP                   |  0.240878 |     2.77821 |                      1.4943 |
| LZ4                   |  0.178676 |     2.56754 |                     2.17979 |


Test with "A few mixed files" sorted by "Time normalized compression"

| Compression Algorithm |      Time | Compression | Time normalized compression |
| :-------------------- | --------: | ----------: | --------------------------: |
| PGZIP                 | 0.0472157 |      2.8845 |                     7.34247 |
| PBZIP2                | 0.0996904 |      3.3937 |                     2.95579 |
| LZ4                   |  0.178676 |     2.56754 |                     2.17979 |
| RAR                   |  0.187353 |     3.48817 |                     1.53018 |
| ZIP                   |  0.240878 |     2.77821 |                      1.4943 |
| 7ZIP                  |   0.53761 |     4.15235 |                    0.447959 |
| LZMA                  |   1.36919 |      4.1687 |                      0.1752 |
| ZSTD                  |   1.64639 |     3.75015 |                    0.161965 |
| XZ                    |   1.56128 |     4.16868 |                    0.153646 |
| PLZIP                 |   2.20772 |     4.18295 |                    0.108287 |
