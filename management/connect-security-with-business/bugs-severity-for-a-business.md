---
description: It will help you to connect product owners and security team
---

# Bugs severity for a business

## Requirements

1. Discuss all severities and business impacts with CEO / Head of products   
2. Discuss SLA for all severities with CTO and CEO / Head of products   
3. If you have a bug bounty program, fix all prices in the table below

[**TABLE FULL VIEW**](https://www.notion.so/whitespots/041a2ffb87384ac99f4c59fd9accb959?v=c310685f66bb43cc806d647a3bbbbf7b) **\[ link \] \(Highly recommend for comfortable reading\)**

{% tabs %}
{% tab title="Business impact \(classes\)" %}
<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Severity</b>
      </th>
      <th style="text-align:left">Impact</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Critical</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>Operational or financial damage</li>
          <li>Privacy violation</li>
          <li>Non-compliance (legal issues)</li>
          <li>Reputational damage</li>
          <li>Indirect damage</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">High</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>Operational or financial damage</li>
          <li>Privacy violation</li>
          <li>Non-compliance (legal issues)</li>
          <li>Reputational damage</li>
          <li>Indirect damage</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Medium</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>Operational or financial damage</li>
          <li>Privacy violation</li>
          <li>Non-compliance (legal issues)</li>
          <li>Indirect damage</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Low</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>Privacy violation</li>
          <li>Non-compliance (legal issues)</li>
          <li>Indirect damage</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}

{% tab title="Business impact \(risks\)" %}
<table>
  <thead>
    <tr>
      <th style="text-align:left">Severity</th>
      <th style="text-align:left">Risks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Critical</td>
      <td style="text-align:left">
        <p><b>Catastrophic impact</b>
        </p>
        <ul>
          <li>Losing significant amounts of money</li>
          <li>Sensitive service DoS</li>
          <li>Mass leakage of Personal or Financial data</li>
          <li>Real danger of regulation authority claim or lawsuit</li>
          <li>Primary websites content manipulation</li>
          <li>Critical technical data disclosure (keys, passwords, etc.)</li>
        </ul>
        <p><b>Major impact</b>
        </p>
        <ul>
          <li>Losing any amounts of money</li>
          <li>Sensitive service DoS</li>
          <li>Personal or Financial data significant leakage</li>
          <li>Possibility of regulation authority claim or lawsuit</li>
          <li>Secondary websites content manipulation</li>
          <li>Production technical data disclosure (service configs, logs)</li>
          <li>Critical service misconfigurations</li>
          <li>Critical service security controls issue</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">High</td>
      <td style="text-align:left">
        <p><b>Moderate impact</b>
        </p>
        <ul>
          <li>Any production service DoS</li>
          <li>Personal or Financial data single/several record leakage</li>
          <li>Partial incompliance of regulatory requirements with clear consequences</li>
          <li>Owned by company websites content manipulation</li>
          <li>Sensitive technical data disclosure (traces, any info that should be hidden)</li>
          <li>Any Production service misconfigurations</li>
          <li>Any production service security controls issue</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Medium</td>
      <td style="text-align:left">
        <p><b>Minor impact</b>
        </p>
        <ul>
          <li>Any test service DoS</li>
          <li>Personal or Financial data single/several record leakage</li>
          <li>Owned by company websites content manipulation</li>
          <li>Any regulatory incompliance with unclear or delayed consequences</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Low</td>
      <td style="text-align:left">
        <p><b>Insignificant impact</b>
        </p>
        <ul>
          <li>Any technical data disclosure (version of servers, test scripts, unused
            plugins)</li>
          <li>Any Test service misconfigurations</li>
          <li>Any test service security controls issue</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}

{% tab title="Comment" %}
<table>
  <thead>
    <tr>
      <th style="text-align:left">Severity</th>
      <th style="text-align:left">Comment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Critical</td>
      <td style="text-align:left">
        <p><b>Catastrophic </b>
          <br />Security incident, high likelihood of exploitation, can substantially
          affect business at any moment.</p>
        <p><b>Major <br /></b>Critical issues, which are not affecting business immediately,
          but it&apos;s a real risk of that.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">High</td>
      <td style="text-align:left"><b>High-level</b> issues, which requires timely response. If vulnerability
        will be chained with another, risk can elevate.</td>
    </tr>
    <tr>
      <td style="text-align:left">Medium</td>
      <td style="text-align:left">General security/configuration/best practices issue, which can lead to
        emerging of elevated risk.</td>
    </tr>
    <tr>
      <td style="text-align:left">Low</td>
      <td style="text-align:left">All low risk non-exploitable vulnerabilities, which is &quot;better to
        fix&quot;</td>
    </tr>
  </tbody>
</table>
{% endtab %}

{% tab title="BugBounty" %}
| Severity | Amount \($\) |
| :--- | :--- |
| Critical | 3000 |
| High | 1000 |
| Medium | 500 |
| Low | 100 |
{% endtab %}

{% tab title="SLA" %}
| Severity | Time to fix |
| :--- | :--- |
| Critical | 4 |
| High | 30 |
| Medium | 75 |
| Low | 180 |
{% endtab %}
{% endtabs %}

## Have questions?

**Website**: [whitespots.io](https://whitespots.io/?utm=appsecwiki)   
**Email**: [sales@whitespots.io](mailto:sales@whitespots.io)

