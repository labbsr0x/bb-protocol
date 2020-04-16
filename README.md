## Big Brother Metric Protocol

A compliant **Big Brother** library should expose the following metrics: 

```
request_seconds_bucket{type, status, isError, errorMessage, method, addr, le}
request_seconds_count{type, status, isError, errorMessage, method, addr}
request_seconds_sum{type, status, isError, errorMessage, method, addr}
response_size_bytes{type, status, isError, errorMessage, method, addr}
dependency_up{name}
dependency_request_seconds_bucket{name, type, status, isError, errorMessage, method, addr, le}
dependency_request_seconds_count{name, type, status, isError, errorMessage, method, add}
dependency_request_seconds_sum{name, type, status, isError, errorMessage, method, add}
application_info{version}
```

In detail:

1. `request_seconds_bucket` is a metric that defines the histogram of how many requests are falling into the well defined buckets represented by the label `le`;
2. `request_seconds_count` is a counter that counts the overall number of requests with those exact label occurrences;
3. `request_seconds_sum` is a counter that counts the overall sum of how long the requests with those exact label occurrences are taking;
4. `response_size_bytes` is a counter that computes how much data is being sent back to the user for a given request type. It captures the response size from the `content-length` response header. If there is no such header, the value exposed as metric will be zero;
5. `dependency_up` is a metric to register weather a specific dependency is up (1) or down (0). The label `name` registers the dependency name;
6. Finally, `application_info` holds static info of an application, such as it's semantic version number; 

## Labels

For a specific request:

1. `type` tells which request protocol was used (e.g. `grpc`, `http`, `<your custom protocol>`);
2. `status` registers the response status code; 
3. `isError` let you know if the request's response status is considered an error;
4. `method` registers the request method (e.g. `GET` for http get requests);
5. `addr` registers the requested endpoint address;
6. and `version` tells which version of your service has handled the request;

## Ecosystem

The following libraries make part of **Big Brother** official libraries:

1. [`express-monitor`](https://github.com/labbsr0x/express-monitor) for Node JS Express apps;
2. [`servlet-monitor`](https://github.com/labbsr0x/servlet-monitor) for Java Servlets apps;
3. [`flask-monitor`](https://github.com/labbsr0x/flask-monitor) for Python Flask apps;
4. [`mux-monitor`](https://github.com/labbsr0x/mux-monitor) for the Golang Mux apps;
4. [TODO] `iris-monitor` for Golang Iris apps;

Without these, you would have to expose the metrics by yourself, possibly leading to inconsistencies and other errors when setting up your app's observability infrastructure with **Big Brother**.

# Big Brother

This is part of a more large application called [Big Brother](https://github.com/labbsr0x/big-brother). Go check it out!
