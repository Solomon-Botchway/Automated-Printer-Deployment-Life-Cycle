# Automated Departmental Printer Deployment

## Objective

Implement automated printer deployment based on department membership using Active Directory Security Groups and Group Policy Preferences.

## Initial Challenge

The original printer deployment did not automatically install printers for users at first sign-in.

Users were required to manually browse:

```text
\\DC01
```

and connect to their departmental printer before the printer became available.

This behavior did not meet the desired enterprise standard for automated provisioning.

## Investigation

Several deployment methods were evaluated.

### Attempt 1

Used:

```text
Microsoft Print to PDF
```

as a test printer.

Outcome:

```text
Unsuccessful
```

Microsoft Print to PDF could not be shared in a way that supported the deployment requirements.

### Attempt 2

A physical HP wireless printer was integrated into the SoloTech lab.

Infrastructure:

```text
Host Network
    ↓
Hyper-V External Switch
    ↓
DC01
    ↓
HP Network Printer
```

The printer was installed on DC01 and additional logical departmental printers were created using the HP print driver.

## Department Printer Structure

```text
IT-PRINTER

HR-PRINTER

FINANCE-PRINTER

SALES-PRINTER

CUST-SERV-PRINTER
```

## Printer Security Configuration

Initially:

```text
Everyone
```

had print permissions.

Result:

```text
All users could access all printers.
```

This violated least-privilege principles.

### Resolution

Removed:

```text
Everyone
```

from printer permissions.

Assigned department security groups:

```text
IT-Team

HR-Team

Finance-Team

Sales-Team

CustomerService-Team
```

to their corresponding printers.

## Printer Automation

Implemented Group Policy Preferences to:

- Deploy departmental printers automatically.
- Set departmental printers as default printers.
- Override Microsoft "Manage my default printer" behavior.
- Remove printers when users move departments.
- Deploy the correct printer based on current group membership.

### Example

User:

```text
Finance-Team
```

Receives:

```text
FINANCE-PRINTER
```

as default printer.

If reassigned to:

```text
HR-Team
```

the system automatically:

```text
Removes FINANCE-PRINTER

Deploys HR-PRINTER

Sets HR-PRINTER as default
```

without manual administrator intervention.

## Security Validation

Testing confirmed:

| Scenario | Result |
|-----------|----------|
| IT User → IT Printer | ✅ Allowed |
| IT User → HR Printer | ❌ Access Denied |
| IT User → Finance Printer | ❌ Access Denied |
| Finance User → Finance Printer | ✅ Allowed |
| Customer Service User → CS Printer | ✅ Allowed |
| Unauthorized User → Department Printer | ❌ Access Denied |

## Skills Demonstrated

- Print Management
- Group Policy Preferences
- Active Directory Security Groups
- Role Based Access Control (RBAC)
- Least Privilege Access
- Printer Security
- Enterprise Printer Deployment
- Lifecycle Access Management
- User Provisioning
- User Offboarding and Role Changes

## Cyber Security Relevance

This implementation demonstrates:

```text
Least Privilege

Role Based Access Control

Resource Segregation

Identity-Based Access Management

Automated Access Governance
```

which are foundational concepts used in enterprise security and identity management environments.
