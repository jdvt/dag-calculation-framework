# Calculation frameworks 

Numerical calculations can be defined in a graphical formats. Here graphical networks (networkx and pygraphviz) are used to store variables and functions on nodes and edges respectively. Calculations are then completed by collapsing each Directed Acyclic Graph (DAG)

## Background 

When defining a calculation there is often a technical specification. This states inputs and outputs in terms of their mathematical context. Each variable can be defined further as to set it belongs to (for example real numbers) (not shown is image) and its relationship with additional variables.

<center>
<img src="https://github.com/jdvt/dag-calculation-framework/blob/master/readme_images/technical_specification.png" height="120">
</center>

A calculation is completed using a computational tool. Loosely this is any framework that allows inputs and outputs joined through a chained mathematics in an automated fashion

This framework could be code / a programming language: 

<center>
<img src="https://github.com/jdvt/dag-calculation-framework/blob/master/readme_images/code_implementation.png" height="150">
</center>

Or by means of some graphical user interface that allows the appropriate inputs, formula, and outputs to be created, for example Excel (and of course other tools exist!): 

<img src="https://github.com/jdvt/dag-calculation-framework/blob/master/readme_images/excel_implementation.png" align="middle" height="150">

Finally I propose that mixing the two to implement a calculation as a graphical network (below) has significant benefits -- these are described below. An output from one possible directed acyclic graph is shown below: 

<img src="https://github.com/jdvt/dag-calculation-framework/blob/master/readme_images/graphical_network_implementation.png" height="180" align="middle">

# Calculation frameworks as Directed Acyclic Graphs

Using Directed Acyclic Graphs as a calculation framework has the following advantages:

**Feature: Calculations are self documenting -- a calculation diagram is readily created**

* Calculations can be easily understood 
* Documentation is simple and easy to understand  
* New documentation can be easily created as calculations change 
* Documentation can be shared separately from code 

**Feature: Calculations themselves are defined in code** 

* Version control is possible 
* Each variable can be easily changed to allow for various types of analysis (for example sensitivity analysis)
* Calculations can be tested to show repeatibility  

**However, the following challenges are not solved using this calculation framework:**
* In this framework users must be able to understand this programming language (python) prior to implimenting calculations
* (currently) Complex calculations are difficult to input. In the simplist of cases each node must be connected only with simple mathematical opperators. For further work on more complex implimentations see the ```work_in_progress``` folder. 

# Implementation 

Graphical networks are defined in pygraphviz. Pygraphviz allow for attributes to be easily applied to nodes and edges. Pygraphviz also allows more options when creating network diagrams. In this implimentation plotting functionality is independent of calculation functionality. Once complete, a dot-file is output and passed to networkx

Calculations are completed in networkx. Networkx has many more functions for dealing with graphical data structures and specifically directed acyclic graphs (DAGs)

Use ```linear_example/dag_calculation_linear.py```. Inputs are defined as the attributes on nodes and edges respectively (```values``` and ```math```). In networkx these attributes are converted to dictionaries for use in calculation. Keys are sorted in order to process the DAG from input to final output. A recursive function (```recursive_collapse.py```) is used to process the values against each operator until each value in the graph has been updated with those above it. 