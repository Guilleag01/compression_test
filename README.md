# Compression test


- [Compression test](#compression-test)
  - [Test setup](#test-setup)
    - [Commands](#commands)
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

Notes: Algorithms noyed with (Best compression) were run with the options for best compression otherwise default options are used.

### Commands

These were the commands used for each algorithm:

| Algorithm                | Command                                     |
| :----------------------- | :------------------------------------------ |
| 7ZIP                     | `7z a <archive> <dir>`                      |
| LZ4                      | `tar c -I"lz4" -f <archive> <dir>`          |
| LZ4 (Best compression)   | `tar c -I"lz4 -12" -f <archive> <dir>`      |
| LZMA                     | `tar c -I"lzma -T0" -f <archive> <dir>`     |
| LZMA (Best compression)  | `tar c -I"lzma -9 -T0" -f <archive> <dir>`  |
| PBZIP2                   | `tar c -Ipbzip2 -f <archive> <dir>`         |
| PGZIP                    | `tar c -I"pigz" -f <archive> <dir>`         |
| PGZIP (Best compression) | `tar c -I"pigz --best" -f <archive> <dir>`  |
| PLZIP                    | `tar c -I"plzip" -f <archive> <dir>`        |
| PLZIP (Best compression) | `tar c -I"plzip -9" -f <archive> <dir>`     |
| RAR                      | `rar a <archive> <dir>`                     |
| XZ                       | `tar c -I"xz -T0" -f <archive> <dir>`       |
| XZ (Best compression)    | `tar c -I"xz -9 -T0" -f <archive> <dir>`    |
| ZIP                      | `zip -r <archive> <dir>`                    |
| ZSTD                     | `tar c -I"zstd -T0" -f <archive> <dir>`     |
| ZSTD (Best compression)  | `tar c -I"zstd -19 -T0" -f <archive> <dir>` |

## Results

All the tables have the next categories:
 - **Time:** The time the compression process took. Lower is better.
 - **Compession:** The compression rate after the process. Higher is better.
 - **Time normalized compression:** The compression normalized to the time obtained ny dividing the compression by the time. Higher is better.

### Non compressible data

Test with "Non compressible data" sorted by "Time"

| Compression Algorithm    |     Time | Compression | Time normalized compression |
| :----------------------- | -------: | ----------: | --------------------------: |
| ZSTD                     | 0.618463 |     1.00274 |                      1.6125 |
| LZ4                      | 0.674424 |    0.999934 |                     1.48284 |
| LZ4 (Best compression)   |  1.31029 |    0.999934 |                     0.76324 |
| PGZIP (Best compression) |  1.33104 |     1.00505 |                    0.747517 |
| PGZIP                    |  1.56324 |     1.00505 |                    0.636483 |
| PBZIP2                   |   4.0795 |     1.02804 |                    0.238442 |
| RAR                      |  15.2829 |     1.00414 |                    0.065163 |
| ZIP                      |  16.6141 |     1.00645 |                   0.0598044 |
| 7ZIP                     |  19.1198 |     1.01995 |                   0.0512788 |
| XZ                       |  22.6181 |     1.01087 |                    0.043737 |
| PLZIP                    |  23.2036 |      1.0101 |                    0.042666 |
| ZSTD (Best compression)  |   29.403 |     1.01446 |                   0.0335254 |
| PLZIP (Best compression) |   39.529 |     1.01846 |                   0.0248394 |
| XZ (Best compression)    |  105.435 |     1.02264 |                  0.00927452 |
| LZMA                     |  251.955 |      1.0119 |                  0.00392229 |
| LZMA (Best compression)  |  355.775 |     1.02573 |                  0.00274026 |


Test with "Non compressible data" sorted by "Compression"

| Compression Algorithm    |     Time | Compression | Time normalized compression |
| :----------------------- | -------: | ----------: | --------------------------: |
| PBZIP2                   |   4.0795 |     1.02804 |                    0.238442 |
| LZMA (Best compression)  |  355.775 |     1.02573 |                  0.00274026 |
| XZ (Best compression)    |  105.435 |     1.02264 |                  0.00927452 |
| 7ZIP                     |  19.1198 |     1.01995 |                   0.0512788 |
| PLZIP (Best compression) |   39.529 |     1.01846 |                   0.0248394 |
| ZSTD (Best compression)  |   29.403 |     1.01446 |                   0.0335254 |
| LZMA                     |  251.955 |      1.0119 |                  0.00392229 |
| XZ                       |  22.6181 |     1.01087 |                    0.043737 |
| PLZIP                    |  23.2036 |      1.0101 |                    0.042666 |
| ZIP                      |  16.6141 |     1.00645 |                   0.0598044 |
| PGZIP (Best compression) |  1.33104 |     1.00505 |                    0.747517 |
| PGZIP                    |  1.56324 |     1.00505 |                    0.636483 |
| RAR                      |  15.2829 |     1.00414 |                    0.065163 |
| ZSTD                     | 0.618463 |     1.00274 |                      1.6125 |
| LZ4 (Best compression)   |  1.31029 |    0.999934 |                     0.76324 |
| LZ4                      | 0.674424 |    0.999934 |                     1.48284 |


Test with "Non compressible data" sorted by "Time normalized compression"

| Compression Algorithm    |     Time | Compression | Time normalized compression |
| :----------------------- | -------: | ----------: | --------------------------: |
| ZSTD                     | 0.618463 |     1.00274 |                      1.6125 |
| LZ4                      | 0.674424 |    0.999934 |                     1.48284 |
| LZ4 (Best compression)   |  1.31029 |    0.999934 |                     0.76324 |
| PGZIP (Best compression) |  1.33104 |     1.00505 |                    0.747517 |
| PGZIP                    |  1.56324 |     1.00505 |                    0.636483 |
| PBZIP2                   |   4.0795 |     1.02804 |                    0.238442 |
| RAR                      |  15.2829 |     1.00414 |                    0.065163 |
| ZIP                      |  16.6141 |     1.00645 |                   0.0598044 |
| 7ZIP                     |  19.1198 |     1.01995 |                   0.0512788 |
| XZ                       |  22.6181 |     1.01087 |                    0.043737 |
| PLZIP                    |  23.2036 |      1.0101 |                    0.042666 |
| ZSTD (Best compression)  |   29.403 |     1.01446 |                   0.0335254 |
| PLZIP (Best compression) |   39.529 |     1.01846 |                   0.0248394 |
| XZ (Best compression)    |  105.435 |     1.02264 |                  0.00927452 |
| LZMA                     |  251.955 |      1.0119 |                  0.00392229 |
| LZMA (Best compression)  |  355.775 |     1.02573 |                  0.00274026 |

### Lots of data with mixed types and sizes

Test with "Lots of data with mixed types and sizes" sorted by "Time"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| ZSTD                     | 3.46664 |     2.51686 |                    0.114613 |
| LZ4                      | 4.21573 |      1.5038 |                    0.157738 |
| PGZIP                    | 9.69945 |      1.6994 |                   0.0606677 |
| PGZIP (Best compression) | 22.9607 |     1.70312 |                   0.0255724 |
| PBZIP2                   | 25.7424 |     2.08055 |                   0.0186713 |
| LZ4 (Best compression)   | 40.0768 |     1.61392 |                   0.0154605 |
| XZ                       | 75.1801 |     3.15492 |                  0.00421608 |
| RAR                      | 87.4462 |     2.76305 |                  0.00413875 |
| PLZIP                    | 91.6147 |     3.08922 |                  0.00353334 |
| 7ZIP                     | 95.7274 |     3.56446 |                  0.00293069 |
| ZIP                      | 116.916 |     1.69067 |                  0.00505901 |
| PLZIP (Best compression) | 148.618 |       3.343 |                  0.00201277 |
| ZSTD (Best compression)  | 161.057 |     3.09079 |                  0.00200886 |
| XZ (Best compression)    | 240.062 |     3.46817 |                  0.00120109 |
| LZMA                     | 1046.05 |     3.21621 |                 0.000297238 |
| LZMA (Best compression)  | 1226.16 |     3.51061 |                 0.000232311 |


Test with "Lots of data with mixed types and sizes" sorted by "Compression"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| 7ZIP                     | 95.7274 |     3.56446 |                  0.00293069 |
| LZMA (Best compression)  | 1226.16 |     3.51061 |                 0.000232311 |
| XZ (Best compression)    | 240.062 |     3.46817 |                  0.00120109 |
| PLZIP (Best compression) | 148.618 |       3.343 |                  0.00201277 |
| LZMA                     | 1046.05 |     3.21621 |                 0.000297238 |
| XZ                       | 75.1801 |     3.15492 |                  0.00421608 |
| ZSTD (Best compression)  | 161.057 |     3.09079 |                  0.00200886 |
| PLZIP                    | 91.6147 |     3.08922 |                  0.00353334 |
| RAR                      | 87.4462 |     2.76305 |                  0.00413875 |
| ZSTD                     | 3.46664 |     2.51686 |                    0.114613 |
| PBZIP2                   | 25.7424 |     2.08055 |                   0.0186713 |
| PGZIP (Best compression) | 22.9607 |     1.70312 |                   0.0255724 |
| PGZIP                    | 9.69945 |      1.6994 |                   0.0606677 |
| ZIP                      | 116.916 |     1.69067 |                  0.00505901 |
| LZ4 (Best compression)   | 40.0768 |     1.61392 |                   0.0154605 |
| LZ4                      | 4.21573 |      1.5038 |                    0.157738 |


Test with "Lots of data with mixed types and sizes" sorted by "Time normalized compression"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| LZ4                      | 4.21573 |      1.5038 |                    0.157738 |
| ZSTD                     | 3.46664 |     2.51686 |                    0.114613 |
| PGZIP                    | 9.69945 |      1.6994 |                   0.0606677 |
| PGZIP (Best compression) | 22.9607 |     1.70312 |                   0.0255724 |
| PBZIP2                   | 25.7424 |     2.08055 |                   0.0186713 |
| LZ4 (Best compression)   | 40.0768 |     1.61392 |                   0.0154605 |
| ZIP                      | 116.916 |     1.69067 |                  0.00505901 |
| XZ                       | 75.1801 |     3.15492 |                  0.00421608 |
| RAR                      | 87.4462 |     2.76305 |                  0.00413875 |
| PLZIP                    | 91.6147 |     3.08922 |                  0.00353334 |
| 7ZIP                     | 95.7274 |     3.56446 |                  0.00293069 |
| PLZIP (Best compression) | 148.618 |       3.343 |                  0.00201277 |
| ZSTD (Best compression)  | 161.057 |     3.09079 |                  0.00200886 |
| XZ (Best compression)    | 240.062 |     3.46817 |                  0.00120109 |
| LZMA                     | 1046.05 |     3.21621 |                 0.000297238 |
| LZMA (Best compression)  | 1226.16 |     3.51061 |                 0.000232311 |

### A lot of many small text files

Test with "A lot of many small text files" sorted by "Time"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| ZSTD                     | 1.18429 |     5.13139 |                    0.164554 |
| LZ4                      | 1.51286 |     3.02663 |                    0.218395 |
| PGZIP                    | 2.15661 |     4.89074 |                   0.0948099 |
| PGZIP (Best compression) | 3.30062 |     4.95067 |                   0.0611984 |
| LZ4 (Best compression)   | 3.99269 |     4.21619 |                   0.0594038 |
| PBZIP2                   | 4.90839 |     6.37939 |                   0.0319361 |
| PLZIP                    | 22.5141 |     7.14673 |                  0.00621496 |
| ZIP                      | 23.1998 |     3.73557 |                   0.0115388 |
| XZ                       | 25.4004 |      7.3132 |                  0.00538335 |
| RAR                      | 35.5695 |     4.04528 |                  0.00694982 |
| 7ZIP                     | 46.5886 |     7.21744 |                  0.00297397 |
| ZSTD (Best compression)  | 50.0969 |     7.19689 |                   0.0027736 |
| PLZIP (Best compression) | 53.0104 |     7.60392 |                  0.00248085 |
| XZ (Best compression)    | 101.392 |     7.61049 |                  0.00129593 |
| LZMA                     | 289.196 |     7.39904 |                 0.000467339 |
| LZMA (Best compression)  | 401.785 |     7.65804 |                 0.000325004 |


Test with "A lot of many small text files" sorted by "Compression"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| LZMA (Best compression)  | 401.785 |     7.65804 |                 0.000325004 |
| XZ (Best compression)    | 101.392 |     7.61049 |                  0.00129593 |
| PLZIP (Best compression) | 53.0104 |     7.60392 |                  0.00248085 |
| LZMA                     | 289.196 |     7.39904 |                 0.000467339 |
| XZ                       | 25.4004 |      7.3132 |                  0.00538335 |
| 7ZIP                     | 46.5886 |     7.21744 |                  0.00297397 |
| ZSTD (Best compression)  | 50.0969 |     7.19689 |                   0.0027736 |
| PLZIP                    | 22.5141 |     7.14673 |                  0.00621496 |
| PBZIP2                   | 4.90839 |     6.37939 |                   0.0319361 |
| ZSTD                     | 1.18429 |     5.13139 |                    0.164554 |
| PGZIP (Best compression) | 3.30062 |     4.95067 |                   0.0611984 |
| PGZIP                    | 2.15661 |     4.89074 |                   0.0948099 |
| LZ4 (Best compression)   | 3.99269 |     4.21619 |                   0.0594038 |
| RAR                      | 35.5695 |     4.04528 |                  0.00694982 |
| ZIP                      | 23.1998 |     3.73557 |                   0.0115388 |
| LZ4                      | 1.51286 |     3.02663 |                    0.218395 |


Test with "A lot of many small text files" sorted by "Time normalized compression"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| LZ4                      | 1.51286 |     3.02663 |                    0.218395 |
| ZSTD                     | 1.18429 |     5.13139 |                    0.164554 |
| PGZIP                    | 2.15661 |     4.89074 |                   0.0948099 |
| PGZIP (Best compression) | 3.30062 |     4.95067 |                   0.0611984 |
| LZ4 (Best compression)   | 3.99269 |     4.21619 |                   0.0594038 |
| PBZIP2                   | 4.90839 |     6.37939 |                   0.0319361 |
| ZIP                      | 23.1998 |     3.73557 |                   0.0115388 |
| RAR                      | 35.5695 |     4.04528 |                  0.00694982 |
| PLZIP                    | 22.5141 |     7.14673 |                  0.00621496 |
| XZ                       | 25.4004 |      7.3132 |                  0.00538335 |
| 7ZIP                     | 46.5886 |     7.21744 |                  0.00297397 |
| ZSTD (Best compression)  | 50.0969 |     7.19689 |                   0.0027736 |
| PLZIP (Best compression) | 53.0104 |     7.60392 |                  0.00248085 |
| XZ (Best compression)    | 101.392 |     7.61049 |                  0.00129593 |
| LZMA                     | 289.196 |     7.39904 |                 0.000467339 |
| LZMA (Best compression)  | 401.785 |     7.65804 |                 0.000325004 |

### A few text files

Test with "A few text files" sorted by "Time"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      |  0.023663 |      1.1127 |                     37.9798 |
| PGZIP                    | 0.0332351 |     1.13478 |                     26.5149 |
| PGZIP (Best compression) | 0.0341132 |     1.13541 |                      25.818 |
| ZSTD                     |  0.036551 |     1.61309 |                     16.9606 |
| LZ4 (Best compression)   |   0.13737 |     1.13707 |                     6.40209 |
| ZIP                      |  0.237154 |     1.08497 |                     3.88645 |
| PBZIP2                   |  0.279492 |     1.37485 |                      2.6024 |
| RAR                      |  0.308938 |     1.10265 |                     2.93557 |
| 7ZIP                     |  0.426743 |     2.15245 |                     1.08868 |
| ZSTD (Best compression)  |  0.928809 |     2.15193 |                    0.500317 |
| XZ                       |   1.49799 |     2.15023 |                    0.310461 |
| XZ (Best compression)    |   1.55916 |     2.15047 |                    0.298247 |
| LZMA                     |   1.56381 |      2.1419 |                    0.298551 |
| LZMA (Best compression)  |   1.57281 |     2.14211 |                    0.296812 |
| PLZIP                    |   1.64311 |     2.14013 |                    0.284375 |
| PLZIP (Best compression) |   2.30391 |     2.14365 |                     0.20248 |


Test with "A few text files" sorted by "Compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| 7ZIP                     |  0.426743 |     2.15245 |                     1.08868 |
| ZSTD (Best compression)  |  0.928809 |     2.15193 |                    0.500317 |
| XZ (Best compression)    |   1.55916 |     2.15047 |                    0.298247 |
| XZ                       |   1.49799 |     2.15023 |                    0.310461 |
| PLZIP (Best compression) |   2.30391 |     2.14365 |                     0.20248 |
| LZMA (Best compression)  |   1.57281 |     2.14211 |                    0.296812 |
| LZMA                     |   1.56381 |      2.1419 |                    0.298551 |
| PLZIP                    |   1.64311 |     2.14013 |                    0.284375 |
| ZSTD                     |  0.036551 |     1.61309 |                     16.9606 |
| PBZIP2                   |  0.279492 |     1.37485 |                      2.6024 |
| LZ4 (Best compression)   |   0.13737 |     1.13707 |                     6.40209 |
| PGZIP (Best compression) | 0.0341132 |     1.13541 |                      25.818 |
| PGZIP                    | 0.0332351 |     1.13478 |                     26.5149 |
| LZ4                      |  0.023663 |      1.1127 |                     37.9798 |
| RAR                      |  0.308938 |     1.10265 |                     2.93557 |
| ZIP                      |  0.237154 |     1.08497 |                     3.88645 |


Test with "A few text files" sorted by "Time normalized compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      |  0.023663 |      1.1127 |                     37.9798 |
| PGZIP                    | 0.0332351 |     1.13478 |                     26.5149 |
| PGZIP (Best compression) | 0.0341132 |     1.13541 |                      25.818 |
| ZSTD                     |  0.036551 |     1.61309 |                     16.9606 |
| LZ4 (Best compression)   |   0.13737 |     1.13707 |                     6.40209 |
| ZIP                      |  0.237154 |     1.08497 |                     3.88645 |
| RAR                      |  0.308938 |     1.10265 |                     2.93557 |
| PBZIP2                   |  0.279492 |     1.37485 |                      2.6024 |
| 7ZIP                     |  0.426743 |     2.15245 |                     1.08868 |
| ZSTD (Best compression)  |  0.928809 |     2.15193 |                    0.500317 |
| XZ                       |   1.49799 |     2.15023 |                    0.310461 |
| LZMA                     |   1.56381 |      2.1419 |                    0.298551 |
| XZ (Best compression)    |   1.55916 |     2.15047 |                    0.298247 |
| LZMA (Best compression)  |   1.57281 |     2.14211 |                    0.296812 |
| PLZIP                    |   1.64311 |     2.14013 |                    0.284375 |
| PLZIP (Best compression) |   2.30391 |     2.14365 |                     0.20248 |

### A few mixed files

Test with "A few mixed files" sorted by "Time"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      | 0.0194356 |     1.99491 |                     25.7916 |
| PGZIP                    | 0.0281055 |      2.8725 |                     12.3865 |
| ZSTD                     | 0.0360215 |     3.09782 |                     8.96153 |
| PGZIP (Best compression) | 0.0510929 |      2.8845 |                     6.78529 |
| PBZIP2                   | 0.0964587 |      3.3937 |                     3.05482 |
| RAR                      |   0.16964 |     3.48817 |                     1.68995 |
| LZ4 (Best compression)   |  0.175575 |     2.56754 |                      2.2183 |
| ZIP                      |  0.249501 |     2.77821 |                     1.44266 |
| 7ZIP                     |  0.524823 |     4.15235 |                    0.458873 |
| XZ                       |   1.22789 |     4.16868 |                    0.195363 |
| LZMA                     |   1.23839 |      4.1687 |                    0.193706 |
| PLZIP                    |   1.26057 |     4.15287 |                    0.191022 |
| LZMA (Best compression)  |   1.29071 |      4.1687 |                    0.185853 |
| ZSTD (Best compression)  |   1.42642 |     3.75015 |                    0.186941 |
| XZ (Best compression)    |   1.44246 |     4.16868 |                    0.166302 |
| PLZIP (Best compression) |   2.02732 |     4.18295 |                    0.117922 |


Test with "A few mixed files" sorted by "Compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| PLZIP (Best compression) |   2.02732 |     4.18295 |                    0.117922 |
| LZMA (Best compression)  |   1.29071 |      4.1687 |                    0.185853 |
| LZMA                     |   1.23839 |      4.1687 |                    0.193706 |
| XZ (Best compression)    |   1.44246 |     4.16868 |                    0.166302 |
| XZ                       |   1.22789 |     4.16868 |                    0.195363 |
| PLZIP                    |   1.26057 |     4.15287 |                    0.191022 |
| 7ZIP                     |  0.524823 |     4.15235 |                    0.458873 |
| ZSTD (Best compression)  |   1.42642 |     3.75015 |                    0.186941 |
| RAR                      |   0.16964 |     3.48817 |                     1.68995 |
| PBZIP2                   | 0.0964587 |      3.3937 |                     3.05482 |
| ZSTD                     | 0.0360215 |     3.09782 |                     8.96153 |
| PGZIP (Best compression) | 0.0510929 |      2.8845 |                     6.78529 |
| PGZIP                    | 0.0281055 |      2.8725 |                     12.3865 |
| ZIP                      |  0.249501 |     2.77821 |                     1.44266 |
| LZ4 (Best compression)   |  0.175575 |     2.56754 |                      2.2183 |
| LZ4                      | 0.0194356 |     1.99491 |                     25.7916 |


Test with "A few mixed files" sorted by "Time normalized compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      | 0.0194356 |     1.99491 |                     25.7916 |
| PGZIP                    | 0.0281055 |      2.8725 |                     12.3865 |
| ZSTD                     | 0.0360215 |     3.09782 |                     8.96153 |
| PGZIP (Best compression) | 0.0510929 |      2.8845 |                     6.78529 |
| PBZIP2                   | 0.0964587 |      3.3937 |                     3.05482 |
| LZ4 (Best compression)   |  0.175575 |     2.56754 |                      2.2183 |
| RAR                      |   0.16964 |     3.48817 |                     1.68995 |
| ZIP                      |  0.249501 |     2.77821 |                     1.44266 |
| 7ZIP                     |  0.524823 |     4.15235 |                    0.458873 |
| XZ                       |   1.22789 |     4.16868 |                    0.195363 |
| LZMA                     |   1.23839 |      4.1687 |                    0.193706 |
| PLZIP                    |   1.26057 |     4.15287 |                    0.191022 |
| ZSTD (Best compression)  |   1.42642 |     3.75015 |                    0.186941 |
| LZMA (Best compression)  |   1.29071 |      4.1687 |                    0.185853 |
| XZ (Best compression)    |   1.44246 |     4.16868 |                    0.166302 |
| PLZIP (Best compression) |   2.02732 |     4.18295 |                    0.117922 |
