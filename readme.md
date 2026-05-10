## How much data your publisher program will send to the message broker in one run?

the publisher sends 5 events in one run, one for each user: amir, budi, cica, dira, and emir. Each
event contains a user_id and a user_name


## The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?

it means the both the publisher and subscriber are connecting to the same message broker on the same machine.
this is how the communicate, the poublisher sens events to that broker, and the subscriber lsitens for events from that same broker. they bever talk to each other directly


