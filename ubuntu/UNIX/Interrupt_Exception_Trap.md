
There are interrupts - things that cause the CPU to start executing code from a table (ae.g. n interrupt vector table).

Interrupts can be split into categories depending on what triggered them:

exceptions - triggered by the CPU itself
IRQs - triggered by external hardware (e.g. network card)
software interrupts - triggered explicitly by the code that was running
IPIs (inter-processor interrupts) - triggered by a different CPU

Exceptions can be further broken down into sub-categories:

aborts - things that prevent the interrupted code from continuing. These are things that indicate a major problem - e.g. division by zero, hardware failures, etc.
traps - things that don't prevent the interrupted code from continuing. These can be used for debugging, for virtual memory management, etc.
Mostly; the difference between a trap and an exception is like the difference between a car and a vehicle (a trap is one kind of exception, and a car is one type of vehicle; but there are exceptions that aren't traps and there are vehicles that aren't cars).