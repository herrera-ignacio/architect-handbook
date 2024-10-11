# HBase Shell

> Please refer to https://hbase.apache.org/book.html#quickstart for latest docs.

> Troubleshooting Windows 10: 
> * HBase standalone mode setup guided: https://www.learntospark.com/2020/08/setup-hbase-in-windows.html
> * jruby: https://www.ibm.com/mysupport/s/question/0D50z000060GHZZ/hbase-shell-not-starting?language=en_US

## Requirements

> Last time I tested, I got it working usign HBase 2.3.5, Hadoop 3.2.1, and JDK8. 

1. Download a stable release of *HBase* binary.
2. You must set `JAVA_HOME` environment variable before starting HBase (you can also set it within the `conf/hbase-env.sh` file).
3. The `bin/start-hbase.sh` script is provided as a convenient way to start HBase. You can use the `jps` command to verify that you have one running process called *HMaster*.
4. Go to http://localhost:16010 to view the HBase Web UI.

> In standalone mode HBase runs all daemons within this single JVM, i.e. the HMaster, a single HRegionServion, and the ZooKeeper daemon.

`bin/stop-hbase.sh` scripts is provided to conveniently stop all HBase daemons.

## Connect to HBase

Connect to your running instance of HBase using the `hbase shell`  commnand located in the `bin/` directory of your HBase install.

```
$ ./bin/hbase shell
```

You can type `help` to display some basic usage information for HBase Shell, as well as several example commands. Notice that table names, rows, columns all must be enclosed in quote characters.

## Examples

Check the latest [*HBase* quickstart documentation](https://hbase.apache.org/book.html#quickstart) for examples such as:

* Create table
* Query table `list`, `describe`, `scan`, `get`, `drop`
* Put data into your table `put`

