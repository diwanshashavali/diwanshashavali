# 🧠 Splunk Web Server Log Analysis Dashboard

### 📌 Overview
This project demonstrates how to analyze **Apache/Nginx web server access logs** using Splunk.
It includes dashboards to visualize:
- Top visitors (by IP)
- Most accessed URLs
- HTTP status code trends
- 404 errors and their sources
- Traffic over time

### ⚙️ Project Structure
```
splunk-web-log-analysis/
├── dashboards/
│   └── web_traffic_overview.xml
├── sample_logs/
│   └── apache_access.log
├── configs/
│   ├── inputs.conf
│   └── props.conf
├── screenshots/
│   ├── overview.png
│   └── errors.png
└── README.md
```

### 🧩 Configuration Details

#### 1️⃣ inputs.conf
```ini
[monitor:///opt/logs/apache_access.log]
sourcetype = apache:access
index = web_index
disabled = false
```

#### 2️⃣ props.conf
```ini
[apache:access]
TIME_PREFIX = \[
TIME_FORMAT = %d/%b/%Y:%H:%M:%S %z
SHOULD_LINEMERGE = false
REPORT-access = apache_access_extractions
```

### 📊 Dashboard Overview
Key panels:
| Metric | Description |
|--------|--------------|
| Top 10 Visitor IPs | Shows IPs generating most traffic |
| Top 10 Requested URLs | Most visited pages |
| HTTP Status Breakdown | Pie chart of 200, 404, 500 responses |
| 404 Error Sources | IPs that triggered errors |
| Traffic Over Time | Timechart of all requests |

### 🕵️‍♂️ Example Search Queries
```spl
index=web_index sourcetype=apache:access 
| stats count by clientip 
| sort - count
```

```spl
index=web_index sourcetype=apache:access 
| stats count by uri_path 
| sort - count
```

```spl
index=web_index sourcetype=apache:access 
| timechart count by status
```

### 📷 Screenshots
Add dashboard screenshots here:
```
/screenshots/
├── overview.png
├── errors.png
```

### 🧪 Sample Data
Use the included sample Apache log file (`sample_logs/apache_access.log`) or your own.

### 🚀 Setup Instructions
1. Copy configs into `$SPLUNK_HOME/etc/system/local/`
2. Create index: `splunk add index web_index`
3. Restart Splunk
4. Import dashboard XML via UI

### 📘 Learnings
- Parsing and ingesting web server logs
- Creating Splunk dashboards
- Using SPL queries for insights

### 🏷️ Tags
#Splunk #Dashboard #ApacheLogs #SIEM #DataAnalytics
