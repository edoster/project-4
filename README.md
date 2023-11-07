# UOCIS322 - Project 4 #

Evan Doster

edoster@uoregon.edu

Description: Learn how to write test cases and test your code, along with more JQuery.

## Outline of the Application

You will reimplement RUSA ACP controle time calculator with Flask and AJAX.
The calculations should populate the open and close time after pressing enter without refreshes!
Inside of the applciation, there should be rigourous nose tests that outline potential weaknesses in the algorithm. 

### ACP controle Algorithm

This project consists of a web application that is based on RUSA's online calculator. The algorithm for calculating controle times is described here [https://rusa.org/pages/acp-brevet-control-times-calculator](https://rusa.org/pages/acp-brevet-control-times-calculator). Additional background information is given here [https://rusa.org/pages/rulesForRiders](https://rusa.org/pages/rulesForRiders). The description is ambiguous, but the examples help. Part of finishing this project is clarifying anything that is not clear about the requirements, and documenting it clearly. 

We are essentially replacing the calculator here [https://rusa.org/octime_acp.html](https://rusa.org/octime_acp.html). We can also use that calculator to clarify requirements and develop test data. 

The outline of the algorithm is as follows:

Depending on the control location, we can expect the minimum and maximum speed (km/hour) to change as a result of this distance. Here si the table used to keep track of these values. 

Control location (km)	Minimum Speed (km/hr)	Maximum Speed (km/hr)
0 - 200		15	34
200 - 400	15	32
400 - 600	15	30
600 - 1000	11.428	28
1000 - 1300	13.333	26

The open time is calculate by dividing control distance by the maximum speed. The algorithm can be generalized as (control distance - (previous interval)) / (current maximum speed) + (last intervals control distance - previous interval) / (last intervals maximum speed) + ...

Similarly the close time is calculated by dividing control distance by the minimum speed. The algorithm can be generalized as (control distance - (previous interval)) / (current minimum speed) + (last intervals control distance - previous interval) / (last intervals minimum speed) + ... Except for when control distance is equal to brevet distance which both are equal to 200. This special rule dictates that our close time is 13H30. 

## Running the Program

There are two ways to run the program. 

#### Docker 

Inside of your terminal, navigate to the folder called "brevets", then type in the command "docker build -t brevets ." the period indicates the current directory. Feel free to build docker from wherever but make sure the end of the command is the correct path to the Dockerfile After the image is done being built, run the container by executing the command "docker run -p 5000X:5000 brevets" where X is the port number you have indicated in your credentials file. Once the container is running you can run the application by searching http://localhost:500X on your browser.

#### Python 
Inside your code editor, navigate to the folder called "brevets", then run flask_brevets.py. You can run the program on a browser by typing in http://localhost:500X where X is the port number you have indicated in your credentials file. 

## Tasks

* Implement the logic in `acp_times.py` based on the algorithm linked above.

* Create test cases using the original website, and write test suites for your project.
	* Based on what was discussed in the lecture, create test cases, try them in the original website, and check if your functions correctly calculate the times.
	* This will effectively replicate the calulator above.

* Edit the template and Flask app so that the required remaining arugments are passed along.
	* Currently the miles to kilometers (and some other basic stuff) is implemented with AJAX. 
	* The remainder is left to you.

* As always, revise the README file, and add your info to `Dockerfile`. These have points!
	* **NOTE:** This time, you should outline the application, the algorithm, and how to use start (docker instructions, web app instructions). **Make sure you're thorough, otherwise you may not get all the points.**

* As always, submit your `credentials.ini` through Canvas. It should contain your name and git repo URL.

### Testing

A suite of nose test cases is a requirement of this project. Design the test cases based on an interpretation of rules here [https://rusa.org/pages/acp-brevet-control-times-calculator](https://rusa.org/pages/acp-brevet-control-times-calculator). Be sure to test your test cases: You can use the current brevet time calculator [https://rusa.org/octime_acp.html](https://rusa.org/octime_acp.html) to check that your expected test outputs are correct. While checking these values once is a manual operation, re-running your test cases should be automated in the usual manner as a Nose test suite.

To make automated testing more practical, your open and close time calculations should be in a separate module. Because I want to be able to use my test suite as well as yours, I will require that module be named `acp_times.py` and contain the two functions I have included in the skeleton code (though revised, of course, to return correct results).

We should be able to run your test suite by changing to the `brevets` directory and typing `nosetests`. All tests should pass. You should have at least 5 test cases, and more importantly, your test cases should be chosen to distinguish between an implementation that correctly interprets the ACP rules and one that does not.

## Authors

Michal Young, Ram Durairajan. Updated by Ali Hassani.
