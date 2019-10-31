# TerarkDB

## Dependencies
- terark-core
  - Terark's core algorithms, including CO-Index and PA-Zip etc.

## Documentation
[Documentation](https://bytedance.feishu.cn/space/doc/doccnPkcQEZ10MmaIKZTow#)


## Build

1. checkout the latest tag version
2. `./build.sh` or `env DEBUG_ENV=1 ./build.sh` for debug version
3. find static / dynamic libraries inside output directory

the output directory looks like this:

```
output
    \__ include
    \__ lib_static
        \__ librocksdb.a
        \__ ...
```

** NOTICE:

- The static library `librocksdb.a` already includes zstd, boost-filesystem and boost-fiber
- additional requrements shoud be linked manually:
 - `-lsnappy`
 - `-llz4`
 - `-lz`
 - `-lgomp`
 - `-laio`
 - `-lrt`

## Usage
If you want to use it as original rocksdb, you can just include librocksdb and the headers.

If you want to enable TerarkDB, then you have to pass these environment variables before you start you application, e.g.


```
env TerarkZipTable_localTempDir=$PWD/terark-tempdir ./app_executable
```


## Valgrind
If you want to use `Valgrind`, please build terarkdb this way:

```
USE_VALGRIND=1 ./build.sh
```

And add a new env when you start your application:

```
env Terark_hasValgrind=1 ./application
```
