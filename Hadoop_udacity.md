#### Basic concepts:
- 3 Vs (3 dimensions of big data): volumn, variety, velocity
    + variery: data format
- Hadoop consists of:
    + store data: in HDFS (hadoop distribited file system)
        * stores in a collection of machines: clusters
    + process data: MapReduce
        * process at where it actually stores
- Hadoop ecosystem:
    + On top of MapReduce (which requires programming skils), there are `Pig` (hive level scripting language) and `Hive` (offer a SQL-like language on top of MR) that helps people run MapReduce jobs without knowing how to write one.
    + Impala (no need to go thru MR, just directly access data in HDFS)
    + and so on...

#### HDFS
- A files is divided to smaller pieaces and saved to different data nodes on different machines. There is also a `name node` to let us know which blocks make up the original file. The information stored on the name node is called **metadata**.

#### MapReduce
- Basic ideas
    + process data serially from top to bottom might take long time.
    + MR is designed to process data in parallel. i.e. file is broken into chunks, and then processed in parallel.
- Steps
    1. each of the mappers deal with a relatively small amount of data and work in parallel (intermediate records: (key, value))
    2. shuffle and sort
    3. each reducer work on one set of records (we don't know how many records eawch reducer might get, it could be nothing - see `Partitioning Data`)

#### Partitioning Data
- "Partitioning" is the process of **determining which reducer instance will receive which intermediate keys and values**. Each mapper must determine for all of its output (key, value) pairs which reducer will receive them. It is necessary that for any key, regardless of which mapper instance generated it, the destination partition is the same. If the key "cat" is generated in two separate (key, value) pairs, they must both be reduced together. It is also important for performance reasons that the mappers be able to partition data independently -- they should never need to exchange information with one another to determine the partition for a particular key.

#### Problem patterns (that we could use MapReduce to solve)
- Filtering patterns
    + sampling
    + top-N
- Summarization patterns
    + counting
    + min/max
    + stats
    + index
- structural patterns
    + combining data sets

###### Filtering patterns







 