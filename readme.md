## How much data your publisher program will send to the message broker in one run?

the publisher sends 5 events in one run, one for each user: amir, budi, cica, dira, and emir. Each
event contains a user_id and a user_name


## The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?

it means the both the publisher and subscriber are connecting to the same message broker on the same machine.
this is how the communicate, the poublisher sens events to that broker, and the subscriber lsitens for events from that same broker. they bever talk to each other directly

## what happened in the subscirber and publisher
the publisher sent 5 events to rabbit mq. rabbitmq held them in a queue. the subscriber, which was already connected and listening picked them up one byu one and processed/printed each one.

the publisher and subscriber never talked to each other directly, rabbitmq was the middleman and thats the whole point of event driven architecture

## Monitoring chart
each spike = one time i ran the publisher, the publisher sent 5 events at once to rabbitmq, which caused a brief burst of activity (the spike) then immediately dropped back to 0 because the subscriber processed them all instantly and the publisher finished.   
