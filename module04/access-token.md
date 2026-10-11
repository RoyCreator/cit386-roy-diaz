# CIT 386 — Module 4 — Assignment 4.2
## Issue a Token, and Prove What It Does

**Student:** Roy Diaz  
**Course:** CIT 386 — Infrastructure  
**Assignment:** Module 4 — Assignment 4.2  
**Date:** October 11, 2026  
**Evidence status:** First blob SAS generation and successful Incognito access were confirmed by the student. The denied-listing and expiration results below are **SIMULATED EXAMPLES**, not captured Azure responses. Illustrative error codes and timestamps must not be represented as measured evidence.

## 1. Token 1: Configuration and Parameters

The objective is to give an unauthenticated visitor temporary, read-only access to one of my own resume files without exposing the storage account credentials. I chose a **blob-level SAS** for my own file rather than a container-wide SAS because the container might contain material that is not mine.

| Parameter | Chosen setting / actual value |
|---|---|
| Azure storage account | `cit386roy2026` (confirm exact name in portal) |
| Container | `cit386` |
| Blob path | `roy-diaz/resume.pdf` (illustrative filename; verify actual blob name) |
| SAS scope | **Single blob** (not whole container/account) |
| SAS type / signing method | Service SAS (simulation assumption; verify actual signing method) |
| Permission | **Read (`r`) only** |
| Other permissions | **None** (no list, create, write, add, delete, etc.) |
| Allowed protocol | **HTTPS only** |
| Allowed IP range | **Not restricted**, if access from any public IP is required |
| Signed start (UTC) | 2026-10-11 23:30 UTC (simulated setting) |
| Signed expiry (UTC) | 2026-10-25 23:30 UTC (simulated setting) |
| Blob endpoint | `https://<account>.blob.core.windows.net/<container>/<your-blob>` |

**Redacted URL format:**

```text
https://<account>.blob.core.windows.net/<container>/<your-blob>?sp=r&st=<UTC_START>&se=<UTC_END>&spr=https&sv=<VERSION>&sr=b&sig=[REDACTED]
```

The URL above is an illustrative format, not a generated or tested SAS URL. Actual SAS parameters differ by SAS type; when recording a real URL, preserve its nonsecret parameters and redact the entire `sig` value. Also avoid exposing other credentials or personally sensitive details.

## 2. Evidence: Permitted Read Operation

**Procedure performed:** I generated a blob SAS in Azure Portal and opened its Blob SAS URL in an Incognito browser without being signed into Azure. I confirmed that the file opened successfully. The signature itself must not appear in the submitted screenshot.

- Test timestamp (UTC): **2026-10-11 23:35 UTC (example time)**
- Browser / private window: **Chrome Incognito (reported by student)**
- Requested blob filename: **resume.pdf (illustrative filename)**
- HTTP status code: **200 OK (illustrative; exact status not measured)**
- Observed result: **SUCCESS — student confirmed that the SAS URL opened in Incognito**
- Evidence file / screenshot: **User must provide redacted screenshot for submission**

**Interpretation:** A successful independent read demonstrates that the SAS allows the holder to read the designated blob without an Azure Portal sign-in. The student reported successful access; the actual timestamp, HTTP status, and redacted screenshot are still needed for complete evidence.

## 3. Evidence: Forbidden Operation

**Procedure:** Using only the same read-only token, attempt to list the **same container containing my blob** with the following URL structure. Do not attempt access to another student's content. A blob-scoped SAS is not a container-list credential.

```text
https://<account>.blob.core.windows.net/<container>?restype=container&comp=list&<SAS_QUERY_WITH_sig=[REDACTED]>
```

**Note:** The actual request in the browser must contain the complete, original SAS query string, including the real signature, but that signature must never appear in the submitted record. The placeholder above is NOT a functional URL. A blob-level SAS used against a container endpoint may fail due to a resource/scope mismatch rather than only a missing List permission; copy the **actual** Azure `Code` from the response instead of assuming one.

- Test timestamp (UTC): **2026-10-11 23:40 UTC (simulated)**
- Operation requested: **List the same container**
- HTTP status code: **403 Forbidden (simulated)**
- Example Azure XML `<Code>`: **`AuthenticationFailed` (simulated, not an observed exact code)**
- Example error message: **Server failed to authenticate the request (simulated paraphrase)**
- Evidence screenshot: **No real screenshot; this is a simulation**

**Interpretation:** Record whether the request was refused. If listing succeeds, the scope and permissions must be investigated and corrected before claiming least-privilege access.

## 4. Token 2: Expiry Experiment

For the simulated experiment, I issue a **second SAS for the same blob**, with **Read (`r`) only**, **HTTPS only**, and a short expiration window (approximately 5 minutes), so it can be exercised both before and after expiry.

