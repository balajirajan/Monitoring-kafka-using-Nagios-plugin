# Monitoring-kafka-using-Nagios-plugin

To find the value of a particular Object name from Kafka server, there is a plugin called check_jmx which enables you to monitor JMX attributes and fetch the value in Nagios. 
we don't need to write any python / bash script to fetch the value :)

We can monitor any JVM parameter that can be accessed by JMX. lets say for an example, to monitor java HeapMemorySize of Kafka.
Also want to alert if the memory usage goes above a particular numbers.

1. Down load the plugin:

2. extract it and cd to check_jmx/nagios/plugin

3. run the command:  
./check_jmx -U service:jmx:rmi:///jndi/rmi://$hostname:$port/jmxrmi -O java.lang:type=Memory -A HeapMemoryUsage -K used -I HeapMemoryUsage -J used -vvvv -w 4248302272 -c 5498760192 


* -U is for JMX url
* -O is for Object name to be checked
* -A is for Attribute of the object to be checked
* -K is for Attribute key for -A attribute compound data
* -I is for Attribute of the object containing information for text output
* -J is for Attribute key for -I attribute compound data
* -v is for verbose level 
* Here i have assigned 4GB as Warning level(-w) and  5GB(-c) as Critical level. but this can be configured based on our requirements.


4. Output of the command is seems OK.
 JMX OK HeapMemoryUsage.used=70437104{committed=202899456;init=209715200;max=608174080;used=70437104} | committed=202899456; init=209715200; max=608174080; used=70437104;

Thats all :) 




