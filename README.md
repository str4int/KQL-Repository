# KQL Repository

Welcome to my KQL _(Kusto Query Language)_ repository!

This repository contains a collection of KQL queries that I  used on daily security operation.

I will updated on a regularly basis and everyone is welcome to contribute with useful queries to help improve and expand this collection.

## Table of Contents

- [Getting Started](#getting-started)
- [Difference Between Sentinel and Defender Queries](#difference-between-sentinel-and-defender-queries)
- [Contributing](#contributing)


# Getting-started
Browse through the different categories of queries available in the repository.

Each query is documented with a description of what it does and how to use it.

# Difference Between Sentinel and Defender Queries
KQL queries can be used in different Microsoft products, such as Azure Sentinel and Microsoft Defender for Endpoint. Here's how they differ:

- **Azure Sentinel**: Cloud-native SIEM (Security Information and Event Management) solution. Queries in Sentinel are used for detecting, hunting, and investigating threats across various data sources. Sentinel queries often analyze data from a wide range of logs, such as Azure Activity, SecurityEvents, and OfficeActivity.

- **Microsoft Defender**: Security platform designed to help enterprise networks prevent, detect, investigate, and respond to advanced threats. Queries in Defender are used to analyze endpoint data and alerts, focusing on identifying and responding to security threats on individual devices.

Example Sentinel Query:
```
// Failed login Count 
// Resources with most failed log in attempts. 
SigninLogs
| where TimeGenerated >= ago(1d)
| where ResultType !=0
| summarize FailedLoginCount=count() by ResourceDisplayName
| sort by FailedLoginCount desc
```

Example Defender Query:
```
// Search for malicious links where user was allowed to proceed through. 
UrlClickEvents
| where Timestamp >= ago(7d)
| where ActionType == "ClickAllowed" or IsClickedThrough !="0"
| where ThreatTypes has "Phish"
| summarize by ReportId, Timestamp, IsClickedThrough, AccountUpn, NetworkMessageId, ThreatTypes
```
Understanding these slight differences can help you craft queries that are tailored to the specific needs and capabilities of each platform.

# Contributing
Whether you are a SOC analyst, threat researcher, or simply passionate about IT and security, your contributions are valuable. If you have a useful KQL query that you would like to share, please feel free to submit:

1. Fork the repository.
2. Create a new branch: `git checkout -b feature-branch-name`.
3. Add your query to the appropriate category folder.
4. Commit your changes: `git commit -m 'Add new query'`.
5. Push to the branch: `git push origin feature-branch-name`.
6. Create a pull request.

/!\ Please make sure your query is well-documented and tested.


**Happy querying!**
