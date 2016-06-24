## Notes on Optimal Logging
from Anthony Vallone's post on [Google Testing Blog](http://googletesting.blogspot.com/2013/06/optimal-logging.html)

______

### 0. Logging Tips:
- never log too much:  
	- **makes it difficult to find info in the chatter**
- never log too little:  
	- There are normally two main goals of logging: 
		1. help with bug investigation and 
		2. event confirmation.
	- If your log can’t explain the cause of a bug or whether a certain transaction took place, you are logging too little.

### 1. What Gets Logged?
- Good things to log: 
	- Important startup configuration
	- Errors
	- Warnings
	- Changes to persistent data
	- Requests and responses between major system components
	- Significant state changes
	- User interactions
	- Calls with a known risk of failure
	- Waits on conditions that could take measurable time to satisfy
	- Periodic progress during long-running tasks
	- Significant branch points of logic and conditions that led to the branch
	- Summaries of processing steps or events from high level functions - Avoid logging every step of a complex process in low-level functions.

- Bad things to log: 
	- **Function entry** - Don’t log a function entry unless it is significant or logged at the debug level.
	- **Data within a loop** - Avoid logging from many iterations of a loop. It is OK to log from iterations of small loops or to log periodically from large loops.
	- **Content of large messages or files** - Truncate or summarize the data in some way that will be useful to debugging.
	- **Benign errors** - Errors that are not really errors can confuse the log reader. This sometimes happens when exception handling is part of successful execution flow.
	- **Repetitive errors** - Do not repetitively log the same or similar error. This can quickly fill a log and hide the actual cause. Frequency of error types is best handled by monitoring. Logs only need to capture detail for some of those errors.
 
### 2. Log Levels:
- don't log everything at the same log level.  
- Classic conventions for log levels:
	- **Debug** - verbose and only useful while developing and/or debugging.
	- **Info** - the most popular level
	- **Warning** - something went wrong, but the process can recover
	- **Critical** - the process cannot recover, and it will shutdown or restart
- The only **Log configurations** you'll really ever need:
	- **Production**
		- Every level is enabled except debug.  If something goes wrong in production, the logs should reveal the cause.
	- **Development and Debug**
		- While developing new code or trying to reproduce a production issue, enable all levels.
		
### 3. Test Logs

Log quality is equally important in test and production code. When a test fails, the log should clearly show whether the failure was a problem with the test or production system. If it doesn't, then test logging is broken.

- ####Test logs should always contain: 
	- test execution environment
	- Initial state
	- Setup steps
	- Test case steps
	- Interactions with the system
	- Expected results
	- Actual results
	- Teardown steps

### 4.  Conditional Verbosity With Temporary Log Queues: 
- when errors occur, the log should contain a lot of detail.  Unfortunately, detail that led to an error is often unavailable once the error is encountered.  Also, if you're following the rule of not logging too much, the log records prior to the error may not provide adequate detail. 
- a good way to solve this problem is to create **temporary, in-memory log queues.**
- Throughout processing of a transaction, **append verbose details** about each step to the queue. 
- If the transaction completes successfully, discard the queue and log a summary. 
- If an error is encountered, log the content of the entire queue and the error. 
- This technique is especially useful for test logging of system interactions.

### 5. Failures and Flakiness Are Opportunities:
- When production problems occur, you’ll obviously be focused on finding and correcting the problem, but you should also think about the logs. 
- If you have a hard time determining the cause of an error, it's a great opportunity to improve your logging. 
- Before fixing the problem, fix your logging so that the logs clearly show the cause. 
- If this problem ever happens again, it’ll be much easier to identify.
- If you cannot reproduce the problem, or you have a flaky test, enhance the logs so that the problem can be tracked down when it happens again.
- **Using failures to improve logging should be used throughout the development process.**  While writing new code, try to refrain from using debuggers and only use the logs. Do the logs describe what is going on? If not, the logging is insufficient.

### 6. Log Performance Data
- Logged timing data can help debug performance issues. 
- For example, it can be very difficult to determine the cause of a timeout in a large system, unless you can trace the time spent on every significant processing step. 
- This can be easily accomplished by logging the start and finish times of calls that can take measurable time: 
	- Significant system calls
	- Network requests
	- CPU intensive operations
	- Connected device interactions
	- Transactions
	
### 7. Tracking Information Through Many Threads and Processes:
- You should create unique identifiers for transactions that involve processing across many threads and/or processes. 
- The initiator of the transaction should create the ID, and it should be passed to every component that performs work for the transaction. 
- This ID should be logged by each component when logging information about the transaction. 
- This makes it much easier to trace a specific transaction when many transactions are being processed concurrently.

### 8. Monitoring and Logging Complement Each Other:
- A production service should have both logging and monitoring. 
- Monitoring provides a real-time statistical summary of the system state. 
- It can alert you if:
	- a percentage of certain request types are failing, 
	- it is experiencing unusual traffic patterns, 
	- performance is degrading, 
	- or other anomalies occur. 
- In some cases, this information alone will clue you to the cause of a problem. 
- However, in most cases, a monitoring alert is simply a trigger for you to start an investigation. 
- **Monitoring shows the symptoms of problems** 
- **Logs provide details and state on individual transactions**, so you can fully understand the cause of problems.
