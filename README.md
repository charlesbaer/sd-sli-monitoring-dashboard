# Stackdriver Monitoring Metrics for

This is the full set of dashboard elements for the associated Medium post. In the Medium post, I described building a monitoring dashboard using Stackdriver Monitoring for a backend app that I developed. The app included Cloud Functions logic, communication via Pub/Sub, calls to the Cloud Vision and Video Intelligence APIs and a BigQuery dataset. I covered the SLI monitoring metrics that I used in great detail in the Medium post, but didn't cover the application monitoring metrics for Cloud Functions, Pub/Sub, Cloud Storage and BigQuery on the monitoring dashboard. This page covers the Cloud Functions, Pub/Sub, Cloud Storage and BigQuery monitoring metrics that I used to build the full monitoring dashboard for the app.

## Here are images of the full dashboard
![SLI monitoring metrics](/images/dashboard_sli_metrics.png)
![Pub/Sub monitoring metrics](/images/dashboard_pubsub.png)
![GCS monitoring metrics](/images/dashboard_cloud_storage.png)
![Cloud Functions monitoring metrics](/images/dashboard_cloud_functions.png)
![BigQuery monitoring metrics](/images/dashboard_bigquery.png)

## Pub/Sub

There are many different metrics for Pub/Sub both for topics and subscriptions. Since I was primarily interested in the Pub/Sub orchestration between the functions, I added 4 different charts related to the Pub/Sub topics. 

1. Published message count - how many messages have been published to each topic.
    1.  Resource Type: pubsub_topic
    2.  Metric: publish requests
    3.  Group By: topic_id
    4.  Aggregation: sum

![Pub/Sub publish requests](/images/chart_pubsub_publish_requests.png)

2. Retained acknowledged message count - how many messages have not been processed for each topic
    1. Resource Type: pubsub_topic
    2. Metric: retained acknowledged messages
    3. Group By: topic_id
    4. Aggregation: sum

![Pub/Sub retained acknowledged messages](/images/chart_pubsub_retained_acknowledged.png)

3. Unacknowledged message count
    1. Resource Type: pubsub_topic
    2. Metric: number of unacknowledged messages
    3. Group By: topic_id
    4. Aggregation: sum

![Pub/Sub Unacknowledged message count](/images/chart_pubsub_unackonwledged_messages.png)

4. Published message operation count
    1. Resource Type: pubsub_topic
    2. Metric: number of unacknowledged messages
    3. Group By: topic_id
    4. Aggregation: sum
    
![Pub/Sub Published message operation count](/images/chart_pubsub_publish_messages_operations.png)


Taken all together, the Pub/Sub charts appeared as shown in the screenshot below.

![Pub/Sub monitoring dashboard](/images/dashboard_pubsub.png)

## Cloud Storage

For Cloud Storage, I was interested in the request rate, the number of objects and then the sizes for the data sent/received. To cover these metrics, I added 4 different charts:

1. Request count - the request rate/sec
    1. Request count - the request rate/sec
    2. Resource Type: gcs_bucket
    3. Metric: request count
    4. Filter: bucket_name=ic*
    5. Group By: bucket_name
    6. Aggregation: sum

![Cloud Storage request count](/images/chart_cloud_storage_request_count.png)


2. Object count - the count of how many objects are stored 
    1. Resource Type: gcs_bucket
    2. Metric: object count
    3. Filter: bucket_name=ic*
    4. Group By: bucket_name
    5. Aggregation: sum

![Cloud Storage object count](/images/chart_cloud_storage_object_count.png)

3.  Received bytes size - size of all uploaded files 
    1.  Resource Type: gcs_bucket
    2.  Metric: received bytes
    3.  Filter: bucket_name=ic*
    4.  Group By: bucket_name
    5.  Aggregation: sum

 ![Cloud Storage received bytes](/images/chart_cloud_storage_received_bytes.png)

4. Sent bytes size - size of all served files
    1.  Resource Type: gcs_bucket
    1.  Metric: sent bytes
    1.  Filter: bucket_name=ic*
    1.  Group By: bucket_name
    1.  Aggregation: sum

![Cloud Storage sent bytes](/images/chart_cloud_storage_sent_bytes.pngD)


Taken all together, the Cloud Storage charts appeared as shown in the screenshot below.

![Cloud Storage monitoring metrics](/images/dashboard_cloud_storage.png)


## Cloud Functions

For Cloud Functions, I was interested in the number of successful and failed executions, the memory used and the execution times for each function. I added 4 different charts to the dashboard.

1.  Execution times
    1.  Resource Type: cloud_function
    1.  Metric: execution times
    1.  Group By: function_name
    1.  Aggregation: 99th percentile


![Cloud Functions execution times](/images/chart_cloud_functions_exection_time.png)

2. Execution count
    1.  Resource Type: cloud_function
    1.  Metric: executions
    1.  Group By: function_name
    1.  Aggregation: sum

![Cloud Functions execution count](/images/chart_cloud_functions_executions.png)


3.  Memory usage
    1.  Resource Type: cloud_function
    1.  Metric: memory usage
    1.  Group By: function_name
    1.  Aggregation: sum

![Cloud Functions memory usage](/images/chart_cloud_functions_memory_usage.png)


4.  Execution error count
    1.  Resource Type: cloud_function
    1.  Metric: memory usage
    1.  Filter by: status != ok
    1.  Group By: function_name
    1.  Aggregation: sum

![Cloud Functions error count](/images/chart_cloud_functions_executions_error_count.png)


Taken all together, the Cloud Function charts appeared as shown in the screenshot below.

![Cloud Functions monitoring dashboard](/images/dashboard_cloud_functions.png)

## BigQuery 


For BigQuery, I added 4 different charts:

1.  Storage sizes 

    I added 2 different metrics to this chart including both the stored and uploaded dataset sizes.

    Stored dataset size 

    1.  Resource Type: bigquery_dataset
    1.  Metric: stored bytes
    1.  Filter by: dataset_id = ic_filtered_content
    1.  Group By: dataset_id
    1.  Aggregation: sum

![BigQuery stored/uploaded dataset sizes](/images/chart_bigquery_stored_bytes.png)

    Uploaded dataset size

    1.  Resource Type: bigquery_dataset
    1.  Metric: stored bytes
    1.  Filter by: dataset_id = ic_filtered_content
    1.  Group By: dataset_id
    1.  Aggregation: sum

![BigQuery stored/uploaded dataset sizes](/images/chart_bigquery_storage_uploaded_bytes.png)


2.  Uploaded rows
    1.  Resource Type: bigquery_dataset
    1.  Metric: uploaded rows
    1.  Filter by: dataset_id = ic_filtered_content
    1.  Group By: dataset_id
    1.  Aggregation: sum

![BigQuery uploaded rows](/images/chart_bigquery_uploaded_rows.png)


3.  Billed bytes size
    1.  Resource Type: bigquery_dataset
    1.  Metric: uploaded bytes billed
    1.  Filter by: dataset_id = ic_filtered_content
    1.  Group By: dataset_id
    1.  Aggregation: sum


![BigQuery billed bytes](/images/?chart_bigquery_uploaded_bytes.png)

4.  Query execution time
    1.  Resource Type: global
    1.  Metric: query execution time
    1.  Group By: project_id
    1.  Aggregation: sum


![BigQuery execution time](/images/chart_bigquery_execution_times.png)

Taken all together, the BigQuery charts appeared as shown in the screenshot below.

![BigQuery monitoring dashboard](/images/dashboard_bigquery.png)


