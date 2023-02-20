# Reliable, Scalable, and Maintainable Applications

> we will start by exploring the fundamentals of what we are trying to
> achieve:  reliable,  scalable,  and  maintainable  data  systems.  We’ll  clarify  what  those
> things mean, outline some ways of thinking about them, and go over the basics that
> we  will  need  for  later  chapters.

**Data-intensive applications: bigger problems are usually the amount of data, the complexity of data, and the speed at which it is changing.**

Many applications need to:

* Store data so that they, or another application, can find it again later (***Database***)
* Remember the result of an expensive operation, to speed up reads (***Caches***)
* Allow users to search data by keyword or filter it in various ways (S***earch Indexes***)
* Send a message to another process, to be handled asynchronously (***Stream Processing***)
* Periodically crunch a large amount of accumulated data (***Batch Processing***)

Three concerns that are important in most software systems:

***Reliability***

    The system should continue to work correctly even in the face of adversity (hardware or software faults, and even human error).

***Scalability***

    As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth.

***Maintainability***

    Over time, many different people will work on the system, and they should all be able to work on it productively

---

## Reliability

**Function, Performance, Security**

When  we talk about "fault-tolerant" of system, there is some limitations, we can't handle every possible kind of fault. So it only makes sense to talk about tolerating **certain types** of faults.
