# Microsoft Entra Sign-In Log Labs

## Ticket 1 — Conditional Access

**Result:** Failed

**Finding:** Authentication attempt was blocked by Conditional Access.

**Next check:** Determine which Conditional Access requirement failed.

---

## Ticket 2 — Device Compliance

**Result:** Failed

**Evidence:**
- MFA succeeded
- Device was managed
- `IsCompliant: False`

**Finding:** Conditional Access required a compliant device.

**Next check:** Determine why the device was marked noncompliant.

---

## Ticket 3 — Invalid Credentials

**Result:** Failed

**Evidence:**
- Conditional Access not applied
- Invalid username or password

**Finding:** Credential failure rather than MFA or Conditional Access.

**Next check:** Verify username and credentials being used.

---

## Ticket 4 — Untrusted Location

**Result:** Failed

**Evidence:**
- MFA succeeded
- Conditional Access failed
- Policy blocked untrusted locations
- Location was unknown

**Finding:** Access was blocked because the sign-in did not originate from a trusted location.

**Next check:** Review approved locations and source IP/location.

---

## Ticket 5 — High-Risk Sign-In

**Result:** Failed

**Evidence:**
- MFA succeeded
- Device compliant
- Risk level: high
- Policy blocks high-risk sign-ins

**Finding:** High sign-in risk triggered a blocking Conditional Access policy.

**Next check:** Determine why the sign-in was classified as high risk.

---

## Ticket 6 — Administrative Role Requirement

**Result:** Failed for Azure management access

**Evidence:**
- MFA succeeded
- Device compliant
- User role: Helpdesk Administrator
- Required role was more privileged

**Finding:** Authentication succeeded but authorization requirements were not met.

**Next check:** Verify whether the user should have the required role.

---

## Ticket 7 — Enterprise Application Assignment

**Result:** Failed

**Evidence:**
- MFA succeeded
- Conditional Access succeeded
- Assignment required
- User lacked application role

**Finding:** Application authorization failure.

**Next check:** Verify which application role the user should have.

---

## Ticket 8 — Guest Tenant Access

**Result:** Failed

**Evidence:**
- Home tenant: VendorCo
- Resource tenant: Contoso
- Guest account status: NotFound

**Finding:** The external identity existed, but no matching guest account existed in the resource tenant.

**Next check:** Verify guest invitation/provisioning and account identity.

---

## Ticket 9 — Corporate Network Requirement

**Result:** Failed

**Evidence:**
- MFA succeeded
- Device compliant
- Named location did not match
- Policy blocked access outside corporate network

**Finding:** Network location caused Conditional Access failure.

**Next check:** Review allowed named locations and the user's current network.

---

## Ticket 10 — Authentication Strength

**Result:** Failed

**Evidence:**
- MFA succeeded
- Required: phishing-resistant MFA
- Used: SMS

**Finding:** MFA occurred, but the authentication method was not strong enough for the policy.

**Next check:** Determine which allowed authentication method satisfies the required strength.

---

## Ticket 11 — Sign-In Frequency

**Result:** Session required reauthentication

**Evidence:**
- Initial sign-in succeeded
- Refresh token became invalid
- Policy required reauthentication every 4 hours
- Session age exceeded 4 hours

**Finding:** Sign-in frequency policy forced reauthentication.

**Next check:** User reauthenticates.

---

## Ticket 12 — Inactive Refresh Token

**Result:** Desktop failed; mobile succeeded

**Evidence:**
- Desktop token had not been used for 92 days
- Mobile token was 6 days old

**Finding:** Desktop refresh token expired due to inactivity.

**Next check:** Reauthenticate on desktop to obtain a new token.

---

## Ticket 13 — Resource Authorization

**Result:** Dashboard access denied

**Evidence:**
- Sign-in succeeded
- MFA succeeded
- Conditional Access succeeded
- User role: Standard User
- Required role: Reporting Administrator

**Finding:** Authentication succeeded, but the user was not authorized for the requested resource.

**Next check:** Verify whether the user should receive the required role.
