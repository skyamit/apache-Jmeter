# Apache JMeter Documentation (Intermediate Level)

## 1. Overview

Apache JMeter is an open-source tool used for performance testing of web applications, APIs, and backend systems. It helps simulate concurrent users and analyze system behavior under load.

---

## 2. Installation & Setup

### Prerequisites

* Java (JDK 8 or above)

### Steps

```bash
# Download JMeter
https://jmeter.apache.org/download_jmeter.cgi

# Extract and run
cd apache-jmeter/bin
./jmeter.sh   # Linux/Mac
jmeter.bat    # Windows
```

---

## 3. JMeter Architecture

```plaintext
Test Plan
 ├── Thread Group
 │     ├── Samplers (HTTP/JDBC)
 │     ├── Config Elements
 │     ├── Assertions
 │     └── Listeners
```

---

## 4. Core Components

### 4.1 Test Plan

* Root container
* Defines overall execution

---

### 4.2 Thread Group

Controls load simulation:

* Number of Threads (Users)
* Ramp-Up Time
* Loop Count

Example:

```plaintext
Users: 100
Ramp-up: 50 sec
Loop: 1
```

---

### 4.3 Samplers

#### HTTP Request

* Used to call APIs

```plaintext
Method: GET / POST
URL: http://localhost:8080/api
```

---

### 4.4 Config Elements

#### HTTP Header Manager

```plaintext
Authorization: Bearer ${token}
Content-Type: application/json
```

#### CSV Data Set Config

Used for multiple users:

```csv
username,password
user1,pass1
user2,pass2
```

---

### 4.5 Assertions

Used to validate responses:

* Response Code = 200
* Response contains expected value

---

### 4.6 Listeners

| Listener          | Purpose             |
| ----------------- | ------------------- |
| View Results Tree | Debugging           |
| Summary Report    | Performance summary |
| Aggregate Report  | Metrics             |

---

## 5. Correlation (Dynamic Data Handling)

### Problem

APIs return dynamic values (token, sessionId)

### Solution

Use Extractors

#### JSON Extractor

```plaintext
Variable Name: token
JSON Path: $.accessToken
```

#### Use in next request

```plaintext
Authorization: Bearer ${token}
```

---

## 6. Parameterization

Use CSV Data Set Config:

```csv
userId
1
2
3
```

Usage:

```plaintext
/api/user/${userId}
```

---

## 7. Timers (Realistic Load)

* Constant Timer
* Uniform Random Timer

Purpose:

* Simulate real user delays
* Avoid sudden spike

---

## 8. Controllers

* Loop Controller → Repeat requests
* If Controller → Conditional execution
* Transaction Controller → Measure full flow

---

## 9. Execution Modes

### GUI Mode

* Used for debugging only

### Non-GUI Mode (Recommended)

```bash
jmeter -n -t test.jmx -l result.jtl
```

---

## 10. Performance Metrics

| Metric            | Meaning                      |
| ----------------- | ---------------------------- |
| Throughput        | Requests/sec                 |
| Avg Response Time | Average latency              |
| Error %           | Failed requests              |
| 90th Percentile   | 90% requests below this time |

---

## 11. Types of Testing

* Load Testing → Expected traffic
* Stress Testing → Beyond limits
* Spike Testing → Sudden load

---

## 12. Best Practices

* Avoid hardcoding values
* Use CSV for scalability
* Always add assertions
* Use realistic ramp-up
* Run tests in non-GUI mode
* Monitor system (CPU, memory)

---

## 13. Common Mistakes

* Running load in GUI mode
* No correlation handling
* No assertions
* Single user testing
* Ignoring response validation

---

## 14. Debugging

* Use View Results Tree
* Use Debug Sampler
* Print variables:

```plaintext
${variableName}
```

---

## 15. Sample Flow (Login + API)

```plaintext
Thread Group
 ├── CSV Data Set Config
 ├── HTTP Request (Login)
 │     └── JSON Extractor (token)
 ├── HTTP Header Manager
 │     Authorization: Bearer ${token}
 └── HTTP Request (Create Order)
```

---

## 16. CI/CD Integration

* Integrate with Jenkins / GitHub Actions
* Run JMeter in pipeline
* Fail build on high error %

---

## 17. Advanced Topics

* Distributed Testing
* Backend Listener (Grafana)
* Plugins (Custom Reports)
* Docker-based execution

---

## 18. Interview Quick Summary

JMeter is used to simulate concurrent users using thread groups, execute API calls using samplers, handle dynamic data using extractors, validate responses using assertions, and analyze performance using reports. Tests are executed in non-GUI mode for scalability and can be integrated with CI/CD pipelines.

---

End of Documentation
