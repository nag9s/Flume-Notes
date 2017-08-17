In the VM web browser, open Hue.

Click File Browser.

Create the /flume/events directory.

```
In the /user/cloudera directory, click New-&gt;Directory.

Create a directory named flume.

In the flume directory, create a directory named events.

Check the box to the left of the events directory, then click the Permissions setting.

Enable Write access for Group and Other users.

Click Submit.
```

Change the Flume configuration.

In the below example, netcat is the source and the output from the netcat will be stored to HDFS using Memory channel

```
Open Cloudera Manager in your web browser.

In the list of services, click Flume.

Click the Configuration tab.

Scroll or search for the Configuration File item.


# Please paste flume.conf here. Example:

# Sources, channels, and sinks are defined per
# agent name, in this case 'tier1'.
tier1.sources  = source1
tier1.channels = channel1
tier1.sinks    = sink1

# For each source, channel, and sink, set
# standard properties.
tier1.sources.source1.type     = netcat
tier1.sources.source1.bind     = 127.0.0.1
tier1.sources.source1.port     = 9999
tier1.sources.source1.channels = channel1
tier1.channels.channel1.type   = memory
tier1.sinks.sink1.type= HDFS
tier1.sinks.sink1.fileType=DataStream
tier1.sinks.sink1.channel      = channel1
tier1.sinks.sink1.hdfs.path = hdfs://localhost:8020/user/cloudera/flume/events

# Other properties are specific to each type of
# source, channel, or sink. In this case, we
# specify the capacity of the memory channel.
tier1.channels.channel1.capacity = 100
```

At the top of the settings list, click

On the far right, choose Actions-&gt;Restart  to restart Flume.

When the restrart is complete, click Close

### Passing Data to the Source

To pass data to NetCat source, you have to open the port given in the configuration file. Open a separate terminal and connect to the source \(56565\) using the **curl** command. When the connection is successful, you will get a message “**connected**” as shown below.

```
$ curl telnet://localhost:9999

Ok
```

.`[cloudera@quickstart ~]$ curl telnet://localhost:9999    
OK`

`hello`

`OK`

`here is flume`

`OK`

`demo`

`OK`

`^C`

`[cloudera@quickstart ~]$`





In the Hue File Browser, open the 

/user/cloudera/flume/events

 directory.

There will be a file named 

FlumeData

 with a serial number as the file extension. Click the file name link to view the data sent by Flume to HDFS.



