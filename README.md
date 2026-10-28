# pv-task-2-medical-coding
# PV Task 2: Medical Coding and Narrative Quality

Source: `pv-case-intake-sample.csv` (4 cases, all for the product Velunex).
Coded table: [`coded_cases.csv`](coded_cases.csv)

## 1. Normalization rules applied

| Field | Rule |
|---|---|
| Product | Kept as reported ("Velunex"). Active ingredient was not supplied, so I did not map it to a generic name or a WHODrug entry. |
| Dose / route / indication | None supplied in any case, so recorded as "Not reported" (nothing inferred). |
| Age / sex | Number + unit ("34 years"); F/M/U expanded to Female/Male/Unknown. Missing age = "Not reported". |
| Country | ISO code expanded (IN = India, GB = United Kingdom). |
| Onset | Kept as a time-to-onset latency (hours/days/weeks). No calendar dates were supplied, so none were created. |
| Outcome | Standard wording: Recovered/Resolved, Recovering/Resolving. |
| Seriousness | Serious only when the source states a seriousness criterion (hospitalisation). |

## 2. Event coding (MedDRA Preferred Terms)

| Case | Reported term | Coded PT | Reason |
|---|---|---|---|
| PV-101 | Nausea | Nausea | Exact match. |
| PV-102 | Loss of consciousness | Loss of consciousness | Exact match. Not coded as syncope, because the reporter gave no such diagnosis. |
| PV-103 | Mild rash | Rash | "Mild" is severity, not part of the medical concept, so it is dropped from the PT and kept in the verbatim. |
| PV-104 | Appendicitis | Appendicitis | Exact match. |

PTs are my best match from MedDRA knowledge. I did not have the MedDRA browser available, so please confirm the LLT/PT and the version in the browser before final submission.

## 3. Narratives (supplied facts only)

**PV-101.** A 34-year-old female patient in India experienced nausea 3 hours after use of Velunex. The dose, route, indication and start date were not reported. No concomitant medication was reported. The event was assessed as not serious. The patient recovered. Action taken with Velunex was not reported.

**PV-102.** A 61-year-old male patient in India experienced loss of consciousness 2 days after use of Velunex. The dose, route, indication and start date were not reported. Concomitant information was unknown. The patient was admitted to hospital as an emergency, and the event was considered serious (hospitalisation). At the time of reporting the patient was recovering. Action taken with Velunex was not reported.

**PV-103.** A 27-year-old female patient in the United Kingdom developed a mild rash 4 days after use of Velunex. The dose, route, indication and start date were not reported. No rechallenge was performed. Concomitant medication was not reported. The event was assessed as not serious. The patient recovered. Action taken with Velunex was not reported.

**PV-104.** A patient in India, whose age was not reported and whose sex was unknown, was diagnosed with appendicitis 3 weeks after use of Velunex. The dose, route, indication and start date were not reported. Medical history was incomplete. The patient was hospitalised, and the event was considered serious (hospitalisation). The patient recovered. Action taken with Velunex was not reported.

## 4. Short explanation and data-quality flags

I normalized each field with fixed rules, coded each event to one MedDRA PT per medical concept, and wrote narratives in chronological order using only supplied facts, writing "not reported" for gaps instead of guessing. Items to query with the reporter:

- All cases lack dose, route, indication, start/stop dates and action taken with Velunex.
- PV-102: concomitant drugs and medical history are unknown. Cause of the loss of consciousness is not given.
- PV-103: "No rechallenge" sat in the concomitant column. I treated it as rechallenge information, not a concomitant drug.
- PV-104: age, sex and history are missing. A 3-week latency is long for an acute event, so it is unclear whether it counts from first or last dose, and the reporter's causality view is absent. I made no causality assessment, since none was supplied.
