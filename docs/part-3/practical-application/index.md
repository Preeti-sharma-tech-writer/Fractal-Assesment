# `mart_attribution_touchpoints_v1`

## Overview

`mart_attribution_touchpoints_v1` stores recorded Facebook and Google ad clicks and connects them to users. Analysts can use these touchpoints to determine which marketing interaction receives credit when a user completes a desired action.

A touchpoint is any recorded interaction between a potential customer and a marketing channel.

## Business context

The table supports analysis of customer journeys across Facebook and Google advertising. For example, a customer may click a Facebook ad, click a Google ad three days later, and then register on the website. The two clicks are separate touchpoints. The selected attribution model determines how credit for the registration is distributed between them.

| Sequence | Interaction |
| --- | --- |
| 1 | The customer clicks a Facebook ad. |
| 2 | The customer clicks a Google ad three days later. |
| 3 | The customer registers on the website. |

## Ownership and support

Contact Sarah in Operations before using the `linear` attribution model.

The data owner and support route are not specified. See [Confirm with PM](#confirm-with-pm).

## Technical metadata

| Attribute | Value |
| --- | --- |
| Table | `mart_attribution_touchpoints_v1` |
| Data included | Facebook and Google ad clicks |
| Refresh schedule | Hourly |

New or changed click and matching data may take up to approximately one hour to appear. The table is not a real-time data source.

## Data dictionary

| Field | Description | Accepted values |
| --- | --- | --- |
| `attribution_model` | Identifies the rule used to assign conversion credit across recorded marketing touchpoints. | `'first_touch'`, `'last_touch'`, `'linear'` |

The exact field names for the user identifier and IP address are not specified. See [Confirm with PM](#confirm-with-pm).

## Business rules and filters

### Touchpoint matching

The system attempts to associate each Facebook or Google click with a known customer by using a unique user identifier. Clicks associated with the same user identifier can be connected as part of the same marketing journey.

If the user identifier is `NULL`, the system uses the device's IP address as a secondary matching signal.

<aside class="callout callout--caution" role="note">
  <div class="callout__title">
    <img class="callout__icon" src="/icons/triangle-exclamation.svg" alt="" aria-hidden="true">
    <strong>Caution</strong>
  </div>
  <p>IP address matching can connect a click to the wrong user, fail to connect interactions from the same user, or combine activity from multiple users. Review results that rely on the IP address fallback before using them for analysis.</p>
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
| `'last_touch'` | Assigns all credit to the final recorded interaction before conversion. | Which channel most directly preceded the conversion? |
| `'linear'` | Divides credit equally among all qualifying touchpoints. | How can credit be shared across all recorded interactions in the journey? |

<aside class="callout callout--beta" role="note">
  <div class="callout__title">
    <img class="callout__icon" src="/icons/flask.svg" alt="" aria-hidden="true">
    <strong>Beta</strong>
  </div>
  <p>The <code>'linear'</code> attribution model is in beta testing. Do not use it for official reporting unless Sarah in Operations approves its use.</p>
</aside>

## Dependencies

The table depends on recorded Facebook and Google click data and on the matching information used to associate clicks with users. Other upstream and downstream dependencies are not specified. See [Confirm with PM](#confirm-with-pm).

## Caveats

- IP address matching may produce inaccurate user associations.
- The `linear` attribution model is in beta testing and requires approval before use for official reporting.
- The table refreshes hourly and should not be treated as a real-time data source.

## Usage example

For a journey containing one Facebook touchpoint followed by one Google touchpoint and a website registration, credit is assigned as follows:

| Attribution model | Facebook credit | Google credit |
| --- | ---: | ---: |
| `'first_touch'` | 100% | 0% |
| `'last_touch'` | 0% | 100% |
| `'linear'` | 50% | 50% |

If a journey contains four qualifying touchpoints, the `'linear'` model assigns 25% credit to each touchpoint.

## Update log

| Date | Version | Change | Customer impact | Author or approver |
| --- | --- | --- | --- | --- |
| 2026-08-23 | V1 | [First Draft Creation] | 'No impact` | Preeti |



