# Emails notifications flow

The table below describes the cases when the email notification is sent depending on user roles and actions performed with visit.  

<table>
  <thead>
    <tr>
      <th style="text-align:left">Actions/Roles</th>
      <th style="text-align:left">
        <p><b>TPM</b>
        </p>
        <p><b> organization</b>
        </p>
      </th>
      <th style="text-align:left"><b>PME</b>
      </th>
      <th style="text-align:left">
        <p><b>TPM </b>
        </p>
        <p><b>Focal point</b>
        </p>
      </th>
      <th style="text-align:left">
        <p><b>UNICEF </b>
        </p>
        <p><b>Focal point</b>
        </p>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Cancellation before Assign</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">by</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Assign</b>
      </td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">by</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Cancellation after Assign</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">by</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Rejection</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">by</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Re-assign</b>
      </td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">by</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Acceptance</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">by</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Submitting report</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">by</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Sending back to TPM</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">by</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>UNICEF Approval</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">Y</td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
The email notifications for action points aren't presented here. See more information in the [Action Point Dashboard Documentation](https://razortheory.gitbook.io/action-points-dashboard/)
{% endhint %}

The detailed information of the Visit workflow see[ here](../tpm-workflow.md).

