# Challenge-09 - Deploy and demonstrate the consent capabilities of Azure API for FHIR

## Introduction

Welcome to Challenge-09!

In this challenge you will learn how to configure Consent Opt-Out filtering using the FHIR-Proxy (OSS) solution.

## Background

In today's rapidly changing healthcare data landscape, the FHIR R4 format is has become the HLS industry standard for storage and exchange of health data. Healthcare consumers expect that their directives related to privacy, treatment, research, and advanced care are respected.

## Learning Objectives for Challenge-09

+ Configure Consent Opt-Out filtering in FHIR-Proxy
+ Add a Consent Resource to the Healthcare APIs FHIR Service
+ Verify that Consent Opt-Out filtering performs as expected

## Prerequisites

+ Azure Healthcare APIs FHIR service instance with patient data
+ FHIR-Proxy successfully deployed
+ Postman (https://www.postman.com/downloads/) or Visual Studio Code with the REST Client extension (https://marketplace.visualstudio.com/items?itemName=humao.rest-client)
+ Multiple Azure AD users to simulate user and or administrator access to the FHIR service. 

## Step - 1 Configure Postman

1. Configure postman using the guidance provided in [Challenge 1](<../Challenge-01 - Deploy Azure API for FHIR (PaaS), FHIR-Proxy (OSS), and FHIR-Bulk Loader (OSS)/Readme.md>).
2. Confirm that the FHIR service contains Patient resources.
![Patient Resources](./images/patient-count-postman.png)
3. Select a Patient resource and record the patient identifier. This will be used to create the Consent resource.

Visual Studio Code with the [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) extension may also be used to complete this challenge. See the walkthrough [here](https://docs.microsoft.com/en-us/azure/healthcare-apis/using-rest-client) for details on how to use REST Client to access Azure Healthcare APIs. Be sure to note that in all cases you will be using the FHIR-Proxy endpoint to complete this challenge.

## Step - 2 Post Consent Record to FHIR Service

1. Review and update (as needed) the sample Consent resource, which may be found [here](./sample-data/consent-resource.json). Be sure to use the Patient resource obtained in Step 1.
2. Create a new request in Postman and post the consent resource.

## Step - 3 Configure Secure FHIR Consent Opt-Out

1. Refer to the FHIR-Proxy configuration [documentation](https://github.com/microsoft/fhir-proxy/blob/main/docs/configuration.md) for additional details.
2. [Configure the Consent Opt Filter](https://github.com/microsoft/fhir-proxy/blob/main/docs/configuration.md). The FP-POST-PROCESSOR-TYPES must be updated to include FHIRProxy.postprocessors.ConsentOptOutFilter.
3. Additionally the FP-MOD-CONSENT-OPTOUT-CATEGORY setting with a value of `http://loinc.org|59284-0` must be added if it does not exist.

## Step - 3 Verify Consent Opt-Out filtering

1. Link a user to an appropriate FHIR resource. See the FHIR-Proxy configuration [documentation](https://github.com/microsoft/fhir-proxy/blob/main/docs/configuration.md) for additional details. Ensure that the linked user is not assigned to the FHIR-Proxy administrator role.

2. Sample query patient result.![Query patient](./images/ConsentOptOut-Withheld-2.png) 


## What does success look like for Challenge-09?

+ Successfully POST a consent record to the Azure Healthcare APIs FHIR service
+ Verify that Consent Opt-Out properly filters resources

## Next Steps

Click [here](<../Challenge-10 - FhirBlaze (Blazor app dev + FHIR)/ReadMe.md>) to proceed to the next challenge.