# Event Correlation #

### 1. Create Wehook ###

Doc Ref: https://www.ibm.com/docs/en/cloud-paks/cloud-pak-aiops/4.11.0?topic=integrations-generic-webhook 

For Webhook creation follow the steps mentioned in the [Lab](https://ibm.github.io/waiops-tech-jam/labs/cloud-pak-aiops/alert-lab/webhook-integration/#41-creating-a-webhook-integration)
Use JSONATA to map the incoming JSON payload to the IBM Cloud Pak for AIOps event data schema and configure Webhook for ingesting events (due to custom integration).


### 2. Ingest Events/Alerts ###

POST event and alerts to the webhook created and verify the grouping of alerts, going to **Alert Viewer**.

Ref: [Validate Topological Correlation Lab](https://ibm.github.io/waiops-tech-jam/labs/cloud-pak-aiops/topology-lab/topology-applications/#validating-topological-correlation)


### 3. Create policy to promote alerts to incidents ###

In order to create actionable incidents from alerts to improve insights into your issue, create relevant policies.

Ref: https://www.ibm.com/docs/en/cloud-paks/cloud-pak-aiops/4.11.0?topic=policies-promote-alerts-incident 
