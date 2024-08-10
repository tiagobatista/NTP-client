# NTP-client

NTP is a networking protocol for clock synchronisation between network attached devices. It is one of the oldest Internet protocols in current use.

NTP is intended to synchronise computers to within a few milliseconds of each other. It uses the intersection algorithm, a modified version of Marzullo's algorithm, to select accurate time servers and is designed to mitigate the effects of variable network latency.

Over the public Internet NTP can usually maintain time to within tens of milliseconds and on a local area network can usually do better than one millisecond accuracy.

However, asymmetric routes and network congestion can cause the accuracy to decrease.

The protocol is usually described in terms of a client–server model, but can also be used in peer-to-peer relationships. Clients and servers using NTP send and receive timestamps as UDP packets on port 123.

The full protocol is defined in the NTP RFC which is RFC 5905.

Step Zero

In this step you’re going to set your environment up ready to begin developing and testing your NTP client solution.

I’ll leave you to setup your editor and programming language of choice. I’d encourage you to pick a tech stack that you’re comfortable doing network programming in.

Step 1

In this step your goal is to send a request to an NTP server and receive the response back. You’ll need to contact the NTP server on port 123. The message you’ll need to send is defined in the RFC under section 7 on page 19. Take care to understand which fields you set for the outgoing message.

NTP uses a hierarchical, semi-layered system of time sources. Each level of the hierarchy is termed a stratum and is assigned a number starting with zero for the reference clock at the top.

A server synchronised to a stratum n server is considered to be a stratum n + 1 server. The number represents the distance from the reference clock and is used to prevent cyclical dependencies in the hierarchy. The stratum is not always an indication of the quality or reliability of the server.

For this challenge you can find a list of time servers you can use here or you can use one from the NTP Pool Project.

The packet you get back will have the same structure as packet you sent, check that the first three fields are correct then proceed to Step 2.

Step 2

In this step your goal is to decode the response from the NTP server and print out the four timestamps in the packet.

The obvious test here is to ensure they are all within a few milliseconds of each other (assuming your network latency to the NTP server you picked is reasonable). Test it with ping if you are unsure.

Step 3

In this step your goal is to calculate the offset and the round trip delay. A typical NTP client regularly polls one or more NTP servers. The client must compute its time offset and round-trip delay.

Time offset θ is the positive or negative (client time > server time) difference in absolute time between the two clocks. It is defined as:

 
Where:

t0 is the client's timestamp of the request packet transmission
t1 is the server's timestamp of the request packet reception
t2 is the server's timestamp of the response packet transmission and
t3 is the client's timestamp of the response packet reception
The round-trip delay delta is calculated as:

Step 4

In this step your goal is to set the system clock based on the NTP calculated time. You’ll need to dig in to how to set the system time for your operating system from your programming language.

You can then adjust the local clock time in a loop until the offset is reduced to zero (or below some acceptable threshold, i.e. +/- 0.5ms).

When you’re confident you have it right you can test by:

Set your system clock to an hour earlier than it is (you might need to disable the operating system’s automatic use of NTP in order to do this.
Set your system time to an incorrect time.
Run your code to set the time.
Check that the time has updated to the correct time.
Don’t forget to re-enable the automatic use of NTP by your OS.

Once that’s done - congratulations you’ve built an NTP Client and seen how it can set your system time and how your OS uses an NTP client to keep the system time and date correct.
