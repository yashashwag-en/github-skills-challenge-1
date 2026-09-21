# GitHub Challenge

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

Hey there!

Your challenge is ready.
Follow the instructions provided for this challenge and complete the required tasks in this repository.

Make sure your work is committed and pushed to your repository before submission.

Good luck!


---

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)


## AIOps Assessment

This project is a small simulation of a payment service. The service data contains things
like response time, CPU usage, memory usage and log messages.

The main problem here is to find out when the payment service is behaving abnormally.
For example, if the response time becomes too high or the CPU/memory usage crosses a
certain limit, it can be treated as an anomaly.

The purpose of AIOps in this project is to automatically check the service data, detect
these problems and create events when an anomaly is found. These events are then passed
through the producer, topic and consumer as part of the AIOps pipeline.

Overall, the flow is:

Service Data → Anomaly Detection → Event Producer → Event Topic → Event Consumer

