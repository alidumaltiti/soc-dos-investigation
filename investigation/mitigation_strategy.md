# Incident Mitigation Strategy

## Immediate Containment
To instantly restore service availability to the web application, the offending IP address must be dropped at the perimeter.

**Action:** Drop all incoming traffic from `198.51.100.42`.
**Command (iptables):**
`sudo iptables -A INPUT -s 198.51.100.42 -j DROP`

## Long-Term Remediation
To prevent future HTTP Flood attacks:
1. **Implement Rate Limiting:** Configure Nginx to limit the number of requests a single IP address can make within a specific timeframe.
2. **Deploy a Web Application Firewall (WAF):** Utilize a WAF to automatically detect and filter out anomalous traffic patterns and volumetric attacks before they reach the application server.