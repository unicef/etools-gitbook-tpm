# FSM Transitions conditions

In some cases there are additional requirements in order to allow the process to go to the next step. For this, custom conditions that integrates with transitions out of the box, were built. 

Base classes for them:

* `BaseTransitionCheck` - base check which collects validation errors inside `get_errors` function and raise them if conditions are not met.
* BaseRequiredFieldsCheck - has `fields` attribute which contain list of required fields to allow performing of transition.

Examples:

Check that attachments of specific type are provided:

```python
class ReportAttachmentsCheck(BaseTransitionCheck):
    def get_errors(self, instance, *args, **kwargs):
        errors = super().get_errors(*args, **kwargs)

        if not instance.report_attachments.filter(file_type__name='report').exists():
            errors['report_attachments'] = _('You should attach report.')
        return errors
```

Check that partner and all required focal points are provided before visit assignment:

```python
class TPMVisitAssignRequiredFieldsCheck(BaseRequiredFieldsCheck):
    fields = [
        'tpm_partner', 'unicef_focal_points', 'tpm_partner_focal_points'
    ]
```

Example of the error response in case of unmet conditions:

![](../.gitbook/assets/8iewjg.jpg)



