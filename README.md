# Automated-Printer-Deployment-Life-Cycle
Deploy departmental printers automatically using Group Policy Preferences and Active Directory Security Groups.
## Automated Departmental Printer Deployment

### Business Objective

Deliver a fully automated printer deployment solution that:

- Assigns printers based on department membership
- Automatically sets default printers
- Removes obsolete printers during department transfers
- Requires zero manual intervention after onboarding

### Challenges Encountered

Initial deployment required users to manually browse:

```text
\\DC01
```

to install printers.

Windows also repeatedly reverted default printers to:

```text
Microsoft Print to PDF
```

during policy refresh cycles.

### Solution

Implemented:

- Group Policy Preferences
- Item-Level Targeting
- Active Directory Security Groups
- Registry-based printer management
- Automated default printer enforcement

### Outcome

Users automatically receive:

- Department-specific printer access
- Correct default printer assignment
- Automatic printer replacement if department membership changes

Example:

```text
Finance-Team
        ↓
FINANCE-PRINTER
        ↓
Default Printer Assigned
```

If the user moves to HR:

```text
FINANCE-PRINTER removed
HR-PRINTER deployed
HR-PRINTER becomes default
```

### Skills Demonstrated

- Print Management
- Group Policy Preferences
- Printer Automation
- Registry Configuration
- RBAC
- User Lifecycle Management
