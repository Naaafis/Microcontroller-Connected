# timer_group_example_main.c

Added flag variable to existing timer_event_t struct in timer_group example code

interupt_handler for timer sets evt.flag to 1

GPIO ISR handler sets start flag to 1 to initialize count

GPIO button task just initializes counter

timer task receives timerqueue and it receives either a zero for evt.flag if a second had not passed or 1 if timer interupt handler is called, which it will be every second

counter is incremented on the basis of is evt.flag is 1 meaning counter increments every second using timer interupts

counter is then used to display time to i2c display

if counter reaches the start value it is reset to 1
