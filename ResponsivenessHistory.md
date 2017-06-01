# Responsiveness History Tile
The overview tile for responsiveness history represents the aggregated responsiveness (measured by 99 Percentile of response time recorded by all request type telemetry) against the CPU utilization of service plans.
On further drill-down, the views show responsiveness vs utilization details along with most frequent operations and their count for each service – Web, Identity Access Management, Business Services and Product Services.
The view used here is two timelines and list which is created using total of three queries – one query each for bar charts with time intervals and the other for list of most frequent requests. The first timeline chart represents 99 percent response time for all requests served by the service, while the second chart represents the average CPU utilization of the corresponding infra during the same time.

**Query for First chart**:
Type:AzureMetrics MetricName="AverageResponseTime" (Resource=NAME_OF_APP_SERVICE) | measure percentile99(Average) by Resource

**Query for second chart**:
Type=AzureMetrics MetricName=CpuPercentage (Resource=NAME_OF_SERVICE_PLAN) | measure avg(Average) by Resource
 
The third query provides details about request URI, VERB and count of such operations listed in decreasing order.
 
**Query for third chart**:
Type=ApplicationInsights Request (ApplicationName = NAME_OF_APP_SERVICE) | measure count() by RequestName 
