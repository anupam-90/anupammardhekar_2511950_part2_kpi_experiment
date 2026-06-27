# Hypothesis Testing: Onboarding & Activation Campaign

## Experiment Overview
The goal is to determine if the Treatment group (new onboarding experience) yields a statistically significant increase in the conversion rate compared to the Control group, without violating guardrail metrics.

## Hypotheses

### Null Hypothesis ($H_0$)
The new onboarding campaign has no effect on the conversion rate ($p_{treatment} = p_{control}$). There is no difference in conversion between the Control and Treatment groups.

### Alternate Hypothesis ($H_a$)
The new onboarding campaign increases the conversion rate ($p_{treatment} > p_{control}$). The Treatment group exhibits a statistically significant higher conversion rate compared to the Control group.

---

## Statistical Design

| Parameter | Specification |
| :--- | :--- |
| **Test Type** | One-tailed Z-test (for proportions) |
| **Significance Level ($ lpha$)** | 0.05 |
| **Metric Being Tested** | Conversion Rate (`converted_to_paid`) |

---

## Reasoning

### Why this metric?
The conversion rate is our **North Star metric**. As defined in the project scope, the primary business decision hinges on whether the new onboarding experience effectively drives users to pay. Testing this specific metric directly answers the leadership's inquiry regarding campaign launch viability.

### Interpretation Logic
* **If $p$-value < 0.05:** We reject the Null Hypothesis. We conclude that the campaign has a statistically significant positive impact on conversion.
* **Guardrail Assessment:** Even if the conversion test is significant, we will recommend *not* launching the campaign if the guardrail metrics (support tickets and refunds) show a statistically significant degradation, as this would indicate low-quality acquisition.

## Connection to Business Decision
The business outcome depends on balancing growth (conversion) with quality (guardrail stability). 

* If $H_a$ is supported and guardrails remain stable, the recommendation will be to proceed with a full rollout.
* If the test fails, we will suggest further iteration on the onboarding flow.
