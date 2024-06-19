Lazy evaluation is a  functional programming technique, where the evalutation of expressions is delayed until their results are actually needed. This approach helps optimize the execution of programs by reducing the computional load, enabling efficient processing and allocation of resources.

As you see, when  you create a Spark Dataframe, the value is not computed yet until you call <code>df.show()</code> , the value is computed and shown.

