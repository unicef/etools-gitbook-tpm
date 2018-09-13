# Emails notifications flow

The table below describes the cases when the email notification is sent depending on user roles and actions performed with visit.  

| Actions/Roles  | **TPM organization** | **PME** | **TPM Focal point** | **UNICEF Focal point** |
| :--- | :--- | :--- | :--- | :--- |
| **Cancellation before Assign** | N | by                 | N                      | N |
| **Assign** | Y | by | Y | N |
| **Cancellation after Assign** | N | by | N | N |
| **Rejection** | N | Y | by | Y |
| **Re-assign** | Y | by | Y | N |
| **Acceptance** | N | N | by | N |
| **Submitting report** | N | Y | by | Y |
| **Sending back to TPM** | N | by | Y | N |
| **UNICEF Approval** | N | N | Y | Y |

{% hint style="info" %}
The email notifications for action points aren't represented. See more information in the [Action Point Dashboard Documentation](https://razortheory.gitbook.io/action-points-dashboard/)
{% endhint %}

The detailed information of the visit workflow see[ here](../tpm-workflow.md).

