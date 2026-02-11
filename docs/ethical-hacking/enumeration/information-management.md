# Information management

A data reconnaissance/enumeration phase only adds value if its results are properly managed, standardized, and documented. Traceability and the quality of the evidence facilitate prioritization, reproducibility of tests, and the preparation of the technical report.

!!! note "Note"

    The following recommendations are primarily aimed at large-scale professional audits, where evidence management and traceability are critical. In laboratory environments or training exercises, a simplified version of this process can be applied, adapted to the size and objectives of the practice.

## Evidence repository structure

It is recommended to organize a repository (local/encrypted or collaborative platform)
with the following folder and file structure:

```
/evidences
 /raw_outputs    # original files (nmap.xml, ffuf.json, amass.txt)
 /screenshots    # screenshots with timestamps
 /notes          # daily notes / operational log (markdown)
 /reports        # drafts and templates
 /artifacts      # downloaded files (docs, config)
 inventory.csv   # normalized asset inventory
 findings.json   # structured findings
 README.md
```

## Finding report template

* **ID:** FIND-xxx
* **Title:** Brief and clear.
* **Description:** What was found and why it matters.
* **Asset:** Host/domain/IP/service.
* **Evidence:** Commands, outputs, and screenshots (with paths).
* **Impact:** Confidentiality / Integrity / Availability.
* **Reproduction:** Minimum steps to validate (command + parameters).
* **Recommendation:** Concrete and prioritized measures (quick wins + plan).
* **Severity/Confidence:** Agreed scale (e.g., Critical/High/Med/Low) + % confidence.