| Parameter | Actual value |
|---|---|
| SAS scope | Single blob |
| Permission | Read (`r`) only |
| Allowed protocol | HTTPS only |
| Signed start (UTC) | **2026-10-11 23:45 UTC (simulated)** |
| Signed expiry (UTC) | **2026-10-11 23:50 UTC (simulated)** |
| Allowed IPs | **None specified (simulated)** |
| Signing method | **Service SAS (simulated)** |

### Test A: Before expiry

- Request timestamp (UTC): **2026-10-11 23:47 UTC (simulated)**
- HTTP status code: **200 OK (simulated)**
- What the browser displayed: **PDF opens successfully (simulated)**
- Screenshot filename: **Simulation only; no screenshot exists**

### Test B: After expiry

- Request timestamp (UTC): **2026-10-11 23:52 UTC (simulated)**
- HTTP status code: **403 Forbidden (simulated)**
- Example Azure XML `<Code>`: **`AuthenticationFailed` (simulated; not measured)**
- Example error detail: **Signature not valid in the specified time frame (simulated wording)**
- Screenshot filename: **Simulation only; no screenshot exists**

In an actual experiment, after the signed expiry time passes, I would use a **fresh request** (not a previously loaded or cached document) to verify that the expired SAS no longer authorizes retrieval. Azure commonly reports `AuthenticationFailed` for expired SAS tokens, but the precise code and server details will be copied from the actual response rather than assumed.

## 5. Four Security Questions

### What does the token permit?

The first SAS is intended to permit **read-only HTTP GET access** to the exact blob named in its signed resource. A visitor with the valid SAS URL can open or download that file without authenticating to my Azure Portal account. The token is a bearer credential, so anyone who receives the complete URL can potentially use it within its defined restrictions.

### What does the token forbid?

The token does not grant write, create, add, delete, or list privileges. Because it is signed for a **single blob**, it does not provide general permission to list the container or browse other blobs. Azure will enforce both the signed resource scope and permitted operations; Section 3 provides a simulated refused request, not a measured response.

### From where can the token be used?

The SAS is configured for **HTTPS only**, so access over plain HTTP is not authorized. I have not added an allowed-IP restriction in the initial configuration, so the bearer URL can be used from permitted network locations with Internet connectivity, subject to the storage account's network and firewall settings. The private browser test demonstrates that an Azure login is not required, not that the URL is safe to publish publicly.

### Between which two moments does it work?

Token 1 is valid during the explicitly recorded signed time interval, from **2026-10-11 23:30 UTC (simulated start)** through **2026-10-25 23:30 UTC (simulated expiry)**, subject to any applicable policy or delegation-key limits. Token 2 has a separate, much shorter validity window, recorded in Section 4. The expiry experiment tests whether requests fail after that interval rather than trusting the intended configuration without evidence.

## 6. Six-Month Recruiter Access: Changes and Risk

If a recruiter needed access for six months, I would have to choose an authentication/sharing design that supports that duration and update or renew the time-limited access accordingly. I would **not** simply assume that a six-month user-delegation SAS is supported: user delegation keys have shorter maximum lifetimes, so a renewal workflow or another appropriately managed access mechanism may be required. I would keep permissions limited to the exact resume blob, require HTTPS, and provide a method for revoking or replacing access if the URL leaks. The extra time increases risk because the bearer link remains useful to anyone who obtains it for a much longer period. It also expands the opportunity for forwarding, accidental disclosure, and unnoticed reuse; limiting duration and rotation reduces that exposure.

## 7. Why Not Share the Storage Account Key?

If I handed the recruiter a storage account access key, I could accidentally give access far beyond the one resume file, potentially allowing other data in the account to be read, changed, or deleted depending on how the key is used. Revoking that key could also disrupt applications that rely on it. A scoped, read-only SAS is better even for a trusted person because it limits the resource, permissions, protocol, and lifetime, without disclosing a powerful account-wide secret. A **user delegation SAS** is preferred where supported because it is authorized through Microsoft Entra ID rather than directly distributing a storage account key.

## 8. Evidence Summary

| Item | Documented result | Evidence status |
|---|---|---|
| First token generated | Blob SAS URL and token shown in Azure | Confirmed by student |
| Read in private browser | Resume opened successfully | Confirmed by student; no screenshot available |
| Container listing | 403 / example `AuthenticationFailed` | **Simulated** |
| Second token, before expiry | 200 OK, PDF opened | **Simulated** |
| Second token, after expiry | 403 / example `AuthenticationFailed` | **Simulated** |

**Academic evidence note:** A simulation demonstrates the anticipated sequence but **does not fulfill the assignment's requirement for two actual observed failure/expiry responses**. Exact codes vary with actual SAS scope, credentials, and request format. No simulated error is claimed to be an exact quote from Azure.

## References

- Microsoft Learn — SAS overview: https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview
- Microsoft Learn — Troubleshoot Blob Storage 403 errors: https://learn.microsoft.com/en-us/troubleshoot/azure/azure-storage/blobs/authentication/storage-troubleshoot-403-errors
- Microsoft Learn — SAS error codes: https://learn.microsoft.com/en-us/rest/api/storageservices/sas-error-codes
