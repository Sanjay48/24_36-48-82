24_36-48-85
===========

//CASE Tools Lab

                                          PRODUCER -CONSUMER PROBLEM

The producer-consumer problem illustrates the need for synchronization in systems where many processes share a resource. In the problem, two processes share a fixed-size buffer. One process produces information and puts it in the buffer, while the other process consumes information from the buffer. These processes do not take turns accessing the buffer, they both work concurrently. Herein lies the problem. What happens if the producer tries to put an item into a full buffer? What happens if the consumer tries to take an item from an empty buffer?

PRODUCER:
(1) The producer must first create a new widget. (2) Then, it checks to see if the buffer is full. If it is, the producer will put itself to sleep until the consumer wakes it up. A "wakeup" will come if the consumer finds the buffer empty.(3) Next, the producer puts the new widget in the buffer. If the producer goes to sleep in step (2), it will not wake up until the buffer is empty, so the buffer will never overflow. (4) Then, the producer checks to see if the buffer is empty. If it is, the producer assumes that the consumer is sleeping, an so it will wake the consumer. Keep in mind that between any of these steps, an interrupt might occur, allowing the consumer to run.

CONSUMER:
(1) The consumer checks to see if the buffer is empty. If so, the consumer will put itself to sleep until the producer wakes it up. A "wakeup" will occur if the producer finds the buffer empty after it puts an item into the buffer. (2) Then, the consumer will remove a widget from the buffer. The consumer will never try to remove a widget from an empty buffer because it will not wake up until the buffer is full.(3) If the buffer was full before it removed the widget, the consumer will wake the producer. (4) Finally, the consumer will consume the widget. As was the case with the producer, an interrupt could occur between any of these steps, allowing the producer to run.//


#include<stdio.h>
#define BUFFER_SIZE 3

int buffer[BUFFER_SIZE],item;
int fillCount = 0; // items produced
int emptyCount = BUFFER_SIZE; // remaining space
producer() {
while (1) {
item = produceItem();
if(item==0)
return;
if(emptyCount==0)
{printf("\nbuffer full");
break;
}
emptyCount--;
buffer[emptyCount]=item;
printf("\n %d put into the buffer..",item);
fillCount++;
}
}
consumer() {
while (1) {
if(fillCount==0)
{printf("\nbuffer empty");
break;
}
fillCount--;
item=buffer[emptyCount];
printf("\n %d removed from buffer..",item);
emptyCount++;
printf("\n %d consumed..",item);
}
} int produceItem()
{ int n;
printf("\n Enter the number for production (0 to stop)..\n");
scanf("%d",&n);
return n;
} int main()
{ char i;
while(i!='y' && i!='Y')
{ 
             producer();

consumer();
printf("\nDo you want to exit...(Y or N)....");
scanf("%c",&i);
} return 1;
}


