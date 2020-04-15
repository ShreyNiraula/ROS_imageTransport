# Throttle

- ref: [http://wiki.ros.org/topic_tools/throttle]

## Basic
- part of ros topic_tools
- node
- like buffer amplifier
- amplifies the incoming to outgoing with message rate maxed (or set to certain value) or bandwidth maxed (or at certain value)


## Structure
- subscribe to incoming topic 
- republishes the outgoing topic with default format as incomingtopic_throttle 


## Parameters
- 3 parameters to play with
	- wall_clock: works a/c to wall clock eventhough log/simulation time is in effect
	- unreliable:
		- asks for unreliable connection for income data
		- more faster transmission at risk of unreliability
		- like using udp instead of tcp

	- lazy: does not send any data till there is something that subscribe to its output topic, like saving unnecessary connection

## Usages
- throttle message (rate)
	- ```rosrun topic_tools throttle messages base_scan 1.0```
		- here, incoming topic of base_scan is set at message rate of 1Hz and republished as base_scan_throttle
		- since, outgoing topic is by default set as base_scan_throttle, we don't need to set its name in command 
		- for different output topic name, we can set it as ```rosrun topic_tools throttle messages base_scan 1.0 my_throttle_output```
		- now, doing above, output topic is named as my_throttle_output instead of base_scan_throttle

- throttle bytes (bandwidth)
	- instead of message rate, now bandwidth is used
	- ``` throttle bytes base_scan 1024 1.0```
		- here, incoming topic of base_scan is set at bandwirdth 1Kbps (or also called as __window__ size of 1kbps sample rate) and republished as base_scan_throttle
		
