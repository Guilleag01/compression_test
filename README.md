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
| ZSTD                     | 0.618463 |     1.00274 |                     1.62134 |
| LZ4                      | 0.674424 |    0.999934 |                     1.48265 |
| LZ4 (Best compression)   |  1.31029 |    0.999934 |                     0.76314 |
| PGZIP (Best compression) |  1.33104 |     1.00505 |                    0.755085 |
| PGZIP                    |  1.56324 |     1.00505 |                    0.642927 |
| PBZIP2                   |   4.0795 |     1.02804 |                    0.252002 |
| RAR                      |  15.2829 |     1.00414 |                   0.0657031 |
| ZIP                      |  16.6141 |     1.00645 |                   0.0605781 |
| 7ZIP                     |  19.1198 |     1.01995 |                   0.0533455 |
| XZ                       |  22.6181 |     1.01087 |                   0.0446928 |
| PLZIP                    |  23.2036 |      1.0101 |                   0.0435319 |
| ZSTD (Best compression)  |   29.403 |     1.01446 |                    0.034502 |
| PLZIP (Best compression) |   39.529 |     1.01846 |                   0.0257648 |
| XZ (Best compression)    |  105.435 |     1.02264 |                  0.00969931 |
| LZMA                     |  251.955 |      1.0119 |                  0.00401619 |
| LZMA (Best compression)  |  355.775 |     1.02573 |                  0.00288308 |


Test with "Non compressible data" sorted by "Compression"

| Compression Algorithm    |     Time | Compression | Time normalized compression |
| :----------------------- | -------: | ----------: | --------------------------: |
| PBZIP2                   |   4.0795 |     1.02804 |                    0.252002 |
| LZMA (Best compression)  |  355.775 |     1.02573 |                  0.00288308 |
| XZ (Best compression)    |  105.435 |     1.02264 |                  0.00969931 |
| 7ZIP                     |  19.1198 |     1.01995 |                   0.0533455 |
| PLZIP (Best compression) |   39.529 |     1.01846 |                   0.0257648 |
| ZSTD (Best compression)  |   29.403 |     1.01446 |                    0.034502 |
| LZMA                     |  251.955 |      1.0119 |                  0.00401619 |
| XZ                       |  22.6181 |     1.01087 |                   0.0446928 |
| PLZIP                    |  23.2036 |      1.0101 |                   0.0435319 |
| ZIP                      |  16.6141 |     1.00645 |                   0.0605781 |
| PGZIP (Best compression) |  1.33104 |     1.00505 |                    0.755085 |
| PGZIP                    |  1.56324 |     1.00505 |                    0.642927 |
| RAR                      |  15.2829 |     1.00414 |                   0.0657031 |
| ZSTD                     | 0.618463 |     1.00274 |                     1.62134 |
| LZ4 (Best compression)   |  1.31029 |    0.999934 |                     0.76314 |
| LZ4                      | 0.674424 |    0.999934 |                     1.48265 |


Test with "Non compressible data" sorted by "Time normalized compression"

| Compression Algorithm    |     Time | Compression | Time normalized compression |
| :----------------------- | -------: | ----------: | --------------------------: |
| ZSTD                     | 0.618463 |     1.00274 |                     1.62134 |
| LZ4                      | 0.674424 |    0.999934 |                     1.48265 |
| LZ4 (Best compression)   |  1.31029 |    0.999934 |                     0.76314 |
| PGZIP (Best compression) |  1.33104 |     1.00505 |                    0.755085 |
| PGZIP                    |  1.56324 |     1.00505 |                    0.642927 |
| PBZIP2                   |   4.0795 |     1.02804 |                    0.252002 |
| RAR                      |  15.2829 |     1.00414 |                   0.0657031 |
| ZIP                      |  16.6141 |     1.00645 |                   0.0605781 |
| 7ZIP                     |  19.1198 |     1.01995 |                   0.0533455 |
| XZ                       |  22.6181 |     1.01087 |                   0.0446928 |
| PLZIP                    |  23.2036 |      1.0101 |                   0.0435319 |
| ZSTD (Best compression)  |   29.403 |     1.01446 |                    0.034502 |
| PLZIP (Best compression) |   39.529 |     1.01846 |                   0.0257648 |
| XZ (Best compression)    |  105.435 |     1.02264 |                  0.00969931 |
| LZMA                     |  251.955 |      1.0119 |                  0.00401619 |
| LZMA (Best compression)  |  355.775 |     1.02573 |                  0.00288308 |

