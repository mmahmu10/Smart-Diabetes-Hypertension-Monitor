
# EMS-to-Hospital FHIR Handoff

## Purpose
This application helps emergency department clinicians review
prehospital EMS assessments and working diagnoses.

## FHIR Version
FHIR R4

## Resources
- Patient: fictional patient demographics
- Encounter: EMS prehospital call
- Condition: EMS provisional diagnosis
- ClinicalImpression: EMS assessment and reasoning
- Encounter: hospital emergency visit
- Condition: hospital diagnosis

## Workflow
1. EMS evaluates the patient.
2. EMS creates a prehospital Encounter.
3. EMS records a provisional Condition.
4. EMS documents a ClinicalImpression.
5. Hospital creates its own Encounter.
6. Hospital Encounter references the EMS Condition.
7. Hospital records its own Condition.

All patient information is synthetic.



# SMART Patient App

A build-free teaching scaffold for GitHub Pages. The HTML comments mark the future SMART authorization and callback steps. All pages serve static content.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | App home and future OAuth redirect target with a commented `FHIR.oauth2.ready()` stub. |
| `launch.html` | Future launch entry point with a commented `FHIR.oauth2.authorize()` stub. |
| `health.html` | Static hosting smoke check. |
| `.nojekyll` | Serves the files as-is on GitHub Pages. |
| `README.md` | Publishing instructions and the launch comparison. |

## Publish and verify

1. Put these files, including `.nojekyll`, at the root of a GitHub project repository and push them to `main`.
2. In **Settings → Pages → Build and deployment**, select **Deploy from a branch**, then **main** and **/(root)**. Save.
3. After deployment, replace the placeholders with the GitHub owner and repository name. Open the app, follow **Health check**, and confirm it displays “OK. Static hosting is working.” Open **Launch stub** and confirm it displays the placeholder page.

| Page | Default GitHub Pages URL |
| --- | --- |
| App and future OAuth redirect target | `https://<owner>.github.io/<repo>/` |
| Health check | `https://<owner>.github.io/<repo>/health.html` |
| Future SMART launch entry point | `https://<owner>.github.io/<repo>/launch.html` |

These URLs assume a project site with the default domain. A repository named `<owner>.github.io` publishes at `https://<owner>.github.io/`, with the file paths directly under that root. [GitHub Pages setup](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

## Patient vs Provider launch

In the patient-facing standalone example, the patient opens the app directly. The app starts with a configured FHIR server and requests patient context with `launch/patient` during authorization. In the provider-facing EHR example, the clinician opens the app from an existing EHR session. The EHR sends `iss` (the FHIR server URL) and `launch` (an opaque handle), and the app passes the handle back during authorization so the server can supply context such as the active patient or encounter. Standalone and EHR describe where the launch starts. Patient and provider describe who uses the app. [HL7 SMART App Launch](https://hl7.org/fhir/smart-app-launch/app-launch.html)
