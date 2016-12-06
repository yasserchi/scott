Required software for development
---------------------------------

- *Java 1.7* to compile the core package, and *Java 1.8* to run the whole test suite
- *Maven 3.0.5*


Project layout
--------------
The core module where you can find all the instrumentation and rendering parts is ```scott```,
while the related tests are in the```scott-tests``` project. These two are submodules of the root pom,
which is provided for convenience. The tests are in a separate module, because the suite excersizes
the complete artifact much like a real project would use it.

When chasing a bug or adding a new feature make sure to add tests for the expected behavior
and build the project with all the tests by issueing ```mvn clean install``` on the root pom.
This test suite is responsible for making Scott crash-free, and verify that
the correct values are recorded during test execution. The report rendering part is not examined
in this test suite.
The correct rendering can be ensured by running the example test suites in the ```scott-examples```,
and examining their outputs. These projects also serve as an example about using Scott with various tools
in your projects.


Debug mode
----------
Scott can be started in debug mode to make it easier to see what instrumentations happen during the
test execution. To activate it, just set the ```scottDebug``` environment variable to true when running
your tests (for example on Unix: ```export scottDebug="true"```), then Scott shows the visited and modified classes.

For example:
```
Scott instrumentation: Visiting: hu/advancedweb/scott/RecordMutationTest.mutationWithLoops
Scott instrumentation:  - instrumentToClearTrackedDataAndSignalStartOfRecording
Scott instrumentation:  - instrumentToTrackVariableName at 81: LocalVariableScope [var=1, name=i, start=81, end=88]
Scott instrumentation:  - instrumentToTrackVariableState of variable at 81: LocalVariableScope [var=1, name=i, start=81, end=88]
Scott instrumentation:  - instrumentToTrackVariableName at 83: LocalVariableScope [var=2, name=j, start=81, end=86]
Scott instrumentation:  - instrumentToTrackVariableState of variable at 83: LocalVariableScope [var=2, name=j, start=81, end=86]
Scott instrumentation:  - instrumentToTrackVariableName at 84: LocalVariableScope [var=1, name=i, start=81, end=88]
Scott instrumentation:  - instrumentToTrackVariableState of variable at 84: LocalVariableScope [var=1, name=i, start=81, end=88]
Scott instrumentation:  - instrumentToTrackVariableState of variable at 85: LocalVariableScope [var=2, name=j, start=81, end=86]
...
```
