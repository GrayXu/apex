<meta name="robots" content="noindex">

# APEX: High Performance Learned Index on Persistent Memory

More details are described in our [preprint](https://arxiv.org/abs/2105.00683).

## What's included

- APEX - the source code of APEX
- Mini benchmark framework

Fully open-sourced under MIT license.

## Building

### Dependencies
We tested our build with Linux Kernel 5.10.11 and GCC 10.2.0. You must ensure that your Linux kernel version >= 4.17 and glibc >=2.29 for proper build. 

### Compiling
Assuming to compile under a `build` directory:
```bash
git clone https://github.com/baotonglu/apex.git
cd apex
./build.sh
```

## Running benchmark

### Memory pool path
Please change the PM pool path of our allocator (./src/util/allocator.h) to the path on your own server.  

### Benchmark setting
We run the tests in a single NUMA node with 24 physical CPU cores. We pin threads to physical cores compactly assuming thread ID == 2 * core ID (e.g., for a dual-socket system, we assume cores 0, 2, 4, ... are located in socket 0).  Check out also the `total.sh` and `full.sh` script for example benchmarks and easy testing of the index. It supports the following arguments:

```bash

./build/benchmark [OPTION...]

--keys_file               the name of the dataset
--keys_file_type          the reading method for dataset (binary/text/sosd)
--keys_type               the type of the key (double/uint64)
--total_num_keys          total number of keys in the dataset
--init_num_keys           the number of keys to bulk-load before testing
--workload_keys           the number of keys in the workload
--operation               the query type in the workload (insert/search/erase/update/range/mixed)
--insert_frac             the fraction of insert in mixed search-insert workload
--lookup_distribution     the access distribution of the workload (uniform/zipf)
--theta                   the skewness of zipf (e.g.,0.9)
--using_epoch             whether to register epoch in application level: 0/1 
--thread_num              the number of worker threads 
--index                   the name of index to evaluate (apex)
--random_shuffle          whether to do the random shuffle for the dataset
--sort_bulkload           whether sort the keys before bulk-loading
```

## Competitors
Here hosts source codes which are used in comparision with APEX , including LB+-Tree [1], DPTree [2], uTree [3], FPTree [4], BzTree [5] and FAST+FAIR [6].

[1] https://github.com/schencoding/lbtree<br/>
[2] https://github.com/zxjcarrot/DPTree-code<br/>
[3] https://github.com/thustorage/nvm-datastructure<br/>
[4] https://github.com/sfu-dis/fptree<br/>
[5] https://github.com/sfu-dis/bztree<br/>
[6] https://github.com/DICL/FAST_FAIR

## Datasets
- [Longitudes (200M 8-byte floats)](https://drive.google.com/file/d/1zc90sD6Pze8UM_XYDmNjzPLqmKly8jKl/view?usp=sharing)
- [Longlat (200M 8-byte floats)](https://drive.google.com/file/d/1mH-y_PcLQ6p8kgAz9SB7ME4KeYAfRfmR/view?usp=sharing)
- [Lognormal (190M 8-byte ints)](https://drive.google.com/file/d/1y-UBf8CuuFgAZkUg_2b_G8zh4iF_N-mq/view?usp=sharing)
- [YCSB (200M 8-byte ints)](https://drive.google.com/file/d/1Q89-v4FJLEwIKL3YY3oCeOEs0VUuv5bD/view?usp=sharing)
- [FB (200M 8-byte ints)](https://github.com/learnedsystems/SOSD)
- [TPCE (259M 8-byte ints)](https://github.com/sfu-dis/ermia/tree/master/benchmarks/tpce_keys)


## Acknowledgements
Our implementation is based on the code of [ALEX](https://github.com/microsoft/ALEX).
