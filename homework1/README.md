# Homework #1

- Assigned: Monday, September 16
- Due: Monday (**Please print and submit the report before the lecture starts**), September 23
- If you have any questions, feel free to contact me (Mijin An / meeeeejin@gmail.com)

> NOTE: You should use Linux. (Recommend Ubuntu 16.04)

## Mount devices

- If you have more than one storage devices on your PC, read and try [this guide](reference/mount-guide.md) to separate data and log devices.

## Install MySQL 5.7 and TPC-C

- Follow the [installation guide](reference/tpcc-mysql-guide.md) to install and run TPC-C benchmark on MySQL 5.7.

## Collect performance information

- Follow [this guide](reference/performance-analysis-guide.md) to gather the necessary information
    1. Please specify the information of your system
    2. Write about the experiment environment
        - The full contents of `my.cnf`. For example:
        ```bash
        #
        # The MySQL database server configuration file.
        #
        [client]
        user    = root
        port    = 3306
        socket  = /tmp/mysql.sock

        [mysql]
        prompt  = \u:\d>\_

        [mysqld_safe]
        socket  = /tmp/mysql.sock

        [mysqld]
        # Basic settings
        default-storage-engine = innodb
        pid-file        = /path/to/datadir/mysql.pid
        socket          = /tmp/mysql.sock
        port            = 3306
        datadir         = /path/to/datadir/
        log-error       = /path/to/datadir/mysql_error.log

        #
        # Innodb settings
        #
        # Page size
        innodb_page_size=16KB

        # file-per-table ON
        innodb_file_per_table=1

        # Buffer settings
        innodb_buffer_pool_size=2G
        innodb_buffer_pool_instances=8
        innodb_lru_scan_depth=1024

        ...
        ```
        - Each configurable arguments of the TPC-C benchmark. For example:
        ```bash
        $ ./tpcc_start -h127.0.0.1 -S/tmp/mysql.sock -dtpcc100 -uroot -pyourPassword -w100 -c32 -r10 -l1200

        - Host: 127.0.0.1
        - MySQL Socket: /tmp/mysql.sock
        - DB: tpcc100
        - Warehouse: 100
        - Connection: 32
        - Rampup time: 10 (sec)
        - Measure: 1200 (sec)
        ```
    3. Collect performance information (I/O status and hit ratio) and capture them *when running the TPC-C benchmark*
    4. Show the result of the TPC-C benchmark
    5. Combine all the results, analyze them, and draw a conclusion