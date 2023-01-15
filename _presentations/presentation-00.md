
---
title: "Static Analysis for Tensor Flow Machine Learning Programs; Paper entitled:Ariadne: Analysis for Machine Learning Programs"
collection: presentations
permalink: /presentations/presentation-00
excerpt: 'The authors apply static analysis to machine learning code that uses Tensorflow.'
date: 2022-02-03
venue: ' '

---

<iframe src="https://unigeit-my.sharepoint.com/personal/s4930082_studenti_unige_it/_layouts/15/Doc.aspx?sourcedoc={a9088d55-616c-4c79-8759-4a8955a83346}&amp;action=embedview&amp;wdAr=1.7777777777777777" width="900px" height="544px" frameborder="0">This is an embedded <a target="_blank" href="https://office.com">Microsoft Office</a> presentation, powered by <a target="_blank" href="https://office.com/webapps">Office</a>.</iframe>

-----------------------------------------------

In this paper, The Authors apply static analysis to machine learning code that uses Tensorflow.

-Firstly, we introduce the problem and some definitions. Then review related works. After that I explain the propose method and finally discuss the results.


<br/><img src='/images/PaperAr0.jpg'>
----------------------------------------------
-In most programming domains, preventing and catching programming errors is aided by supportive tooling. Tools also aid programming by suggesting appropriate completions while writing code, and refactoring code to improve design and reuse. These tools usually are part of IDEs. Machine learning code is commonly written in Python, partly because of its wealth of machine learning libraries. Due to ML's statistical nature, code with subtle errors may run and produce results that look plausible but are meaningless.

They have created a static analysis tool for Python, a type system for tracking tensors—Tensorflow's core data structures—and a data flow analysis to track their usage.

-Static Analysis: static analysis is the analysis of computer programs performed without executing them, in contrast with dynamic analysis, which is performed on programs during their execution.


<br/><img src='/images/PaperAr1.jpg'>
----------------------------------------------
-Python & ML: Machine learning is increasingly used in science from translation to vision. Python is a popular language because of its wealth of machine learning libraries, and it makes development faster; however, this language has less support for error detection at code creation time than tools like Eclipse.


<br/><img src='/images/PaperAr2.jpg'>
----------------------------------------------
-Challenges: Machine learning code generally uses all the standard features of programming languages, such as classes and methods; hence, program analysis must handle them. Three necessary aspects are: Call graph construction, Pointer analysis, and Library modelling. 

•	Call graph construction is required to understand the direct and indirect function calls. A direct call could be handled easily, but more complex cases require higher-order functions. 

•	Pointer analysis is needed, for example, to know the loading of the images correctly. It requires pointer analysis to understand that the objects at two points might be aliased. 

•	In Library modelling, sometimes there is no connection in the source code being analyzed, and the TensorFlow source is not typically available when analyzing a program. However, there is an indirect connection between them through the library. These challenges are all connected. Fortunately, these challenges are similar to what analysis frameworks have long had to do for other languages, and we can leverage that technology.

-Related works: There has been some Python program analysis work, and we will discuss the most related tools and summarize the rest of the work.
These works are two broad classes: code quality checkers and dynamic analysis. Code quality checkers are static analyzers for code quality metrics or tools. Examples are Pylint, Pycodestyle, Pyflakes, Flake8, QuantifiedCode CE, and Pydocstyle. Python Taint is a static analysis tool for detecting security vulnerabilities in Python. It uses standard dataflow techniques and can do some analysis. These tools are not for whole-program static analysis based on dataflow, as WALA is.

Dynamic analyses sometimes build call graphs, of which a notable example is "Python CallGraph". Another dynamic analysis tool, like PyChecker, do things one would expect a compiler to do for many other languages. These tools are very different from WALA, as our goal is to statically approximate all possible runs rather than dynamic tools focusing on one or a few executions.

There is also much exciting work in the area of using machine learning to analyze code. However, those work remains technically distinct in that it uses machine learning to analyze rather than applying code analysis to aid machine learning.

