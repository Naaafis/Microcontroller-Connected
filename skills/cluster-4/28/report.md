#  Leader Election

Author: Nafis Abeer, Justin Lam, Daniel Shimon

Date: 2021-04-12
-----

## Summary
The purpose of this skill was to create a leader election using the Bully Algorithm. After some trouble using UDP Client/Server code, we decided to instead use the UDP Multicast example in the esp-idf examples/protocol section. We first established this worked by connecting 4 ESPs to our router and verifying that they were receiving messages from eachother. From here, we modified the code to implement the Bull Algorithm. Multicasting allows us to send messages from all of the ESPs to eachother, and by keeping track of an election timer as well as a leader timer, in addition to keep track of Heartbeats sent by leaders to its non-leaders. Furthermore, by each ESP keeping track of its own ID as well as the maxID it recognizes in the system, the messages are sent accordingly and the system is able to converge to 1 recognized Leader by the system. This is seen as the leader sends a Heartbeat and the non-leaders receive one. 

Furthermore, if a leader is removed from the system the other ESPs recognize this as they no longer receive heartbeats, and start a new election process.


## Sketches and Photos
YouTube Video Demo:
https://youtu.be/NoQF20yhagw

## Modules, Tools, Source Used Including Attribution
ESP-IDF/Examples/Protocols/udp_multicast example

## Supporting Artifacts
![Code](./code/udp_multicast_example_main.c)

-----
