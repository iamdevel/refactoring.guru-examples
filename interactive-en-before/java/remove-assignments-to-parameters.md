Let's look at <i>Remove Assignments to Parameters</i> using a small discount calculation method as an example.

Initialize our variable with the parameter value.

In the method body, replace all references to the parameter with the variable that we have created.

And finally, to explicitly say that no assignments can be made to the parameters, you can add the keyword <code>final</code> to each of them.

Let's run the final compile.

Now refactoring is complete. If you like, you can compare the old and new code.