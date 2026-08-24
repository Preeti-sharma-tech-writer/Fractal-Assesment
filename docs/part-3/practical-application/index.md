# `mart_attribution_touchpoints_v1`

## Overview

`mart_attribution_touchpoints_v1` stores Facebook and Google ad clicks and connects them to users. Analysts can use the table to determine which marketing interaction receives credit when a user completes an action, such as registering, requesting a demo, or making a purchase.

A touchpoint is any recorded interaction between a potential customer and a marketing channel.

## Business context

A customer may interact with multiple marketing channels before completing an action. Each interaction is stored as a separate touchpoint. The selected attribution model determines how credit is distributed across those touchpoints.

For example:

| Sequence | Interaction |
| --- | --- |
| 1 | The customer clicks a Facebook ad. |
| 2 | The customer clicks a Google ad three days later. |
| 3 | The customer registers on the website. |

The Facebook and Google clicks are two separate touchpoints in this journey.

## Technical metadata

| Attribute | Value |
| --- | --- |
| Table | `mart_attribution_touchpoints_v1` |
| Data included | Facebook and Google ad clicks |
| Refresh schedule | Hourly |

New or changed click and matching data may take up to one hour to appear. The table is not a real-time data source.

## Data dictionary

| Field | Description | Accepted values |
| --- | --- | --- |
| `attribution_model` | Identifies the rule used to assign credit across a user's recorded marketing touchpoints. | `'first_touch'`, `'last_touch'`, `'linear'` |

## Business rules and filters

### Touchpoint matching

The system attempts to associate each Facebook or Google click with a known customer by using a unique user identifier. Clicks connected to the same identifier can be combined to reconstruct the customer's marketing journey.

If the user identifier is `NULL`, the system uses the device's IP address as a secondary matching signal.

<aside class="callout callout--caution" role="note">
  <div class="callout__title">
    <img class="callout__icon" src="/icons/triangle-exclamation.svg" alt="" aria-hidden="true">
    <strong>Caution</strong>
  </div>
  <p>IP address matching can connect a click to the wrong user, fail to connect interactions from the same user, or combine activity from multiple users. Interpret results that rely on IP address matching carefully.</p>
</aside>

IP address matching can be inaccurate because:

- Several people may use the same office, household, or public Wi-Fi network.
- A user's IP address may change between interactions.
- Virtual private networks and mobile networks may mask or regularly change IP addresses.
- Different devices may share one public IP address.

Matching by a stable user identifier is deterministic. Matching by an IP address is probabilistic or inferred.

### Attribution models

| Value | Credit assignment | Question answered |
| --- | --- | --- |
| `'first_touch'` | Assigns all credit to the first recorded interaction. | Which channel originally brought the customer into the journey? |
| `'last_touch'` | Assigns all credit to the final recorded interaction before the customer completes an action. | Which channel most directly preceded the action? |
| `'linear'` | Divides credit equally among all qualifying touchpoints. | How can credit be shared across all recorded interactions in the journey? |

<aside class="callout callout--beta" role="note">
  <div class="callout__title">
    <img class="callout__icon" src="/icons/flask.svg" alt="" aria-hidden="true">
    <strong>Beta</strong>
  </div>
  <p>The <code>'linear'</code> attribution model is in beta testing. Do not use it for official reporting.</p>
</aside>

## Caveats

- IP address matching may produce inaccurate user associations.
- The `'linear'` attribution model is in beta testing and is not approved for official reporting.
- The table refreshes hourly and should not be treated as a real-time data source.

## Usage example

For a journey with one Facebook touchpoint followed by one Google touchpoint and a website registration, the models distribute credit as follows:

| Attribution model | Facebook credit | Google credit |
| --- | ---: | ---: |
| `'first_touch'` | 100% | 0% |
| `'last_touch'` | 0% | 100% |
| `'linear'` | 50% | 50% |



## Update log

| Date | Version | Change | Customer impact | Author or approver |
| --- | --- | --- | --- | --- |
| 2026-08-23 | V1 | [First Draft Creation] | 'No impact` | Preeti |



