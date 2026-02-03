# Microsoft Teams Firewall Issue (VLAN Specific)

## Summary
Users from one VLAN faced Microsoft Teams issues because required Microsoft 365 backend endpoints (SharePoint Online) were blocked by URL Filtering on Check Point.

## Environment
- Firewall: Check Point
- Feature: URL Filtering
- Impacted VLAN: 172.20.30.0/24

## Root Cause
URL Filtering categorized SharePoint traffic as "File Storage and Sharing" and blocked it for that VLAN, which impacted Teams features.

## Fix (Scoped & Safe)
Excluded only Microsoft 365 / SharePoint Online required endpoints from URL category-based blocking (not a global bypass).

## Evidence
Screenshots will be placed here:
`projects/teams-firewall-issue/screenshots/`
