# Compression test


- [Compression test](#compression-test)
  - [Test setup](#test-setup)
    - [Commands](#commands)
  - [Results](#results)
    - [Artificial](#artificial)
    - [Calgary](#calgary)
    - [Canterbury](#canterbury)
    - [Large](#large)

I made some test on multiple of the compression algorithms and tools found on linux.

## Test setup
<!-- The algorithms were tested on the following situations:
 - **Lots of data with mixed types and sizes:** A lot of various types of files of varying sizes. The total size of all the files is 4.36 GiB
 - **Non-compressible data:** A lot of barely compressible files, in thes case jpeg images. The total size of all the files is 0.62 GiB
 - **A lot of many small text files:** A lot of small text files, all the files are under 1MB in size. The total size of all the files is 0.96 GiB
 - **A few text files:** A few text files. The total size of all the files is 9.54 MiB
 - **A few mixed files:** A few files varying in size and type. The total size of all the files is 6.66 MiB -->

The algorithms have been tested with the [canterbury corpus](https://en.wikipedia.org/wiki/Canterbury_corpus). Downloaded from [this repository](https://github.com/pfalcon/canterbury-corpus).

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

### Artificial

Test with "Artificial" sorted by "Time"

| Compression Algorithm    |       Time | Compression | Time normalized compression |
| :----------------------- | ---------: | ----------: | --------------------------: |
| LZ4                      | 0.00500178 |     2.94217 |                     588.224 |
| PGZIP                    | 0.00692916 |     3.89652 |                     562.336 |
| ZSTD                     | 0.00734138 |     3.96104 |                     539.549 |
| LZ4 (Best compression)   | 0.00752068 |     2.94896 |                     392.114 |
| ZIP                      | 0.00768423 |     3.87759 |                     504.617 |
| PGZIP (Best compression) | 0.00786114 |     3.89748 |                      495.79 |
| 7ZIP                     |  0.0215967 |     3.87664 |                     179.502 |
| PLZIP                    |  0.0232768 |     3.88643 |                     166.966 |
| RAR                      |  0.0236309 |     3.84245 |                     162.603 |
| ZSTD (Best compression)  |  0.0301487 |     3.96554 |                     131.532 |
| XZ                       |   0.030818 |     3.88426 |                     126.039 |
| LZMA                     |  0.0315187 |     3.88753 |                     123.341 |
| PBZIP2                   |  0.0370195 |      3.9214 |                     105.928 |
| PLZIP (Best compression) |   0.040936 |     3.88733 |                     94.9612 |
| XZ (Best compression)    |  0.0605237 |     3.88426 |                     64.1775 |
| LZMA (Best compression)  |  0.0609977 |     3.88753 |                     63.7324 |


Test with "Artificial" sorted by "Compression"

| Compression Algorithm    |       Time | Compression | Time normalized compression |
| :----------------------- | ---------: | ----------: | --------------------------: |
| ZSTD (Best compression)  |  0.0301487 |     3.96554 |                     131.532 |
| ZSTD                     | 0.00734138 |     3.96104 |                     539.549 |
| PBZIP2                   |  0.0370195 |      3.9214 |                     105.928 |
| PGZIP (Best compression) | 0.00786114 |     3.89748 |                      495.79 |
| PGZIP                    | 0.00692916 |     3.89652 |                     562.336 |
| LZMA (Best compression)  |  0.0609977 |     3.88753 |                     63.7324 |
| LZMA                     |  0.0315187 |     3.88753 |                     123.341 |
| PLZIP (Best compression) |   0.040936 |     3.88733 |                     94.9612 |
| PLZIP                    |  0.0232768 |     3.88643 |                     166.966 |
| XZ (Best compression)    |  0.0605237 |     3.88426 |                     64.1775 |
| XZ                       |   0.030818 |     3.88426 |                     126.039 |
| ZIP                      | 0.00768423 |     3.87759 |                     504.617 |
| 7ZIP                     |  0.0215967 |     3.87664 |                     179.502 |
| RAR                      |  0.0236309 |     3.84245 |                     162.603 |
| LZ4 (Best compression)   | 0.00752068 |     2.94896 |                     392.114 |
| LZ4                      | 0.00500178 |     2.94217 |                     588.224 |


Test with "Artificial" sorted by "Time normalized compression"

| Compression Algorithm    |       Time | Compression | Time normalized compression |
| :----------------------- | ---------: | ----------: | --------------------------: |
| LZ4                      | 0.00500178 |     2.94217 |                     588.224 |
| PGZIP                    | 0.00692916 |     3.89652 |                     562.336 |
| ZSTD                     | 0.00734138 |     3.96104 |                     539.549 |
| ZIP                      | 0.00768423 |     3.87759 |                     504.617 |
| PGZIP (Best compression) | 0.00786114 |     3.89748 |                      495.79 |
| LZ4 (Best compression)   | 0.00752068 |     2.94896 |                     392.114 |
| 7ZIP                     |  0.0215967 |     3.87664 |                     179.502 |
| PLZIP                    |  0.0232768 |     3.88643 |                     166.966 |
| RAR                      |  0.0236309 |     3.84245 |                     162.603 |
| ZSTD (Best compression)  |  0.0301487 |     3.96554 |                     131.532 |
| XZ                       |   0.030818 |     3.88426 |                     126.039 |
| LZMA                     |  0.0315187 |     3.88753 |                     123.341 |
| PBZIP2                   |  0.0370195 |      3.9214 |                     105.928 |
| PLZIP (Best compression) |   0.040936 |     3.88733 |                     94.9612 |
| XZ (Best compression)    |  0.0605237 |     3.88426 |                     64.1775 |
| LZMA (Best compression)  |  0.0609977 |     3.88753 |                     63.7324 |

### Calgary

Test with "Calgary" sorted by "Time"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      | 0.0139112 |       1.928 |                     138.593 |
| PGZIP                    | 0.0204134 |     3.04514 |                     149.174 |
| ZSTD                     | 0.0300949 |     3.06354 |                     101.796 |
| PGZIP (Best compression) | 0.0378704 |     3.06692 |                     80.9846 |
| PBZIP2                   |  0.063678 |     3.65207 |                     57.3522 |
| RAR                      | 0.0703645 |      3.3894 |                     48.1692 |
| ZIP                      |  0.124563 |     3.03758 |                     24.3858 |
| LZ4 (Best compression)   |  0.220412 |      2.6397 |                     11.9762 |
| 7ZIP                     |  0.315797 |     3.79749 |                     12.0251 |
| XZ                       |  0.733703 |     3.80797 |                     5.19007 |
| ZSTD (Best compression)  |  0.745826 |     3.63498 |                     4.87377 |
| LZMA                     |  0.765039 |     3.80878 |                     4.97855 |
| XZ (Best compression)    |  0.783136 |     3.80797 |                     4.86246 |
| PLZIP                    |  0.797309 |     3.79922 |                     4.76505 |
| LZMA (Best compression)  |  0.869179 |     3.80878 |                     4.38205 |
| PLZIP (Best compression) |   1.05285 |     3.82562 |                     3.63359 |


Test with "Calgary" sorted by "Compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| PLZIP (Best compression) |   1.05285 |     3.82562 |                     3.63359 |
| LZMA (Best compression)  |  0.869179 |     3.80878 |                     4.38205 |
| LZMA                     |  0.765039 |     3.80878 |                     4.97855 |
| XZ (Best compression)    |  0.783136 |     3.80797 |                     4.86246 |
| XZ                       |  0.733703 |     3.80797 |                     5.19007 |
| PLZIP                    |  0.797309 |     3.79922 |                     4.76505 |
| 7ZIP                     |  0.315797 |     3.79749 |                     12.0251 |
| PBZIP2                   |  0.063678 |     3.65207 |                     57.3522 |
| ZSTD (Best compression)  |  0.745826 |     3.63498 |                     4.87377 |
| RAR                      | 0.0703645 |      3.3894 |                     48.1692 |
| PGZIP (Best compression) | 0.0378704 |     3.06692 |                     80.9846 |
| ZSTD                     | 0.0300949 |     3.06354 |                     101.796 |
| PGZIP                    | 0.0204134 |     3.04514 |                     149.174 |
| ZIP                      |  0.124563 |     3.03758 |                     24.3858 |
| LZ4 (Best compression)   |  0.220412 |      2.6397 |                     11.9762 |
| LZ4                      | 0.0139112 |       1.928 |                     138.593 |


Test with "Calgary" sorted by "Time normalized compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| PGZIP                    | 0.0204134 |     3.04514 |                     149.174 |
| LZ4                      | 0.0139112 |       1.928 |                     138.593 |
| ZSTD                     | 0.0300949 |     3.06354 |                     101.796 |
| PGZIP (Best compression) | 0.0378704 |     3.06692 |                     80.9846 |
| PBZIP2                   |  0.063678 |     3.65207 |                     57.3522 |
| RAR                      | 0.0703645 |      3.3894 |                     48.1692 |
| ZIP                      |  0.124563 |     3.03758 |                     24.3858 |
| 7ZIP                     |  0.315797 |     3.79749 |                     12.0251 |
| LZ4 (Best compression)   |  0.220412 |      2.6397 |                     11.9762 |
| XZ                       |  0.733703 |     3.80797 |                     5.19007 |
| LZMA                     |  0.765039 |     3.80878 |                     4.97855 |
| ZSTD (Best compression)  |  0.745826 |     3.63498 |                     4.87377 |
| XZ (Best compression)    |  0.783136 |     3.80797 |                     4.86246 |
| PLZIP                    |  0.797309 |     3.79922 |                     4.76505 |
| LZMA (Best compression)  |  0.869179 |     3.80878 |                     4.38205 |
| PLZIP (Best compression) |   1.05285 |     3.82562 |                     3.63359 |

### Canterbury

Test with "Canterbury" sorted by "Time"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      | 0.0113311 |     2.28631 |                     201.773 |
| PGZIP                    | 0.0188959 |     3.82866 |                     202.619 |
| ZSTD                     | 0.0193903 |     4.38005 |                     225.888 |
| PBZIP2                   | 0.0492446 |     4.94642 |                     100.446 |
| RAR                      | 0.0585382 |     5.45329 |                     93.1579 |
| PGZIP (Best compression) | 0.0595274 |     3.84635 |                     64.6147 |
| ZIP                      | 0.0982521 |     3.81731 |                     38.8522 |
| 7ZIP                     |  0.331636 |     5.78365 |                     17.4398 |
| XZ                       |  0.630135 |     5.78572 |                     9.18172 |
| LZMA                     |  0.638212 |      5.7872 |                     9.06784 |
| ZSTD (Best compression)  |  0.644854 |     5.45402 |                     8.45777 |
| XZ (Best compression)    |  0.658105 |     5.78572 |                     8.79149 |
| LZMA (Best compression)  |  0.674388 |      5.7872 |                     8.58141 |
| PLZIP                    |  0.709754 |     5.77106 |                     8.13107 |
| LZ4 (Best compression)   |  0.981928 |     3.01902 |                     3.07458 |
| PLZIP (Best compression) |   1.07809 |     5.83406 |                     5.41146 |


Test with "Canterbury" sorted by "Compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| PLZIP (Best compression) |   1.07809 |     5.83406 |                     5.41146 |
| LZMA (Best compression)  |  0.674388 |      5.7872 |                     8.58141 |
| LZMA                     |  0.638212 |      5.7872 |                     9.06784 |
| XZ (Best compression)    |  0.658105 |     5.78572 |                     8.79149 |
| XZ                       |  0.630135 |     5.78572 |                     9.18172 |
| 7ZIP                     |  0.331636 |     5.78365 |                     17.4398 |
| PLZIP                    |  0.709754 |     5.77106 |                     8.13107 |
| ZSTD (Best compression)  |  0.644854 |     5.45402 |                     8.45777 |
| RAR                      | 0.0585382 |     5.45329 |                     93.1579 |
| PBZIP2                   | 0.0492446 |     4.94642 |                     100.446 |
| ZSTD                     | 0.0193903 |     4.38005 |                     225.888 |
| PGZIP (Best compression) | 0.0595274 |     3.84635 |                     64.6147 |
| PGZIP                    | 0.0188959 |     3.82866 |                     202.619 |
| ZIP                      | 0.0982521 |     3.81731 |                     38.8522 |
| LZ4 (Best compression)   |  0.981928 |     3.01902 |                     3.07458 |
| LZ4                      | 0.0113311 |     2.28631 |                     201.773 |


Test with "Canterbury" sorted by "Time normalized compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| ZSTD                     | 0.0193903 |     4.38005 |                     225.888 |
| PGZIP                    | 0.0188959 |     3.82866 |                     202.619 |
| LZ4                      | 0.0113311 |     2.28631 |                     201.773 |
| PBZIP2                   | 0.0492446 |     4.94642 |                     100.446 |
| RAR                      | 0.0585382 |     5.45329 |                     93.1579 |
| PGZIP (Best compression) | 0.0595274 |     3.84635 |                     64.6147 |
| ZIP                      | 0.0982521 |     3.81731 |                     38.8522 |
| 7ZIP                     |  0.331636 |     5.78365 |                     17.4398 |
| XZ                       |  0.630135 |     5.78572 |                     9.18172 |
| LZMA                     |  0.638212 |      5.7872 |                     9.06784 |
| XZ (Best compression)    |  0.658105 |     5.78572 |                     8.79149 |
| LZMA (Best compression)  |  0.674388 |      5.7872 |                     8.58141 |
| ZSTD (Best compression)  |  0.644854 |     5.45402 |                     8.45777 |
| PLZIP                    |  0.709754 |     5.77106 |                     8.13107 |
| PLZIP (Best compression) |   1.07809 |     5.83406 |                     5.41146 |
| LZ4 (Best compression)   |  0.981928 |     3.01902 |                     3.07458 |

### Large

Test with "Large" sorted by "Time"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| LZ4                      | 0.0310037 |     1.92368 |                     62.0468 |
| ZSTD                     | 0.0540023 |     3.45881 |                     64.0493 |
| PGZIP                    | 0.0762684 |     3.42005 |                     44.8423 |
| PBZIP2                   | 0.0938406 |     4.26873 |                     45.4891 |
| RAR                      |  0.146149 |     3.94542 |                     26.9958 |
| PGZIP (Best compression) |  0.204228 |     3.48357 |                     17.0572 |
| ZIP                      |  0.935222 |     3.42537 |                     3.66263 |
| LZ4 (Best compression)   |    2.2331 |     2.95496 |                     1.32326 |
| 7ZIP                     |   2.33647 |     4.34037 |                     1.85766 |
| XZ                       |   3.90453 |     4.36674 |                     1.11838 |
| ZSTD (Best compression)  |   3.95725 |     4.37968 |                     1.10675 |
| XZ (Best compression)    |   4.03401 |     4.36679 |                     1.08249 |
| LZMA                     |   4.04633 |      4.3675 |                     1.07938 |
| LZMA (Best compression)  |   4.15799 |     4.36756 |                      1.0504 |
| PLZIP                    |   4.66973 |     4.33882 |                    0.929137 |
| PLZIP (Best compression) |    4.9531 |     4.36848 |                    0.881968 |


Test with "Large" sorted by "Compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| ZSTD (Best compression)  |   3.95725 |     4.37968 |                     1.10675 |
| PLZIP (Best compression) |    4.9531 |     4.36848 |                    0.881968 |
| LZMA (Best compression)  |   4.15799 |     4.36756 |                      1.0504 |
| LZMA                     |   4.04633 |      4.3675 |                     1.07938 |
| XZ (Best compression)    |   4.03401 |     4.36679 |                     1.08249 |
| XZ                       |   3.90453 |     4.36674 |                     1.11838 |
| 7ZIP                     |   2.33647 |     4.34037 |                     1.85766 |
| PLZIP                    |   4.66973 |     4.33882 |                    0.929137 |
| PBZIP2                   | 0.0938406 |     4.26873 |                     45.4891 |
| RAR                      |  0.146149 |     3.94542 |                     26.9958 |
| PGZIP (Best compression) |  0.204228 |     3.48357 |                     17.0572 |
| ZSTD                     | 0.0540023 |     3.45881 |                     64.0493 |
| ZIP                      |  0.935222 |     3.42537 |                     3.66263 |
| PGZIP                    | 0.0762684 |     3.42005 |                     44.8423 |
| LZ4 (Best compression)   |    2.2331 |     2.95496 |                     1.32326 |
| LZ4                      | 0.0310037 |     1.92368 |                     62.0468 |


Test with "Large" sorted by "Time normalized compression"

| Compression Algorithm    |      Time | Compression | Time normalized compression |
| :----------------------- | --------: | ----------: | --------------------------: |
| ZSTD                     | 0.0540023 |     3.45881 |                     64.0493 |
| LZ4                      | 0.0310037 |     1.92368 |                     62.0468 |
| PBZIP2                   | 0.0938406 |     4.26873 |                     45.4891 |
| PGZIP                    | 0.0762684 |     3.42005 |                     44.8423 |
| RAR                      |  0.146149 |     3.94542 |                     26.9958 |
| PGZIP (Best compression) |  0.204228 |     3.48357 |                     17.0572 |
| ZIP                      |  0.935222 |     3.42537 |                     3.66263 |
| 7ZIP                     |   2.33647 |     4.34037 |                     1.85766 |
| LZ4 (Best compression)   |    2.2331 |     2.95496 |                     1.32326 |
| XZ                       |   3.90453 |     4.36674 |                     1.11838 |
| ZSTD (Best compression)  |   3.95725 |     4.37968 |                     1.10675 |
| XZ (Best compression)    |   4.03401 |     4.36679 |                     1.08249 |
| LZMA                     |   4.04633 |      4.3675 |                     1.07938 |
| LZMA (Best compression)  |   4.15799 |     4.36756 |                      1.0504 |
| PLZIP                    |   4.66973 |     4.33882 |                    0.929137 |
| PLZIP (Best compression) |    4.9531 |     4.36848 |                    0.881968 |
