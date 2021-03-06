# Blazemeter

## Summary of the report

### Labels

You'll see the summary panel at the top of the report. This panel showcases key statistics of the test, including:

- Max Users - Maximum number of concurrent users generated at any given point in the test run.  (Note: this does NOT refer to the total users, only the total users who ran simultaneously at any given moment. As a result, Max Users may not match your total users, which may be significantly higher.)
- Average Throughput (Hits/s) - The average number of HTTP/s requests per second that are generated by the test.
Errors Rate - The ratio of bad responses out of all responses received.
- Average Response Time - The average amount of time from first bit sent to the network card to the last byte received by the client.
- 90 Percentile of Response Time - The top average value of the first 90% of all samples. Only 10% of the sample is higherthan this value.
- Average Bandwidth (MB/s) - The average bandwidth consumption in MegaBytes per second generated by the test.

### Overview

This section shows key configurations alongside the main categories of responses codes received during the test run. This really helps you grasp the general purpose and performance. These include:

- The Test Duration (HH:MM:SS)
- The Test's Start & End Times.
- The Test Type - JMeter Test, Multi-Test. URL/API Test, Webdriver Test.
- Locations: The geo-locations the load has originated from.
R- esponse Codes: A breakdown of the HTTP response status codes received during the test run.

### Graphs

There are two graphs which indicate the key performance metrics and their trends throughout the duration of the test:

- Load Graph - This shows the maximum number of users vs hits/s vs errors rate. In the example above, you can see that while the load increased gradually until it reached its maximum, the hit/s increased rapidly and remained relatively high for the duration of the test and the errors rate stayed at 0%.

- Response Time Graph - This shows the maximum number of users vs response times, revealing how the size of the load affects the response times.

## References

- https://guide.blazemeter.com/hc/en-us/articles/206733909-Summary-Report-Summary-Report
