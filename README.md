# LDAP IAM Lab — Group Policy & Least Privilege Enforcement

## Overview
Hands-on Identity and Access Management (IAM) lab completed using CyberKy's IAM Defender platform. The objective was to deploy a live LDAP directory server, provision a test user identity, create a least-privilege group policy, and validate access control enforcement through real login testing and admin verification.

## Technologies Used
- **LLDAP** — Lightweight LDAP server (web UI)
- **LDAP Protocol** — Directory service protocol for identity and access management
- **Group Policy** — Group-based access restriction and permission enforcement
- **Access Control** — Least privilege enforcement and access validation

## Lab Objectives
- Provision a SOC Tier 1 analyst user identity
- Create a read-only group policy aligned with least privilege
- Validate that restricted users cannot perform admin-level operations
- Perform final admin verification to confirm group integrity

## Steps Completed

### Step 1 — Accessed the LLDAP Environment
Launched the CyberKy lab workspace and logged into LLDAP as `admin` via the web UI at `http://172.19.0.3:17170/`.

### Step 2 — Provisioned a New User
Created user identity `analyst1` to simulate a SOC Tier 1 analyst requiring restricted, read-only access to the directory.

### Step 3 — Created a Least-Privilege Group Policy
Created the group `soc-tier1-readonly` designed to enforce read-only access — blocking all write and admin-level directory operations.

### Step 4 — Assigned User to Group
Assigned `analyst1` to the `soc-tier1-readonly` group, applying the least-privilege policy to the user account.

### Step 5 — Validated Policy Enforcement
Logged in as `analyst1` and tested access behavior:
- ✅ Can authenticate successfully
- ✅ Can view own profile (read access confirmed)
- ❌ Cannot access `/users` list — **Error: Unauthorized access to user list**
- ❌ Cannot perform admin-level operations

### Step 6 — Final Admin Verification
Logged back in as `admin` and confirmed:
- ✅ `soc-tier1-readonly` members: `analyst1` only
- ✅ `analyst1` absent from `lldap_admin` group
- ✅ No unintended group memberships detected
- ✅ Zero privilege escalation confirmed

## Evidence / Findings

| Test | Result |
|---|---|
| analyst1 login | ✅ Allowed |
| analyst1 view own profile | ✅ Allowed |
| analyst1 access /users list | ❌ Blocked — Unauthorized |
| analyst1 in soc-tier1-readonly | ✅ Confirmed |
| analyst1 in lldap_admin | ❌ Absent — Confirmed |
| Privilege escalation | ❌ None detected |

## Key Concepts Demonstrated
- **Principle of Least Privilege** — Users receive only the access needed for their role
- **Group-based Policy Enforcement** — Permissions managed at group level, not individual user level
- **Identity Provisioning** — Creating and configuring user accounts in a live directory
- **Access Control Validation** — Testing and confirming restrictions hold up under real login conditions
- **Admin Integrity Verification** — Confirming no unintended privilege escalation occurred

## Screenshots
*(See /screenshots folder)*

## Platform
**CyberKy IAM Defender Course** — [cyberky.com](https://cyberky.com)
