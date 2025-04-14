# MongoDB 8.0 Community Edition

## Installing MongoDB 8.0 Community Edition on MacOS

1. Tap the MongoDB Homebrew Tap to download the official Homebrew formula for MongoDB and the Database Tools, by running the following command in your macOS Terminal:

   ```bash
   brew tap mongodb/brew
   ```

   If you have already done this for a previous installation of MongoDB, you can skip this step.

2. To update Homebrew and all existing formulae:

   ```bash
   brew update
   ```

3. To install MongoDB, run the following command in your macOS Terminal application:

   ```bash
   brew install mongodb-community@8.0
   ```

The installation includes the following binaries:

- The `mongod` server
- The `mongos` sharded cluster query router
- The MongoDB Shell, `mongosh`

In addition, the installation creates the following files and directories at the location specified below, depending on your Apple hardware:

|                    | Intel Processor            | Apple Silicon Processor       |
| ------------------ | -------------------------- | ----------------------------- |
| configuration file | /usr/local/etc/mongod.conf | /opt/homebrew/etc/mongod.conf |
| log directory      | /usr/local/var/log/mongodb | /opt/homebrew/var/log/mongodb |
| data directory     | /usr/local/var/mongodb     | /opt/homebrew/var/mongodb     |

You can also run the following command to check where `brew` has installed these files and directories:

```bash
brew --prefix
```

---

## Run MongoDB Community Edition

These instructions assume that you are using the default settings.

You can run MongoDB as a macOS service using `brew`, or you can run MongoDB manually as a background process. It is recommended to run MongoDB as a macOS service, as doing so sets the correct system `ulimit` values automatically

### Run MongoDB (i.e. the `mongod` process) as a macOS service, run:

```bash
brew services start mongodb-community@8.0
```

or

```bash
brew services start mongodb/brew/mongodb-community
```

To stop a `mongod` running as a macOS service, use the following command as needed:

```bash
brew services stop mongodb-community@8.0
```

### Run `mongod` manually as a background process using a config file

If your deployment does not use `TLS connections`, use the --fork option:

- For macOS running on Intel processors, run:

  ```bash
  mongod --config /usr/local/etc/mongod.conf --fork
  ```

- For macOS running on `Apple Silicon processors`, run:

  ```bash
  mongod --config /opt/homebrew/etc/mongod.conf --fork
  ```

- If your deployment uses `TLS connections`, use `GNU Screen`.

  - For macOS running on Intel processors:

    1. Start your screen.
       ```bash
       screen -S <name-of-screen>
       ```
    2. Start `mongod`.
       ```bash
       mongod --config /usr/local/etc/mongod.conf
       ```
    3. Detach from screen.
       Detach from your screen by typing `Ctrl+a`, then clicking `d`.
    4. View all active screens.
       ```bash
       screen -ls
       ```

  - For macOS running on Apple Silicon processors:

    1. Start your screen.

    ```bash
    screen -S <name-of-screen>
    ```

    2. Start `mongod`.

    ```bash
    mongod --config /opt/homebrew/etc/mongod.conf
    ```

    3. Detach from screen.
       Detach from your screen by typing `Ctrl+a`, then clicking `d`.

    4. View all active screens.

    ```bash
    screen -ls
    ```

### Run `mongod` manually as a background process specifying `--dbpath` and `--logpath` on the command line

```bash
mongod --dbpath /path/to/dbdir --logpath /path/to/mongodb.log --fork
```

To stop a `mongod` running as a background process, connect to the `mongod` using `mongosh`, and issue the `shutdown` command as needed.

## Verify that MongoDB is running

### If you started MongoDB as a macOS service

```bash
brew services list
```

You should see the service `mongodb-community` listed as `started`.

### If you started MongoDB manually as a background process

```bash
ps aux | grep -v grep | grep mongod
```

You should see your `mongod` process in the output.

You can also view the log file to see the current status of your mongod process: `/usr/local/var/log/mongodb/mongo.log`.

## Connect and Use MongoDB

To begin using MongoDB, connect `mongosh` to the running instance. From a new terminal, issue the following:

```bash
mongosh
```
