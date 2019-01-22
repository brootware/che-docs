## Release summary

Eclipse Che 6.16 includes:

* **Prometheus and Grafana deployed in the Helm chart**: Allowing to collect and inspect metrics emitted by the Che server
* **Upgrade of Tomcat & CORS Configuration**: Changes to default CORS configuration and providing more configuration options

## Upgrading

Instructions on how to upgrade.

## Release details

### Prometheus and Grafana deployed in the Helm chart
As part of our ongoing work to ensure that Eclipse Che is easier to monitor and trace, we have been
adding a number of metrics which are tracked since the 6.15.0 release. To make it easier for Che 
admins to visualize these metrics, a Helm deployment of Eclipse Che now also deploys a Prometheus 
server which gathers metrics from Che, and Grafana, a popular visualization project, pre-configured 
with a sample dashboard to visualize these metrics.

To try it out, install Che's Helm chart with `--set global.metricsEnabled=true`. 

### Upgrading Tomcat & CORS configuration (https://github.com/eclipse/che/pull/12144)

In this release, Tomcat  will be upgraded to newest version 8.5.35, alongisde our CORS configuration to be compatible with it.
CORS filters are present in Che to allow requests with origins, that can be different from the origin that the client is loaded on (For example, GWT IDE executing requests from browser to WS Agent, with origin belonging to WS Master domain)

While CORS filter on WS Master would remain, we will also add some more configuration variables to Configure CORS for WS Agent, so it would as flexible in configuraion, as WS Master.

Here is what CORS settings will look like in Che 6.16 by default:

WS Master:

"cors.support.credentials" - "false"
"cors.allowed.origins" - "*"

WS Agent:

"cors.support.credentials" - true
"cors.allowed.origins" - <domain of ws master, will be provided automatically based on CHE_API variable>

Here is the full list of environment variables that will be available in Che 6.16 for overriding of default configuration for CORS on WS Master and WS Agent: 

* `CHE_CORS_ENABLED` = Enabling CORS Filter on WS Master. On by default
* `CHE_CORS_ALLOWED_ORIGINS` = List of allowed origins in requests to WS Master. Default is "*".
* `CHE_CORS_ALLOW_CREDENTIALS` = Allowing requests with credentials to WS Master. Default is "false".

* `CHE_WSAGENT_CORS_ENABLED` = Enabling CORS Filter on WS Agent. 
* `CHE_WSAGENT_CORS_ALLOWED__ORIGINS` = List of allowed origins in requests to WS Agent. If not set, or set to "null", value will be evaluated from CHE_API variable at runtime.
* `CHE_WSAGENT_CORS_ALLOW__CREDENTIALS` = Allowing requests with credentials to WS Agent. Default is "true".

PR with changes introduced in 6.16: https://github.com/eclipse/che/pull/12144

### Feature 2 (#ISSUE)

Feature description focusing on value to the user or contributor.

Learn more in the documentation: [Link to the documentation](<URL>).

## Other notable enhancements

* Issue title. (#ISSUE)

## Notable bug fixes

* Fixed issue’s title. (#ISSUE)

## Community, Thank You!

We’d like to say a big thank you to everyone who helped to make Che even better:

* [Contributor Name](<PROFILE_URL>) – [Company Name](<COMPANY_URL>) – (#PR): [PR Title](<PR_URL>)