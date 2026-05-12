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

## why the total number of queue is as such
the total number depends on how many times we ran the publisher, so if we were to ran it twice quickly, tjats 10 events queued up at once. the number we are seeing is just however many event were sitting in rabbitmq waiting to be processed at that moment before the subscriber caught up

## why the queue spike reduced quicker with multiple subscriber
when there was only 1 subscriber (it was slow with 1 second delay) all 5+ messages has to be processed one by one by that single subscriber. so the queue drained slowly. with 2 or even more subscibers running at the same time, the messages get split between them. one subscriber takes some messages, the other takes the rest, and they process in parallel, this means the queue empties rougly n times as fast

## what can be improved in the code
looking at the code it always send the same 5 hard coded users every run, in real world implementation it would preferably if we send dynamic data, not hardcoded names. also the publisher has no way to know if messages were actually received, theres no acknowledgement or confirmation back from the subscriber. in production we'd want some form of feedback or logging to confirm directory