### Lots of data with mixed types and sizes

Test with "Lots of data with mixed types and sizes" sorted by "Time"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| ZSTD                     | 3.46664 |     2.51686 |                    0.726022 |
| LZ4                      | 4.21573 |      1.5038 |                    0.356712 |
| PGZIP                    | 9.69945 |      1.6994 |                    0.175206 |
| PGZIP (Best compression) | 22.9607 |     1.70312 |                   0.0741754 |
| PBZIP2                   | 25.7424 |     2.08055 |                   0.0808218 |
| LZ4 (Best compression)   | 40.0768 |     1.61392 |                   0.0402708 |
| XZ                       | 75.1801 |     3.15492 |                   0.0419649 |
| RAR                      | 87.4462 |     2.76305 |                   0.0315972 |
| PLZIP                    | 91.6147 |     3.08922 |                   0.0337197 |
| 7ZIP                     | 95.7274 |     3.56446 |                   0.0372356 |
| ZIP                      | 116.916 |     1.69067 |                   0.0144606 |
| PLZIP (Best compression) | 148.618 |       3.343 |                    0.022494 |
| ZSTD (Best compression)  | 161.057 |     3.09079 |                   0.0191906 |
| XZ (Best compression)    | 240.062 |     3.46817 |                   0.0144469 |
| LZMA                     | 1046.05 |     3.21621 |                  0.00307463 |
| LZMA (Best compression)  | 1226.16 |     3.51061 |                  0.00286308 |


Test with "Lots of data with mixed types and sizes" sorted by "Compression"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| 7ZIP                     | 95.7274 |     3.56446 |                   0.0372356 |
| LZMA (Best compression)  | 1226.16 |     3.51061 |                  0.00286308 |
| XZ (Best compression)    | 240.062 |     3.46817 |                   0.0144469 |
| PLZIP (Best compression) | 148.618 |       3.343 |                    0.022494 |
| LZMA                     | 1046.05 |     3.21621 |                  0.00307463 |
| XZ                       | 75.1801 |     3.15492 |                   0.0419649 |
| ZSTD (Best compression)  | 161.057 |     3.09079 |                   0.0191906 |
| PLZIP                    | 91.6147 |     3.08922 |                   0.0337197 |
| RAR                      | 87.4462 |     2.76305 |                   0.0315972 |
| ZSTD                     | 3.46664 |     2.51686 |                    0.726022 |
| PBZIP2                   | 25.7424 |     2.08055 |                   0.0808218 |
| PGZIP (Best compression) | 22.9607 |     1.70312 |                   0.0741754 |
| PGZIP                    | 9.69945 |      1.6994 |                    0.175206 |
| ZIP                      | 116.916 |     1.69067 |                   0.0144606 |
| LZ4 (Best compression)   | 40.0768 |     1.61392 |                   0.0402708 |
| LZ4                      | 4.21573 |      1.5038 |                    0.356712 |


Test with "Lots of data with mixed types and sizes" sorted by "Time normalized compression"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| ZSTD                     | 3.46664 |     2.51686 |                    0.726022 |
| LZ4                      | 4.21573 |      1.5038 |                    0.356712 |
| PGZIP                    | 9.69945 |      1.6994 |                    0.175206 |
| PBZIP2                   | 25.7424 |     2.08055 |                   0.0808218 |
| PGZIP (Best compression) | 22.9607 |     1.70312 |                   0.0741754 |
| XZ                       | 75.1801 |     3.15492 |                   0.0419649 |
| LZ4 (Best compression)   | 40.0768 |     1.61392 |                   0.0402708 |
| 7ZIP                     | 95.7274 |     3.56446 |                   0.0372356 |
| PLZIP                    | 91.6147 |     3.08922 |                   0.0337197 |
| RAR                      | 87.4462 |     2.76305 |                   0.0315972 |
| PLZIP (Best compression) | 148.618 |       3.343 |                    0.022494 |
| ZSTD (Best compression)  | 161.057 |     3.09079 |                   0.0191906 |
| ZIP                      | 116.916 |     1.69067 |                   0.0144606 |
| XZ (Best compression)    | 240.062 |     3.46817 |                   0.0144469 |
| LZMA                     | 1046.05 |     3.21621 |                  0.00307463 |
| LZMA (Best compression)  | 1226.16 |     3.51061 |                  0.00286308 |

