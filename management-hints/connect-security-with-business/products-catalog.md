---
description: Control your products and have all important info in one place
---

# Products catalog

## Products catalog

\*\*\*\*[**FULL TABLE**](https://www.notion.so/whitespots/66465a720f684c7c89914929271614cb?v=a0091105c9384a29be412cf9a388c8f4) **\[LINK\] \(Highly recommend for comfortable reading\)**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Services in use</th>
      <th style="text-align:left">Security controls</th>
      <th style="text-align:center">WRT</th>
      <th style="text-align:center">Business crititcality</th>
      <th style="text-align:left">Risks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Great site</td>
      <td style="text-align:left">
        <ul>
          <li>API</li>
          <li>WEB</li>
          <li>DB</li>
          <li>MOBILE</li>
          <li>LDAP</li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li>SAST</li>
          <li>DAST</li>
          <li>Dep Checker</li>
          <li>ASVS</li>
        </ul>
      </td>
      <td style="text-align:center">65</td>
      <td style="text-align:center">90%</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>Losing money on SMS</li>
          <li>Client can change the contest rules</li>
          <li>...</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
You will learn, how to fill the "**Risks**" column from [here](risks-analysis.md)
{% endhint %}

{% hint style="info" %}
WRT \(Weighed Risk Trend\) is the OWASP metric, which you can use for bugs only. **Do not try to measure security controls** in this way
{% endhint %}

## WRT calculation

After you have discussed all business risks and bug severities, you can transform them to numbers \(weights\).

| Severity | Weight |
| :--- | :--- |
| Critical | 10 |
| High | 5 |
| Medium | 2 |
| Low | 1 |

## Calculation logic

All we need is just to sum all bugs severities and multiply by business criticality.

```text
WRT = ( (BugN * Severity) + (BugN+1 * Severity) ).... * Business criticality
```

Let's say we have the "great site" product with **stored XSS**, **SQLi** and **Account takeover via Open Redirect**.

```text
WRT = ( (XSS) + (SQLi) + (?) ) * Business criticality
```

If we have a non-typical vulnerability, we must set it's severity by using our special page  
From there we get High priority for our Account takeover

```text
WRT = ( 5 + 10 + 5 ) * 0.9 = 18
```

## How to work with WRT

### CEO

Must set the risk-appetite, based on business risks

**Example**

* Any test service DoS **\(5 bugs allowed\) \(medium\)**
* Any technical data disclosure \(version of servers, test scripts, unused plugins\) **\(5 bugs allowed\) \(low\)**

The target **initial \(can be changed\)** risk-appetite will be :

\(5 \* 2 + 5 \* 1\) \* 100% = 15

So, nobody can exceed this value from now.

All exceeded values should be immediately reported to CEO.

### Product owners

Keep track of WRT and try to keep as low, as possible.

### Security

Implement security assessment processes

## Have questions?

**Website**: [whitespots.io](https://whitespots.io/?utm=appsecwiki)   
**Email**: [sales@whitespots.io](mailto:sales@whitespots.io)

