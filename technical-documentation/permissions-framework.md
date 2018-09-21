---
description: etools.applications.permissions2
---

# Permissions framework

###  __Basics

The core of the module is the Permissions model.   
  
It consists of:  
- target \({app}.{module}.{field}\)  
- permission \(read/write/action\)  
- permission type \(allow/deny\)  
- array of required predicates for this permission.  
  
The main idea is to collect permissions context \(predicates\) and then restrict the access to the fields if not all permission conditions are met. In most cases only `allow` permissions should be used in order to allow the correct roles distribution and to unsure that the system is flexible enough, but if required, black list also can be helpfull. So, firstly the white list will be applied, which enables some fields for the user, and then the result will be passed through the black list, which will filter out the fields that met its conditions.

### Predicates

Each permission has the list of predicates that should exist in the context. When view is processing, it generates list of Conditions, which returns predicate or empty value \(if condition is not satisfied\). Also condition can return list of predicates \(example - GroupCondition, which returns value for every user group\). Resulting list can be simply used in permissions queryset filter by array.

### Serializers

To protect fields from being edited without the required permissions, etools.applications.permissions2.serializers.PermissionsBasedSerializerMixin should be used. It filters out inaccessible fields from \_writable\_fields and \_readable\_field, so there is no way to read or edit them through the serializer. Main part of the work of this mixin is just to collect the list of targets that are used as fields. It requires conditions to be included into the context inside the`permission_context`.

Serializer process flow can be described in the next steps:

* collect targets from its fields
* filter permissions using the collected targets
* apply provided permissions context to the filtered permissions

### Views

PermissionContextMixin collects permissions context. By default user groups \(GroupCondition\) and information about new instance \(NewObjectCondition\) existing in context.

In order to check the serializer permissions, PermittedSerializerMixin was implemented, which is inherited from PermissionContextMixin and deny access if user is not allowed to access any field.

Additionally, fsm transitions can be protected with permissions. PermittedFSMActionMixin can be used to check them and provide flexible endpoint for switching between FSM transitions. In this case transitions can be performed using POST to `/api/<view_path>/<transition_name>/`. If conditions are met, the instance will go to the next state. If any additional information is needed \(e.g. cancellation reason\), serializer can be attached to transition.

Example:

```python
class CancelSerializer(serializers.Serializer):
    cancelled_by = serializers.HiddenField(default=serializers.CurrentUserDefault())
cancel_comment = serializers.CharField()

@transition(..., custom={'serializer': CancelSerializer})
def cancel(self, cancelled_by, cancel_comment):
...
```

In this case initiator \(automatic\) and required comment will be passed to transition function. In case of the missing comment, corresponding validation error will be raised.

### View-level permissions

In case of nested views it's important to be assured that we have access to the nested field. Example: to edit the Visit attachments we have to be allowed to edit tpmactivity.attachments field. To protect view, drf permissions can be generated with get\_permission\_for\_targets.

```python
class ActivityAttachmentsViewSet(BaseTPMAttachmentsViewSet):
    permission_classes = BaseTPMViewSet.permission_classes + [
        get_permission_for_targets('tpm.tpmactivity.attachments')
    ]
```

### Updating permissions related to TPM module

Special management command were written to update the permissions . It can be called as:

```text
python manage.py update_tpm_permissions
```

and every time when called, it collects required set of permissions, removes old permissions, which are related to TPM \(their targets are starting with `tpm.` or `tpmpartner.`\) and creates everything that's needed.

The most important function in the management command is the`assign_permissions` one. Here are the definitions of the required permissions \(they are grouped by core instance statuses, so they are easy to understand\).

There are some examples of definitions:

```python
# everybody can view partner details, pme can edit
self.add_permissions([self.unicef_user, self.third_party_monitor], 'view', 
                     self.tpm_partner)
self.add_permissions(self.pme, 'edit', self.tpm_partner)

# pme can create new visits
self.add_permissions(self.pme, 'edit', self.visit_create, condition=self.new_visit())

# pme can assign and cancel draft visits
self.add_permissions(self.pme, 'action', ['tpm.tpmvisit.assign', 'tpm.tpmvisit.cancel'],
                             condition=self.visit_status(TPMVisit.STATUSES.draft))
```

