# Microsoft Teams Firewall Issue – VLAN Specific

## Project Summary
Users from a specific VLAN were unable to use Microsoft Teams
features such as meetings and chat, while users from other VLANs
were working fine.

## Environment
- Firewall: Check Point
- Feature involved: URL Filtering
- User VLAN: 172.20.30.0/24
- Application: Microsoft Teams / SharePoint Online

## Problem Statement
Microsoft Teams traffic was intermittently failing for users in one
VLAN due to security policy restrictions.

## High-Level Investigation
- Teams was partially working (login successful)
- Meetings and content failed to load
- Firewall logs showed traffic categorized as **sharepoint.com**
  being blocked under File Storage and Sharing category

## Outcome
Root cause was identified as URL Filtering policy blocking required
Microsoft 365 backend services used by Microsoft Teams.

## Root Cause Analysis
The issue was caused by a URL Filtering policy on the Check Point firewall.
Microsoft Teams relies on backend services hosted on SharePoint Online
(`sharepoint.com`) for chat, meeting content, and file access.

The URL Filtering blade categorized SharePoint traffic under
**File Storage and Sharing**, which was blocked for the affected VLAN.
As a result, critical Microsoft Teams components failed to load.

## Evidence Collected
- Firewall logs showed dropped connections to `sharepoint.com`
- Drops occurred only for the affected VLAN subnet
- Users from other VLANs were not impacted

## Fix Implementation
- Identified the restrictive URL Filtering rule
- Allowed Microsoft 365 traffic using supported allow-listing
- prevent category-based blocking while maintaining security controls
for other traffic.

## Verification
- Firewall logs confirmed no further drops
- Microsoft Teams meetings, chat, and content loaded successfully
- Users confirmed stable performance after the change

## Lessons Learned
- Modern SaaS applications depend on multiple backend services
- URL category-based blocking can impact business-critical applications
- Vendor-recommended allow-listing should be preferred for SaaS platforms
