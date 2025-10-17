### Real Time Analytics
- as we see data lake is pulling the data and downstream services which are using these are pulling again from datalake
- there is another thing which can be very useful to our business if we use real time analytics
- lets say there is some item in you app which is getting lots of view and people are so much interested in this
- now these kind of information are required immediately , now to do so we will stream these data to message queues, this is called streaming architecture
- what if few events are missed, doesnt really matter to analytics service, as availability is important than consitency
- you also want general view of these data which is also called observability
- map reduce is good for doing complex operation, where as streaming architecture is good simple operations
- this overall architecture is lambda architecture, combination of streaming acrhitecture and map reduce architecture