### A lot of many small text files

Test with "A lot of many small text files" sorted by "Time"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| ZSTD                     | 1.18429 |     5.13139 |                     4.33289 |
| LZ4                      | 1.51286 |     3.02663 |                     2.00061 |
| PGZIP                    | 2.15661 |     4.89074 |                     2.26779 |
| PGZIP (Best compression) | 3.30062 |     4.95067 |                     1.49992 |
| LZ4 (Best compression)   | 3.99269 |     4.21619 |                     1.05598 |
| PBZIP2                   | 4.90839 |     6.37939 |                     1.29969 |
| PLZIP                    | 22.5141 |     7.14673 |                    0.317434 |
| ZIP                      | 23.1998 |     3.73557 |                    0.161018 |
| XZ                       | 25.4004 |      7.3132 |                    0.287917 |
| RAR                      | 35.5695 |     4.04528 |                    0.113729 |
| 7ZIP                     | 46.5886 |     7.21744 |                    0.154919 |
| ZSTD (Best compression)  | 50.0969 |     7.19689 |                    0.143659 |
| PLZIP (Best compression) | 53.0104 |     7.60392 |                    0.143442 |
| XZ (Best compression)    | 101.392 |     7.61049 |                     0.07506 |
| LZMA                     | 289.196 |     7.39904 |                   0.0255848 |
| LZMA (Best compression)  | 401.785 |     7.65804 |                   0.0190601 |


Test with "A lot of many small text files" sorted by "Compression"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| LZMA (Best compression)  | 401.785 |     7.65804 |                   0.0190601 |
| XZ (Best compression)    | 101.392 |     7.61049 |                     0.07506 |
| PLZIP (Best compression) | 53.0104 |     7.60392 |                    0.143442 |
| LZMA                     | 289.196 |     7.39904 |                   0.0255848 |
| XZ                       | 25.4004 |      7.3132 |                    0.287917 |
| 7ZIP                     | 46.5886 |     7.21744 |                    0.154919 |
| ZSTD (Best compression)  | 50.0969 |     7.19689 |                    0.143659 |
| PLZIP                    | 22.5141 |     7.14673 |                    0.317434 |
| PBZIP2                   | 4.90839 |     6.37939 |                     1.29969 |
| ZSTD                     | 1.18429 |     5.13139 |                     4.33289 |
| PGZIP (Best compression) | 3.30062 |     4.95067 |                     1.49992 |
| PGZIP                    | 2.15661 |     4.89074 |                     2.26779 |
| LZ4 (Best compression)   | 3.99269 |     4.21619 |                     1.05598 |
| RAR                      | 35.5695 |     4.04528 |                    0.113729 |
| ZIP                      | 23.1998 |     3.73557 |                    0.161018 |
| LZ4                      | 1.51286 |     3.02663 |                     2.00061 |


Test with "A lot of many small text files" sorted by "Time normalized compression"

| Compression Algorithm    |    Time | Compression | Time normalized compression |
| :----------------------- | ------: | ----------: | --------------------------: |
| ZSTD                     | 1.18429 |     5.13139 |                     4.33289 |
| PGZIP                    | 2.15661 |     4.89074 |                     2.26779 |
| LZ4                      | 1.51286 |     3.02663 |                     2.00061 |
| PGZIP (Best compression) | 3.30062 |     4.95067 |                     1.49992 |
| PBZIP2                   | 4.90839 |     6.37939 |                     1.29969 |
| LZ4 (Best compression)   | 3.99269 |     4.21619 |                     1.05598 |
| PLZIP                    | 22.5141 |     7.14673 |                    0.317434 |
| XZ                       | 25.4004 |      7.3132 |                    0.287917 |
| ZIP                      | 23.1998 |     3.73557 |                    0.161018 |
| 7ZIP                     | 46.5886 |     7.21744 |                    0.154919 |
| ZSTD (Best compression)  | 50.0969 |     7.19689 |                    0.143659 |
| PLZIP (Best compression) | 53.0104 |     7.60392 |                    0.143442 |
| RAR                      | 35.5695 |     4.04528 |                    0.113729 |
| XZ (Best compression)    | 101.392 |     7.61049 |                     0.07506 |
| LZMA                     | 289.196 |     7.39904 |                   0.0255848 |
| LZMA (Best compression)  | 401.785 |     7.65804 |                   0.0190601 |

