Cloudflare Prometheus Alert Rules
=================================

This repository contains a set of Prometheus alert rules specifically designed for monitoring Cloudflare metrics. These rules help you detect and respond to various issues related to website traffic, security threats, firewall events, and more.

Alert Rules Overview
--------------------

### 1\. **Cloudflare High Traffic Spike**

-   **Description:** Detects unusually high visitor traffic on a website.
-   **Expression:** `rate(cloudflare_zone_requests_total[5m]) > 1000`
-   **Severity:** Warning
-   **Actions:** Monitor website performance, check for legitimate traffic sources or potential attacks, consider scaling resources.


### 2\. **Cloudflare High Threat Rate**

-   **Description:** High rate of security threats detected on a website.
-   **Expression:** `rate(cloudflare_zone_threats_total[20m]) > 40`
-   **Severity:** Critical
-   **Actions:** Review security logs, verify Cloudflare security settings, consider enabling additional security measures.

### 3\. **Cloudflare High Firewall Events**

-   **Description:** High number of requests blocked by the website firewall.
-   **Expression:** `rate(cloudflare_zone_firewall_events_count{action="block"}[5m]) > 1000`
-   **Severity:** Warning
-   **Actions:** Review blocked traffic patterns, verify firewall rules, check for false positives.

### 4\. **Cloudflare Country-Based Attack**

-   **Description:** High threat activity detected from a specific country.
-   **Expression:** `rate(cloudflare_zone_threats_country[20m]) > 20`
-   **Severity:** Warning
-   **Actions:** Review traffic patterns from the affected country, consider geographic-based access rules.

### 5\. **Cloudflare High Bandwidth Usage**

-   **Description:** Large amounts of data being transferred from the website.
-   **Expression:** `rate(cloudflare_zone_bandwidth_total[5m]) > 10485760`
-   **Severity:** Warning
-   **Actions:** Identify high-bandwidth content, check for unauthorized content sharing, review bandwidth optimization options.

### 6\. **Cloudflare High Error Rate**

-   **Description:** High error rate on website requests.
-   **Expression:** `sum(rate(cloudflare_zone_requests_status{status=~"5.."}[5m])) by (zone) / sum(rate(cloudflare_zone_requests_total[5m])) by (zone) * 100 > 5`
-   **Severity:** Warning
-   **Actions:** Check website backend health, review error logs, verify system functionality, test critical user workflows.

Usage
-----

To use these alert rules, simply add them to your Prometheus configuration file under the `rule_files` section. Ensure that you have the necessary Cloudflare metrics exposed to Prometheus.

```
rule_files:
  - /path/to/cfalerts-yaml

```

Testing and Validation
----------------------

All rules have been tested. Make sure to validate your rules before deploying them in a production environment.

Contributing
------------

Feel free to contribute by opening issues or pull requests. Your feedback and improvements are highly appreciated!

Resources
---------

-   [Prometheus Documentation](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/)
