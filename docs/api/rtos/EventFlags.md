## EventFlags

<span class="images">![](http://os-doc-builder.test.mbed.com/docs/development/mbed-os-api-doxy/classrtos_1_1_event_flags.png)<span>EventFlags class hierarchy</span></span>

The EventFlags class provides a mechanism for setting and waiting for specific conditions. It provides a generic way of notifying other threads about conditions or events. You can think of each instance of the EventFlags class as an event channel. There are 31 different flags available for each event.

### EventFlag class reference

[![View code](https://www.mbed.com/embed/?type=library)](http://os-doc-builder.test.mbed.com/docs/development/mbed-os-api-doxy/classrtos_1_1_event_flags.html)

### EventFlags example

Below is an example of EventFlags usage, where one thread is generating events every 1s, and the second thread is waiting for the events and executing some action.

<span class="images">![](https://s3-us-west-2.amazonaws.com/mbed-os-docs-images//eventflags_usage.png)</span>

```
#include "mbed.h"

EventFlags event;

void worker_f()
{
    while (true) {
        event.wait_all(0x1);

        printf("Got signal!\r\n");
    }
}

int main()
{
    Thread worker;

    worker.start(callback(worker_f));

    while (true) {
        wait(1);
        event.set(0x1);
    }
}
```