-WALA: Existing program analysis frameworks (like Doop, Safe, WALA) provide the program analysis that would enable analyzing programs; they can build call graphs describing how functions interact and analysis of how objects behave. However, none of these support Python. WALA supports Java and JavaScript. Fortunately, WALA does have a frontend designed to make adding new languages as easy as possible.

WALA has been public for several years and used by researchers for various works. It has been robust and scalable enough to support products.
The Authors have presented WALA's application to analyze tensors' behaviour in Tensorflow ML programs. This involved adapting WALA to Python, which they believe is the first application of traditional program analysis technology to Python.


<br/><img src='/images/PaperAr3.jpg'>
----------------------------------------------
-The authors extend WALA to support Python, build a type system for tracking tensors—one of machine learning's core data structures—and an analysis of tensor usage. Their contributions are:
 
 1. Application of WALA program analysis to Python
 
 2. Type system capturing semantic properties of tensors
 
 3. An open-source implementation


<br/><img src='/images/PaperAr4.jpg'>
----------------------------------------------
-Example: Here, we consider an example that uses well-known MNIST data to train image recognition. MNIST is a handwritten dataset of numbers. This program reads training data and classifies images using operations like Reshape, Conv2d and read_data_sets. 

-The reshape operation reshapes a tensor to the dimensions specified in its second argument. The reshape operation can transform dimensions, but the total size must be the same since it is accessing the same data. They hypothesize that operations such as this could be checked for correctness in terms of both dimensions and types of data and perhaps even generated automatically.

The conv2d method requires that the input tensor has four dimensions. It requires that the contents of the dimension be a number. Also, it requires that the middle two dimensions represent height and width.

-WALA provides a framework for handling new languages, the Common Abstract Syntax Tree (CAst) system. 
The supported way to handle new languages is to translate a language into CAst, and use the built-in support for translating CAst into WALA's Internal Representation (IR) for analysis; They use the existing Jython functionality to create Python Abstract Syntax Tree for translation to CAst. 

Some constructs are standard enough across languages that CAst provides a construct with translation to Internal Representation, like if, while, and goto. -For such constructs, simply creating the appropriate CAst construct suffices.

Some other constructs differ in detail. -After that, they choose to model popular machine learning frameworks to capture their semantic properties, using an XML representation of the IR.


<br/><img src='/images/PaperAr5.jpg'>
----------------------------------------------
-Analyzing Tensors: WALA produces a dataflow graph as part of pointer analysis and call graph construction. The dataflow graph summarizes the program's flow of objects and values; this graph is an abstraction of possible program behaviour. -Given a dataflow graph G, the authors defined a tensor estimate T(y) as the set of possible tensor types that tensors held by y may have. 

According to this definition, y can have all tensor values, such as input, assigning a value of x to y, or equal to the result of reshaping a tensor or other TensorFlow operators. It formulates and configures the program and structures in this way.


<br/><img src='/images/PaperAr6.jpg'>
----------------------------------------------
-Results: They evaluated their prototype implementation by analyzing 6 Tensorflow examples. Their analysis checks that the tensor argument is the right size to be transformed into the desired shape for the reshape operation. The conv2d operation performs a 2D convolution on images, requiring the images to be in a height, width, and channels format. Their analysis checks that the argument has that structure. conv3d is similar to conv2d, but for 3D images. placeholder is used for operations later applied to data;

They evaluate these six programs. These programs build and train convolutional neural networks to classify images. 
This Table shows the APIs analyzed in each program; for each API, their analysis verified that these programs used them correctly. The ✓ (check mark) notation in the Table denotes constructs that they found in the codes and were able to verify appropriately used;
The ✗ (multiplication sign) denotes that they verified that the program does not contain the construct.
They claim that the analysis of each program took just a few seconds on a typical laptop.

-Limitations:

•	This implementation is still preliminary.

•	Not evaluated on different ML programs and data.

•	It is not complete and comprehensive.

•	But it's a good starting point.

--> [Link to the Paper ](https://arxiv.org/pdf/1805.04058) <--

