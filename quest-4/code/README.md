# Code Readme

## udp_multicast_example_main.c
//Previous implementation of leader Election:
## udp_multicast_ex_main.c

This is adopted code from the UDP multicast example.

We added in code for a timer interrupt that is sending flags every 1 second to indicate that we should reduce timeout values.

We use the onboard LED to indicate who is the leader at the time by checking myState in a while loop, and if the state becomes LEADER, we change the light.

Every ESP has 3 states, and it starts off in the ELECTION state.
Each ESP is assigned an ID and during broadcasts, the ESP sends its ID along with the ID of the max known FOB, and what kind of message it is sending.

The timer event task only works once every second.
  It starts off by decrementing the current timeout time, which can either be time until an election start or until one ends
  An election starts if a Leader heartbeat is not heard in the allocated seconds and the FOB was in follower state
  An election ends if the FOB does not hear any responses from any other FOBs during the election state, meaning it has the highest ID

  There is also a heartbeat time consistently being processes in this task, and this is only used by Leaders to send heartbeats when this timer reaches 0.

  At the start or end of an election, the MAXval is assigned the ID of the current fob. If this fob is the one to end an election, it has the highest ID in the system.

The process messages task rely on the receiving buffer being of length greater than 0. This is because we are using UDP multicast to send data, and we are always sending data weather we need to or not, so we send empty strings unless an actual message is needed.
  StrTok is used to break up actual messages and place those values such as what kind of message and the sended ID and senders known max value into the respective variables.
  If we receive messages from anyone but our selves, then we handle it by setting flags for what kind of message it is.

    If its a heartbeat and im not a leader, I just reset my leader timeout because the leader is active

    If its a response and im in an election, then I'm now aware that there are higherID fobs present and I reset my election timeout to allow time for that FOB to get the leader position.

    If its an election message, I start an election no matter what because there is a conflict with the leader somewhere.

    If its a victory message and the sender has a higher ID than me, I accept them as the leader.

    Along these response messages, I also update my maxVal if a response makes me aware of higher IDs.

Our UDP multicast implementation is mostly borrowed code and it just sends actual data if a send flag goes up because of response messages.

//New additions
We have additional initializations for code borrowed from our IR task. We now have onboard LEDs toggle on in response to votes or in response to button presses. We have a button to also send the current state of the lights as well as own ID to be casted as a vote.

We have flags to account for when a fob receives a vote and when a leader is made aware of that vote. We send additional messages tagged along with the broadcast message to account for vote, voter, weather it is to be processed by the leader and finally, weather it is coming from the leader an is to be processed by the node. Our immage and caption should clear this up a bit.

## final.js
This code deals with handling the node server.
Lines 1 - 21 deal with all of the initializations needed. Some important aspects are declaring the multicast address for the server to also be able to listen and receive these messages from UDP Multicast, as well as creating/opening the underlying LevelDB store.

Lines 31-61 deal with receiving a message from the socket, converting this message into a string so it is able to be parsed for its proper values, and putting these proper values into the database with the key being the number of the vote, and the value containing the voterID as well as the color that the specific voter voted for.

Lines 69 - 72 serve the webpage using indexx.html (2 x's)

Lines 75 - 93 include the readDB function which streams the database and emits all of these key-value pairs over to the web-client so it will be able to receive, query, and chart these values.

Lines 96- 107 handle a user connecting to the web-client and further streaming the database on this connection.

Lines 144-146 allow us to listen on port 3000 of 'localhost'.

Lines 149 - 153 contain some of the most important capabalities of the file as it connects the node server to the Multicast address so that we can receive messages from the leader.

## indexx.html

This is the client side of the web-interface.

Lines 34-55 include the chart that will hold the respective votes for each 'color' in the election running.

Lines 69 - 93 handle receiving the message over the socket that holds the respective key-value pair values. It then accesses these respective values and increments the chart's values for each vote it receives, either for 'G' or 'Y'.

## Attribution

final.js and indexx.html are heavily adapted from the class documentation.

Please describe what is in your code folder and subfolders. Make it
easy for us to navigate this space.

Also
- Please provide your name and date in any code submitted
- Indicate attributrion for any code you have adopted from elsewhere
