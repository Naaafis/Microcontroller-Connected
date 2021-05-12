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
