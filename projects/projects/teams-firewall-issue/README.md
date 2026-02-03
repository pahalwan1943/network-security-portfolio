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
