# GitHub Challenge

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

Hey there!

Your challenge is ready.
Follow the instructions provided for this challenge and complete the required tasks in this repository.

Make sure your work is committed and pushed to your repository before submission.

Good luck!


---

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)


### Service Being Monitored

The service in this project is a simulated payment service. The data given for the service
includes things like response time, CPU usage, memory usage and logs.

### Operational Problem

The main problem is to find when the payment service is not working normally. For example,
if the response time is too high or the CPU and memory usage goes above the given limit,
it can be considered as an unusual situation. The logs can also give information about
problems in the service.


## Data Analysis

I checked the operational data given for the payment service and found three main
metrics: response time, CPU usage and memory usage.

The log information is given using the `log_level` and `message` fields. The
`timestamp` field shows when each record was collected. The data is recorded
every one minute from 10:00 to 10:09.

Most of the data looks normal from 10:00 to 10:04 and again from 10:07 to 10:09.
During this time, the response time is around 120-150 ms and the CPU and memory
usage are also at normal levels. The logs also show that the payment requests
were processed successfully.

The data at 10:05 and 10:06 looks unusual. At 10:05, the response time goes up
to 610 ms and the log says "Payment service timeout". At 10:06, the response
time is 640 ms, CPU usage is 94% and memory usage is 91%. The log also shows a
"Database connection timeout".

After 10:06, the values return to normal again. So these two records are the
main unusual observations in the given data.


## Anomaly Detection

The anomaly detector checks response time, CPU usage and memory usage using the
given thresholds. It also checks the log level for error events.

Two anomalies were detected in the data:

- At 10:05, the response time was 610 ms and the log showed an error.
- At 10:06, the response time was 640 ms, CPU usage was 94%, memory usage was
  91% and the log showed an error.

The normal records were not flagged as anomalies.

## Event Processing Flow

The detected anomaly is converted into an event and passed to the event
producer. The producer publishes the event to the event topic. The consumer
then reads the event from the same topic and the event is shown in the final
AIOps output.

The flow is:

Operational Data → Anomaly Detection → Event → Producer → Topic → Consumer → AIOps

## Issues Found and Corrected

There were two main issues in the provided workflow.

First, the anomaly detector was checking for `WARNING` log levels, while the
provided data contains `ERROR` log levels. I changed the check so that error
logs are detected.

Second, the producer and consumer were using different topic objects. Because
of this, the consumer was receiving zero events. I changed the workflow so
that both the producer and consumer use the same topic.

After these corrections, the consumer successfully received both anomaly
events.

## Final Execution Result

The final pipeline processed 10 records and detected 2 anomalies. Both anomaly
events were successfully published and consumed.

The final output showed:

- Records processed: 10
- Anomalies detected: 2
- Events consumed: 2

## Limitation and Possible Improvement

One limitation is that the anomaly detection uses fixed threshold values.
These values may not work equally well for every service or workload. A
possible improvement would be to calculate normal behaviour from historical
data and use dynamic thresholds for detecting unusual behaviour.

## How to Run

To reproduce the workflow:

1. Open the repository in GitHub Codespaces or VS Code.
2. Open the terminal in the repository.
3. Run the following command:

```bash
python src/aiops_pipeline.py


