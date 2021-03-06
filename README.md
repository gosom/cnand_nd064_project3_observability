[img1]: ./answer-img/monitoring_verify.png
[img2]: ./answer-img/observability_verify.png
[img3]: ./answer-img/grafana_after_login.png
[img4]: ./answer-img/basic_dashboard.png

**Note:** For the screenshots, you can store all of your answer images in the `answer-img` directory.

## Verify the monitoring installation

*TODO:* run `kubectl` command to show the running pods and services for all components. Take a screenshot of the output and include it here to verify the installation

```
kubectl get svc --namespace=monitoring
kubectl get pods --namespace=monitoring
```

![][img1]

```
kubectl get svc --namespace=observability
kubectl get pods --namespace=observability
```
![][img2]

## Setup the Jaeger and Prometheus source

*TODO:* Expose Grafana to the internet and then setup Prometheus as a data source. Provide a screenshot of the home page after logging into Grafana.

In a terminal run:
```
kubectl port-forward -n monitoring service/prometheus-kube-prometheus-prometheus 9090
```

Now in `http://localhost:9090` you can access Prometheus

in another terminal run:
```
kubectl port-forward -n monitoring $(kubectl get pods --namespace=monitoring|grep grafana|cut -d ' ' -f1) 3000
```

Now in `http://www.localhost:3000/login` is the Login page of Grafana

Username is `admin`

To grab the password:
```
kubectl get secret --namespace monitoring prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

![][img3]


## Create a Basic Dashboard
*TODO:* Create a dashboard in Grafana that shows Prometheus as a source. Take a screenshot and include it here.

![][img4]

## Describe SLO/SLI
*TODO:* Describe, in your own words, what the SLIs are, based on an SLO of *monthly uptime* and *request response time*.

A Service Level Indicator (SLI), is a metric that is used to determine if the SLO (Service Level Objective) is being met.

In the case the SLO is based on monthly uptime and request response time. 
Then the one SLI is the exact value of the uptime and the other SLI is the exact value of the mean of the response times.


## Creating SLI metrics.
*TODO:* It is important to know why we want to measure certain metrics for our customer. Describe in detail 5 metrics to measure these SLIs. 

- The uptime, which is the time which the service is up and running
- The response time of requests
- The failure rate, which is the amount of errors (non success status codes, most probably 50x errors or 40x erros)
- The amount of CPU usage
- The amount of memory usage


## Create a Dashboard to measure our SLIs
*TODO:* Create a dashboard to measure the uptime of the frontend and backend services We will also want to measure to measure 40x and 50x errors. Create a dashboard that show these values over a 24 hour period and take a screenshot.

## Tracing our Flask App
*TODO:*  We will create a Jaeger span to measure the processes on the backend. Once you fill in the span, provide a screenshot of it here.

## Jaeger in Dashboards
*TODO:* Now that the trace is running, let's add the metric to our current Grafana dashboard. Once this is completed, provide a screenshot of it here.

## Report Error
*TODO:* Using the template below, write a trouble ticket for the developers, to explain the errors that you are seeing (400, 500, latency) and to let them know the file that is causing the issue.

TROUBLE TICKET

Name:

Date:

Subject:

Affected Area:

Severity:

Description:


## Creating SLIs and SLOs
*TODO:* We want to create an SLO guaranteeing that our application has a 99.95% uptime per month. Name three SLIs that you would use to measure the success of this SLO.

## Building KPIs for our plan
*TODO*: Now that we have our SLIs and SLOs, create KPIs to accurately measure these metrics. We will make a dashboard for this, but first write them down here.

## Final Dashboard
*TODO*: Create a Dashboard containing graphs that capture all the metrics of your KPIs and adequately representing your SLIs and SLOs. Include a screenshot of the dashboard here, and write a text description of what graphs are represented in the dashboard.  
