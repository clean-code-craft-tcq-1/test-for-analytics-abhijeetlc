# Test for Analytics

 Tests for Analytics functionality on a Battery Monitoring System.


## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. A timing/Clock mechanism to record the timestamp to analyse trends. ( can be a plugin ) 
3. Trend detection / analysis functionality. ( Logic ) 
4. Breach Detection
5. Service to create PDF of the trend data.
6. Service to issue notification of the analysed data and handle success/failure of the notification process.

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | No need to test the PDF Convereter, Out of scope for us.
Counting the breaches       |  Yes          | This is part of the software being developed
Detecting trends            |  Yes          | This is part of the software being developed
Notification utility        | No            | Assumption : This is a Off the shelf code and hence out of scope for our test. A count of the Number of times Notifiactions are issued can be tracked and tested.

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Should record minimum and maximum info to the PDF when info from CSV is analysed for trend and breach.
4. Should report as  "Invalid input" to the PDF when the csv has unsupported/unintended data
5. Should detect increasing trend (if observed) and report in PDF when when info from CSV is analysed for trend and breach.
6. Should report no increasing trend in case of constant values  and report in PDF when when info from CSV is analysed for trend and breach.
7. Should detect breaches and report in PDF when when info from CSV is analysed for trend and breach.
8. Should detect breache count and report in PDF when when info from CSV is analysed for trend and breach.
9. Should verify that PDF is stored on the server when analysis is completed.
10. Should verify that Notification is issued when PDF is published at the server.


### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | PDF file  | Success OR Failure Notification              | Fake notification service
Report inaccessible server | Server Info ( Address ) | Error return value               | Fake the server store
Find minimum and maximum   | csv file      | Min and Max Values               | None - it's a pure function
Detect trend               | csv file      |Trend info              | None - it's a pure function
Write to PDF               | Trend Input | PDF File of Trend data              | Fake the write to PDF service