### A few text files

Test with "A few text files" sorted by "Time"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      |  0.023663 |      1.1127 |                     47.0225 |
| PGZIP                    | 0.0332351 |     1.13478 |                     34.1441 |
| PGZIP (Best compression) | 0.0341132 |     1.13541 |                     33.2838 |
| ZSTD                     |  0.036551 |     1.61309 |                     44.1327 |
| LZ4 (Best compression)   |   0.13737 |     1.13707 |                      8.2774 |
| ZIP                      |  0.237154 |     1.08497 |                     4.57493 |
| PBZIP2                   |  0.279492 |     1.37485 |                     4.91911 |
| RAR                      |  0.308938 |     1.10265 |                     3.56915 |
| 7ZIP                     |  0.426743 |     2.15245 |                     5.04389 |
| ZSTD (Best compression)  |  0.928809 |     2.15193 |                     2.31687 |
| XZ                       |   1.49799 |     2.15023 |                     1.43541 |
| XZ (Best compression)    |   1.55916 |     2.15047 |                     1.37925 |
| LZMA                     |   1.56381 |      2.1419 |                     1.36967 |
| LZMA (Best compression)  |   1.57281 |     2.14211 |                     1.36197 |
| PLZIP                    |   1.64311 |     2.14013 |                     1.30249 |
| PLZIP (Best compression) |   2.30391 |     2.14365 |                    0.930438 |


Test with "A few text files" sorted by "Compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| 7ZIP                     |  0.426743 |     2.15245 |                     5.04389 |
| ZSTD (Best compression)  |  0.928809 |     2.15193 |                     2.31687 |
| XZ (Best compression)    |   1.55916 |     2.15047 |                     1.37925 |
| XZ                       |   1.49799 |     2.15023 |                     1.43541 |
| PLZIP (Best compression) |   2.30391 |     2.14365 |                    0.930438 |
| LZMA (Best compression)  |   1.57281 |     2.14211 |                     1.36197 |
| LZMA                     |   1.56381 |      2.1419 |                     1.36967 |
| PLZIP                    |   1.64311 |     2.14013 |                     1.30249 |
| ZSTD                     |  0.036551 |     1.61309 |                     44.1327 |
| PBZIP2                   |  0.279492 |     1.37485 |                     4.91911 |
| LZ4 (Best compression)   |   0.13737 |     1.13707 |                      8.2774 |
| PGZIP (Best compression) | 0.0341132 |     1.13541 |                     33.2838 |
| PGZIP                    | 0.0332351 |     1.13478 |                     34.1441 |
| LZ4                      |  0.023663 |      1.1127 |                     47.0225 |
| RAR                      |  0.308938 |     1.10265 |                     3.56915 |
| ZIP                      |  0.237154 |     1.08497 |                     4.57493 |


Test with "A few text files" sorted by "Time normalized compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      |  0.023663 |      1.1127 |                     47.0225 |
| ZSTD                     |  0.036551 |     1.61309 |                     44.1327 |
| PGZIP                    | 0.0332351 |     1.13478 |                     34.1441 |
| PGZIP (Best compression) | 0.0341132 |     1.13541 |                     33.2838 |
| LZ4 (Best compression)   |   0.13737 |     1.13707 |                      8.2774 |
| 7ZIP                     |  0.426743 |     2.15245 |                     5.04389 |
| PBZIP2                   |  0.279492 |     1.37485 |                     4.91911 |
| ZIP                      |  0.237154 |     1.08497 |                     4.57493 |
| RAR                      |  0.308938 |     1.10265 |                     3.56915 |
| ZSTD (Best compression)  |  0.928809 |     2.15193 |                     2.31687 |
| XZ                       |   1.49799 |     2.15023 |                     1.43541 |
| XZ (Best compression)    |   1.55916 |     2.15047 |                     1.37925 |
| LZMA                     |   1.56381 |      2.1419 |                     1.36967 |
| LZMA (Best compression)  |   1.57281 |     2.14211 |                     1.36197 |
| PLZIP                    |   1.64311 |     2.14013 |                     1.30249 |
| PLZIP (Best compression) |   2.30391 |     2.14365 |                    0.930438 |

