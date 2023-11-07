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

### Outline of Algorithm

Depending on the control location, we can expect the minimum and maximum speed (km/hour) to change as a result of this distance. Refer to the table here [https://rusa.org/pages/acp-brevet-control-times-calculator](https://rusa.org/pages/acp-brevet-control-times-calculator).

The open time is calculate by dividing control distance by the maximum speed. The algorithm can be generalized as (control distance - (previous interval)) / (current maximum speed) + (last intervals control distance - previous interval) / (last intervals maximum speed) + ...

Similarly the close time is calculated by dividing control distance by the minimum speed. The algorithm can be generalized as (control distance - (previous interval)) / (current minimum speed) + (last intervals control distance - previous interval) / (last intervals minimum speed) + ... Except for when control distance is equal to brevet distance which both are equal to 200. This special rule dictates that our close time is 13H30. 

## Running the Program

There are two ways to run the program. 

#### Docker 

Inside of your terminal, navigate to the folder called "brevets", then type in the command "docker build -t brevets ." the period indicates the current directory. Feel free to build docker from wherever but make sure the end of the command is the correct path to the Dockerfile After the image is done being built, run the container by executing the command "docker run -p 5000X:5000 brevets" where X is the port number you have indicated in your credentials file. Once the container is running you can run the application by searching http://localhost:500X on your browser.

#### Python 
Inside your code editor, navigate to the folder called "brevets", then run flask_brevets.py. You can run the program on a browser by typing in http://localhost:500X where X is the port number you have indicated in your credentials file. 

## Authors

Michal Young, Ram Durairajan. Updated by Ali Hassani.
