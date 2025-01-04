through 3 chapters

A @staticmethod decorator makes the method that follows it into a static method of class. Such a method does not have a self parameter, and therefore it is not implicitly passed a reference to an object instantiated from the class.

The Single Responsibility Principle states that a well-designed class should be _cohesive_, meaning that it ought to have only a single primary responsibility. A poorly designed class has too many responsibilities. A cohesive class with a clear responsibility is easy to use—there should be no doubt what its purpose is. A cohesive class is easy to maintain—all its methods and instance variables serve a single primary purpose.

##### Strings vs. enumeration types
Whenever there is a limited set of values, such as for the genre, an enumeration type is preferable to using a string type. With strings, we must worry about case-sensitive versus case-insensitive comparisons. If we have a typo or a misspelling in a string, the resulting runtime logic error may be hard to detect. Comparisons of enumeration constant values during run time are very efficient, and Python will catch a misspelling of an enumeration constant before the application runs.

It usually takes several development iterations to achieve a well-designed program. Be willing to backtrack from bad design decisions.