# STAGE
State-based Test Suites Generation and Execution Tool Chain
# Description
STAGE is an automation tool chain. The first tool in the tool chain (STAGE-1) generates test trees from a finite state machine (FSM) diagram, extracts test cases from the generated trees, and composes a test suite from each generated tree. This tool is the first to generate all possible distinctive trees using Depth and Breadth First graph traversal algorithms. The tool generates random test suites as well as a complete round-trip test suite of the supplied FSM diagram. The tool chain should be of interest to researchers in state-based testing as well as practitioners who are interested in alternative adequate test suites especially for comparing the effectiveness of the different test suites satisfying one criterion and the effectiveness of the other different criteria.
The second tool (STAGE-2) automatically executes one or more generated test suites on the code of the SUT. It also encloses a test oracle that is responsible for checking whether the SUT conforms with the specification provided by the input FSM, or not. STAGE-2 also can run in an alternative mode to generate JUnit tests instead of directly executing the test suites. This is useful, as the JUnit tests may be used by other tools to run the test suites.
# Getting Started
To get started, you need to get a copy of stage and Major[1] on your local machine 
A.	STAGE
To get a copy of the project:
1.	Download the source code.
2.	Compile the project
B.	Major
All the information needed to install and use the tool are available on the website.
http://mutation-testing.org/
Prerequisites

# Installing

# Running
The step below that are needed to go through the whole process for generating, executing and measuring the effectiveness of the test suites.
1.	An FSM diagram representing the experimental object is created using the Graph Description Language (DOT). It can be visualized using Graphviz [2]. The file that models the experimental object is then fed to STAGE-1, and a traversal technique is chosen (Breadth, Depth, Round-trip, or Random).



2.	STAGE-1 generates all the traversal trees of the FSM diagram. From each generated tree, STAGE-1 produces one test suite that is composed of all tree paths from the root node to a leaf node (test sequences).
3.	The researcher/test engineer adds parameters when needed for each test suite. Figure 2 shows a sample of how the parametrized test suite looks like. Each line corresponds to one test case (tree path). For example, in test case 0 of Figure 2 PF5 is a state name, while 37 is a transition number that maps to a method that takes an integer parameter. The test engineer in this case specified the parameter value to be 6.
4.	The parametrized test suites as well as the experimental object code are fed to STAGE-2, and the mode that exercises the test suites on the experimental object code is chosen for this step. There are few details in this step that have been omitted from Figure 1 for simplicity. They are:
a.	An experimental object class inherits from a provided abstract java class that has the get state functions, and each experimental object implementation implements this function. This is to guarantee that the test oracle can use the getters to check the current state of the object.
b.	When an experimental object is implemented, or the code is supplied to STAGE-1, one has to make sure that the code has some error handling mechanism in order not to crash when the mutants are seeded. For instance, each small block of statements can be surrounded by try and catch so that the SUT can be resilient enough to survive the mutants inserted by Major without crashing. 
c.	In addition to the test suites and the code, STAGE-2 needs a way to map the transition numbers to actual functions. Therefore, it accepts a transition to function map file as the one shown in Figure 14. The file also specifies the type of arguments for each transition/method as shown by the provided format. Parameters are separated from functions by a ‘-‘, while spaces are used as a separators between the different parameters of the same function. Since STAEG-2 supports arrays as parameters, two square brackets “[ ]” are used to indicate that the parameter is an array.
5.	STAGE-2 runs using the inputs listed in the previous steps (test suites and transition to function map) and it produces log files. If the log file is empty, this means all test cases passed and the experimental object code is error free. Otherwise, each reported failure in any experimental object should be resolved before moving to the following step.
6.	The parametrized test suites are fed again to STAGE-2, but this time to produce all JUnit files.
7.	STAGE-2 produces all the JUnit files, where each JUnit file maps to one test suite.
8.	The experimental object code is fed to the first step of Major.
9.	Major produces the faulty version of the experimental object code files. It also provides a log file that specifies the seeded mutants and their locations in the code. 
10.	 The faulty version of the code (from step ‎9), the mutation log file (from step‎9), and the JUnit files (from step ‎7) are the inputs to the second step of Major. 
Finally, Major runs the experimental objects and based on assertion failures (in the JUnit tests) produces a report indicating which mutants have been killed and which mutants have been covered

# Built with
# Authors
Hoda Khalil
Yvan Labiche
# Acknowledgements
We would like to thank René Just for answering all our questions related to Major.
# Bibliography 
[1]	R. Just, “The Major Mutation Framework,” no. April, pp. 1–21, 2014.
[2]	“Graphviz.” [Online]. Available: http://www.graphviz.org/.

