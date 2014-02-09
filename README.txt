DistAlgo implementation of Ricart Agarwala's Timestamp and Token Based Algorithms
Date: 9/6/2013
by Madhurima Roy
-----------------------------------------------------------------------------------------------------------------------
GENERAL USAGE NOTES
--------------------

- How to run:
python -m distalgo.compiler examples/main.da
python -m distalgo.runtime  examples/main.da processes requests times step

- default values:
processes: 5
requests: 5
times: 1
step: 1

- The code has been developed and tested in python 3.3.2 on Linux

- It is observed that when large number of processes and requests are given,
  the difference in the performance of clear version and that of the efficent
version is more.
-------------------------------------------------------------------------------------------------------------------------
SUMMARY
---------
Basic approach of the code:

I am using DistAlgo module in python to demonstrate
	Ricart Agrawala's Timestamp based algorithm clear version
	Ricart Agrawala's Timestamp based algorithm efficient version	
	Ricart Agrawala's Token based algorithm clear version
	Ricart Agrawala's Token based algorithm efficient version	

I am measuring the runtimes for each algorithm to summarize the statistics in the end of the run
Finally we are printing these statistics together in a tabular format

I am running each of the above algorithms one by one. A main driver process is responsible for running a set of child processes which would run the same algorithm simultaneously and they would communicate via message passing only.
It is to show that in the above algorithms it is possible to implement a critical section in a distributed system environment.

Each process takes the number of requests supplied into its quota and exits systematically as soon as it finishes executing all the requests that was assigned to it.
Currently the number of requests are supplied per process using the request argument to the DistAlgo script.
Each process needs to keep a track of the other processes to make sure that it exits the distributed system along with the other threads to prevent a possible deadlock among other threads

In the efficient versions of the above algorithms I am trying to optimize the code by using 
	- counts instead of whole lists
	- using for loops and breaking midway to prevent unneccessary iteration through the loops
	- removing certain set queries and list comprehensions and replacing with ifs and loops to reduce the performance load

---------------------------------------------------------------------------------------------------------------------------
OUTPUT (Example):
-----------------
Statistics: processes: 5, requests: 5, times: 3, step: 3

1. Ricart Agrawala Timestamp based algorithm

  Requests |        Clear version |    Efficient version
-----------+----------------------+----------------------
         5 |                27.79 |                23.93
         8 |                40.28 |                26.40
        11 |                49.28 |                23.29

2. Ricart Agrawala Token based algorithm

  Requests |        Clear version |    Efficient version
-----------+----------------------+----------------------
         5 |                24.78 |                22.44
         8 |                29.20 |                28.96
        11 |                26.29 |                27.74
------------------------------------------------------------------------------------------------------------------------------
