---
title: "Coding Questions 1"
date: 2022-09-01T20:59:27-04:00
draft: false
---

The following questions are taken from {{< link "https://www.geeksforgeeks.org/qualcomm-interview-experience-on-campus-2022/" "Qualcomm Interview Experience 2022" >}}

## Question 1

{{< admonition question "Question 1" true >}}
A friend of Alex has gifted them a movie collection, and Alex is excited to watch them all as quickly as possible. The duration of the movies is given in array durations[n], where n is the number of movies, and each movie duration lies between 1.01 and 3.00 units of time (up to two decimal places). Every day, Alex wants to spend no more than 3.00 units of time watching the movies but also wants to complete the movies in the least number of days possible. Alex does not leave a movie in between. That is, if Alex has picked up a movie, Alex watches the complete movie on the same day. Find the minimum number of days needed to watch all the movies. 
{{< /admonition >}}

{{< admonition example "Example" true >}}
Input:

- n = 5
- duarations = [1.90, 1.04, 1.25, 2.5, 1.75]

Output: 3

Explanation:

- day 1 Alex watches [2.5]
- day 2 Alex watches [1.90, 1.04]
- day 3 Alex watches [1.75, 1.25]

{{< /admonition >}}

The trick to solving this question is to realize that Alex can watch at most 2 movies per day :astonished:.

Steps to solve:
1. Sort the array of movies.
2. Make pointers at both ends of the array
3. If sum of movies at pointers are are less than or equal to 3, move both pointers inward
4. Else, move only the pointer closer to the end inward



```python
def min_days_to_watch(arr):
  days = 0
  start_pointer = 0
  end_pointer = len(arr)-1
  arr.sort()
  
  while start_pointer <= end_pointer:
    if arr[start_pointer]+arr[end_pointer] <= 3.0:  
      start_pointer += 1
      end_pointer -= 1
    else:
      end_pointer -= 1
    days += 1
  
  return days

arr = [1.90, 1.04, 1.25, 1.75, 1.1, 1.99, 1.01 ]
min_days_to_watch(arr)
```

## Question 2

{{< admonition question "Question 2" true >}}

Given two positive integers n and k, perform a circular shift on the binary representation of n by k positions.

{{< /admonition >}}

{{< admonition example "Example" true >}}
Input:

- n = 13
- k = 1

Output: 11

Explanation:

- 13 in binary is 1101
- Circualar shift 1101 to the left by 1 results in 1011 = 11

{{< /admonition >}}



k := k%4

a := n << k

b := n >> (4-k)

answer := (a | b) & 15 


```cpp
int circularShift(unsigned int n, unsigned int k)
{
  unsigned int BIT_LENGTH = 4;
  k %= BIT_LENGTH;
  unsigned int mask = 15;
  return ((n << k) | (n >> (BIT_LENGTH - k))) & mask;
}
```

## Question 3 

{{< admonition question "Question 1" true >}}
Complete the function allocateMemory() in the below code in C language. 

```c
int main() {
int *ptr = NULL;
allocateMemory();
*ptr = 5;
printf(“%d”, *ptr);
return 0;
}
```
{{< /admonition >}}

The answer is 
```c
ptr = (int*) malloc(sizeof(int));
```

## Question 4

> What is mutex?

A mutex is a lock that we set before using a shared resource and release after using it. When the lock is set, no other thread can access the locked region of code.

## Question 5

> Difference between mutex and semaphores.

A mutex is similar to a binary semaphore. A key difference between the two is that the process that locks the mutex (sets the value to 0) must be the one to unlock it (sets the value to 1). This does not have to be the case for binary semaphores.

## Question 6

> How do deadlocks occur and how do prevent deadlocks?

Deadlocks occur when two or more processes are unable to proceed because each is waiting for one of the others to do something.

Deadlocks can be prevented by adopting a policy that eleminates on of the following coditions:
- Mutual exclusion
- No preemption
- Hold and wait
- Circular wait

For example the hold-and-wait condition can be prevented by requiring that a process request all of its required resources at one time and blocking the process until all requests can be granted simultaneously. 

The circular wait condition can be prevented by defining a linear ordering of resource types. If a process has been allocated resources of type R, then it may subsequently request only those resources of types following R in the ordering.

## Question 7

> What is virtual memory and how it is achieved?

A storage allocation scheme in which secondary memory can be addressed as though it were part of main memory. The addresses a program may use to reference memory are distinguished from the addresses the memory system uses to identify physical storage sites, and program-generated addresses are translated automati- cally to the corresponding machine addresses. The size of virtual storage is limited by the addressing scheme of the computer system, and by the amount of secondary memory available and not by the actual number of main storage locations.

## Question 8

> What is the advantage of using thread over process?

The key benefits of threads derive from the performance implications:

1. It takes far less time to create a new thread in an existing process,than to create a brand-new process. Studies done by the Mach developers show that thread creation is ten times faster than process creation in UNIX [TEVA87].
2. It takes less time to terminate a thread than a process.
3. It takes less time to switch between two threads within the same process than to switch between processes.
4. Threads enhance efficiency in communication between different executing programs. In most operating systems, communication between independent processes requires the intervention of the kernel to provide protection and the mechanisms needed for communication. However, because threads within the same process share memory and files, they can communicate with each other without invoking the kernel.

Thus, if there is an application or function that should be implemented as a set of related units of execution, it is far more efficient to do so as a collection of threads, rather than a collection of separate processes.

## Referances

{{< admonition note "Referance" true >}}

- Stallings, William. Operating Systems: Internals and Design Principles. Ninth edition, Global edition, Pearson, 2018.

{{< /admonition >}}