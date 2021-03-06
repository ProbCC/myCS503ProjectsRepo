# Lab1 PSO materials
Index
1. handout go through
1. process context switch
1. readylist and queue
1. timer interrupt


</br>
</br>

------------------------------------------
</br>

### 1. Handout go through
1. Aging Scheduler [20pt]
1. Proportional Share Scheduler [50pt]
1. Multilevel Feedback Queueu Scheduler [70pt]
1. Process owernership [20pt]

[lab1 handout](https://www.cs.purdue.edu/homes/pfonseca/teaching/cs503/21spring/labs/lab1.html)


reminder: 
1. Do **NOT** *define/initilize* new function or variables in `main.c`. i.e. you can *define/initilize* in the begining of *initilzed.c*, and *declare* in *prototype.h*.
1. Recommanded using `XDEBUG_KPRINTF` for your own debug print purpose.

</br>
</br>

-----------------------------------------

</br>

### 2. Context-Switch and `resched()`


![processes ctxsw example](https://raw.githubusercontent.com/ProbShin/myCS503ProjectsRepo/main/PSO/lab1/img1.png)

</br>
</br>

-----------------------------------------

</br>

### 3. Readylist

XINU store all the `PR_READY` processes in a prority-queue data structure called **readylist**. It utlizes XINU's queue system. 
You need to implement your own operation on this data structure. i.e. `traverse`, `insert`, `remove`.

```
# An example of double linked list, (Note, this is not XINU used)
struct node {
  int    val;
  struct node*  prev;
  struct node*  next
}
```

```
# priority-queue operation demo
Head <-> 30 <-> 20 <-> 20 <-> 10 <-> Tail 
         |      |       |      |
         p1     p2      p3     p4
        

Demo: insert 40 (p5); insert 5 (p6); insert 20 (p7);

Head <-> 40 <-> 30 <-> 20 <-> 20 <-> 20 <-> 10 <-> 5 <-> Tail 
          |     |     |      |      |     |     |
         p5    p1     p2     p3     p7    p4    p6
```


The XINU's readylist related implementations.
* data structure and marco functions in *queue.h*
* `insert` in *insert.c*
* `dequeue` in *queue.c*


</br>
</br>

-----------------------------------------

</br>

### 4. Queue
XINU's queue system. Preassigned space for a **Head** and a **Tail** for per queue using table to implement double-linked-list.
* `dequeue`, `enqueue` in *queue.c*
* data structure and marco functions in *queue.h*
* assigned space in *initialize.c*

```
# each row of the table served as an node.
# each process assigned a node.
# each queue assigned two nodes (Head, tail)

      
rowNo.|    Key    | nxt | pre |
      |-----------------------|
              ...
      |   ...     |     |     |
      |-----------------------|
  4   |   10      |  q  |  5  |
      |-----------------------|
  5   |   20      | q+1 |  4  |
      |-----------------------|
      |           |     |     |
      |-----------------------|
      |           |     |     |
      |-----------------------|
  q   |    Head   | nxt | pre |    \
      |-----------------------|     |-> readylist
 q+1  |    Tail   | nxt | pre |    /
      |-----------------------|
      |           |     |     |
       ...
```

This example shows that there are only two process P4 and P5 which have preority 10 and 20 in the *readylist*.



</br>
</br>
** Traverse **
```
# pseudo code, not the real code.
For i = Head_of_readylist.qnext; i!=Tail_of_readylist; i = queuetab[i].qnext :
    print "process with pid = %d "%(i)
```

</br>
</br>


<!--
------------------------------------------------

</br>

### 4.1 Double-linked-list
basic operations of double-linked-list.
* `travers`
* `insert`
* `remove`

</br>
</br>

-->
-----------------------------------------

</br>

### 5. Timer Interrupt 
* clkhandler.c
* clkinit.c
* clkdisp.S

`clkhandler()` by default would be triggered per 1ms. It would call `resched()` to "context-switch" procesess depend on the `QUTANTUM`.

</br>
</br>