### A few mixed files

Test with "A few mixed files" sorted by "Time"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      | 0.0194356 |     1.99491 |                     102.642 |
| PGZIP                    | 0.0281055 |      2.8725 |                     102.204 |
| ZSTD                     | 0.0360215 |     3.09782 |                     85.9993 |
| PGZIP (Best compression) | 0.0510929 |      2.8845 |                     56.4561 |
| PBZIP2                   | 0.0964587 |      3.3937 |                     35.1829 |
| RAR                      |   0.16964 |     3.48817 |                     20.5622 |
| LZ4 (Best compression)   |  0.175575 |     2.56754 |                     14.6237 |
| ZIP                      |  0.249501 |     2.77821 |                     11.1351 |
| 7ZIP                     |  0.524823 |     4.15235 |                     7.91191 |
| XZ                       |   1.22789 |     4.16868 |                       3.395 |
| LZMA                     |   1.23839 |      4.1687 |                     3.36623 |
| PLZIP                    |   1.26057 |     4.15287 |                     3.29444 |
| LZMA (Best compression)  |   1.29071 |      4.1687 |                     3.22976 |
| ZSTD (Best compression)  |   1.42642 |     3.75015 |                     2.62906 |
| XZ (Best compression)    |   1.44246 |     4.16868 |                     2.88998 |
| PLZIP (Best compression) |   2.02732 |     4.18295 |                     2.06329 |


Test with "A few mixed files" sorted by "Compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| PLZIP (Best compression) |   2.02732 |     4.18295 |                     2.06329 |
| LZMA (Best compression)  |   1.29071 |      4.1687 |                     3.22976 |
| LZMA                     |   1.23839 |      4.1687 |                     3.36623 |
| XZ (Best compression)    |   1.44246 |     4.16868 |                     2.88998 |
| XZ                       |   1.22789 |     4.16868 |                       3.395 |
| PLZIP                    |   1.26057 |     4.15287 |                     3.29444 |
| 7ZIP                     |  0.524823 |     4.15235 |                     7.91191 |
| ZSTD (Best compression)  |   1.42642 |     3.75015 |                     2.62906 |
| RAR                      |   0.16964 |     3.48817 |                     20.5622 |
| PBZIP2                   | 0.0964587 |      3.3937 |                     35.1829 |
| ZSTD                     | 0.0360215 |     3.09782 |                     85.9993 |
| PGZIP (Best compression) | 0.0510929 |      2.8845 |                     56.4561 |
| PGZIP                    | 0.0281055 |      2.8725 |                     102.204 |
| ZIP                      |  0.249501 |     2.77821 |                     11.1351 |
| LZ4 (Best compression)   |  0.175575 |     2.56754 |                     14.6237 |
| LZ4                      | 0.0194356 |     1.99491 |                     102.642 |


Test with "A few mixed files" sorted by "Time normalized compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      | 0.0194356 |     1.99491 |                     102.642 |
| PGZIP                    | 0.0281055 |      2.8725 |                     102.204 |
| ZSTD                     | 0.0360215 |     3.09782 |                     85.9993 |
| PGZIP (Best compression) | 0.0510929 |      2.8845 |                     56.4561 |
| PBZIP2                   | 0.0964587 |      3.3937 |                     35.1829 |
| RAR                      |   0.16964 |     3.48817 |                     20.5622 |
| LZ4 (Best compression)   |  0.175575 |     2.56754 |                     14.6237 |
| ZIP                      |  0.249501 |     2.77821 |                     11.1351 |
| 7ZIP                     |  0.524823 |     4.15235 |                     7.91191 |
| XZ                       |   1.22789 |     4.16868 |                       3.395 |
| LZMA                     |   1.23839 |      4.1687 |                     3.36623 |
| PLZIP                    |   1.26057 |     4.15287 |                     3.29444 |
| LZMA (Best compression)  |   1.29071 |      4.1687 |                     3.22976 |
| XZ (Best compression)    |   1.44246 |     4.16868 |                     2.88998 |
| ZSTD (Best compression)  |   1.42642 |     3.75015 |                     2.62906 |
| PLZIP (Best compression) |   2.02732 |     4.18295 |                     2.06329 |
