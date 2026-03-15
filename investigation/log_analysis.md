# Technical Log Analysis

## Objective
Identify the source of the traffic spike causing the 503 (Service Unavailable) and 408 (Request Timeout) errors on `www.yummyrecipesforme.com`.

## Command Line Investigation
To determine which IP addresses were sending the most requests, I utilized Linux command-line tools to parse the `simulated_access.log` file.

**Command Executed:**
`cat simulated_access.log | awk '{print $1}' | sort | uniq -c | sort -nr`

**Findings**
1. **Malicious Actor:** The IP address `198.51.100.42` is responsible for a highly disproportionate number of requests in a very short timeframe.
2. **Targeted Endpoint:** The logs reveal this IP is repeatedly hitting the `/search?q=dinner` endpoint. Search queries require database lookups, making them an ideal target for an Application Layer HTTP Flood attack.
3. **Impact on Legitimate Users:** The subsequent requests from regular users (`192.0.2.88` attempting to view a recipe) resulted in `408 Request Timeout` errors, confirming the server's resources were exhausted.