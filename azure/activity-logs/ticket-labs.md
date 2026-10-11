# Azure Activity Log Labs

## Ticket 14 - RBAC Authorization Failure

**Finding:** User authenticated successfully but could not restart the VM because the assigned Reader role did not permit the restart action.

**Next check:** Verify whether the user should have a role that permits VM management and at what scope.

---

## Ticket 15 - Resource Deletion

**Finding:** The VM did not crash. It was successfully deleted by an automation identity with sufficient permissions.

**Evidence:**
- Delete operation succeeded
- Caller: automation-prod@contoso.com
- Role: Virtual Machine Contributor
- No resource lock

**Next check:** Determine whether deletion was intentional and whether a CanNotDelete lock should have existed.

---

## Ticket 16 - Network Configuration Change

**Finding:** The VM remained healthy, but an NSG rule was changed from allowing inbound HTTPS traffic to denying it.

**Evidence:**
- Caller: network-admin@contoso.com
- TCP 443
- Access changed from Allow to Deny
- Change succeeded

**Next check:** Determine whether the change was intentional before reverting it.

---

## Ticket 17 - Failed Deployment

**Finding:** Authentication and authorization succeeded, but the deployment failed because the requested storage account name was unavailable.

**Evidence:**
- Status: BadRequest
- Error: InvalidTemplateDeployment
- Storage account name unavailable

**Next check:** Choose an available valid storage account name and retry the deployment.

---

## Ticket 18 - KQL Log Investigation

Status: NEXT LAB

Goal:
Use KQL to find relevant Azure Activity Log records instead of being given the answer directly.
