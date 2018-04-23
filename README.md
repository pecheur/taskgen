# taskgen

A taskset generation framework for the
[genode-Taskloader](https://github.com/argos-research/genode-Taskloader)
component.


# Installation

Only Ubuntu 16.04 with the default python version 3.5 is supported.

```
git clone https://github.com/argos-research/taskgen.git
cd taskgen
make install
```

If you want to use the MongoDB backend & RoboMongo:

```
make mongodb
sudo service mongod start
make robomongo
```


# Getting started

The core of taskgen is the distribution of task-sets to running
genode-Taskloader instances. taskgen is shipped with a command line tool.


```bash
./taskgen-cli --help
```

Use the tool to list all available tasksets:

```bash
./taskgen-cli list --taskset
```

Task-sets in `example.*` are good starting points for testing and exploring
taskgen.

The next command distributes the `example.Hey0TaskSet` task-set to a running
Genode instance at IP address `172.25.0.1`.

```bash
./taskgen-cli run -t example.Hey0TaskSet 172.25.0.1
```


General Workflow
================

1. Choose a task-set class
3. Optionally choose a monitor class for monitoring and recording task runtime
   behaviour.
4. Optionally choose a session for a target platform.
5. Start sending and processing task-set.

These steps can be done by using the [command line tool](docs/commandline.md). It is
also possible to directly use the [`Distributor`](docs/distributor.md) class in a
python script.


Components of taskgen
=====================
  
* [**Task**](docs/tasks.md) A Task consists of key-value pairs, which describes
  the behavior of a real-time capable process. For example: one key could be `priority` and
  its associated value might be `25`. Tasks are implemented as python
  dictionaries.  
  
* [**Task Blocks**](docs/blocks.md) are building blocks for a task and are
  represented with key-value pairs, too.  A (task) block is a dictionary object or
  a function which returns a dictionary object.  
  
* [**Task-Sets**](docs/taskset.md) are containers for tasks.  

* [**Admission Control**](docs/admctrl.md) objects contains optimization goals
  for a task-set. Optimizations are represented by python dictionaries.  
  
* [**Monitors**](docs/monitor.md) handle occuring events. An event is fired,
  whenever a task processing starts or ends.  
  
* [**Distributor**](docs/distributor.md) sends a task-set and its optimization
  goal to a platform, which is able to execute task-sets. The low level
  connection to such a platform is realized with a **Session**.  
  
* [**Sessions**](docs/session.md) contain the low level implementations for
  sending task-sets, optimization classes and for receiving events.  
  
![Overview of all components](design_overview.png "Overview of all components.")














# Documentation
* [Overview](docs/overview.md)
* [Command line](docs/commandline.md)
* [Distributors](docs/distributor.md)
* [Task-Sets](docs/taskset.md)
* [Tasks](docs/tasks.md)
* [Task Blocks](docs/blocks.md)
* [Admission Control](docs/admctrl.md)
* [Monitors](docs/monitor.md)
* [Sessions](docs/session.md)
* [Dictionary to XML format](docs/dict2xml.md)
* [Qemu Startup Script](docs/qemu.md)
