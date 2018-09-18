# Permissions framework

main module - etools.applications.permissions2 The core of the module is the Permissions module. It consists of target \({app}.{module}.{field}\), permission \(read/write/action\) permission type \(allow/deny\) and array of required predicates for this permission. The main idea is to collect permissions context \(predicates\) and then restrict access to fields if not all permission conditions are met. In most cases only `allow` permissions should be used, to allow correct roles mixing and to be system flexible enough, but if required, black list also can be helpfull. So, firstly will be applied white list, which enables some fields for user, and then result will be passed through black list, which will filter out fields that met hist conditions.

Predicates Each permission has list of predicates that should exist in context. When view is processing, it generates list of Conditions, which returns predicate or empty value \(if condition is not satisfied\). Also condition can return list of predicates \(example - GroupCondition, which returns value for every user group\). Resulting list can be simply used in permissions queryset filter by array.

Serializers to protect fields from being edited without required permissions etools.applications.permissions2.serializers.PermissionsBasedSerializerMixin should be used. it filters out inaccessible fields from \_writable\_fields and \_readable\_field, so there is no way to read or edit them through serializer. Main part of work of this mixin is just collecting list of targets that are used as fields. It required conditions to be included into context inside `permission_context`.

serializer process flow can be described in the next steps:

* collect targets from it's fields
* filter permissions using collected targets
* apply provided permissions context to filtered permissions

Views

PermissionContextMixin collects permissions context. By default user groups \(GroupCondition\) & information about new instance \(NewObjectCondition\) existing in context.

For checking serializer permissions was implemented PermittedSerializerMixin which is inherited from PermissionContextMixin and deny access if user is not allowed to access any field.

Additionally, fsm transitions can be protected with permissions. PermittedFSMActionMixin can be used to check them and provide flexible endpoint for switching between FSM transitions. In this case transitions can be performed with POST to `/api/<view_path>/<transition_name>/`. If conditions are met, instance will go to the next state. If any additional information is needed \(e.g. cancellation reason\), serializer can be attached to transition.

Example:

```python
class CancelSerializer(serializers.Serializer):
    cancelled_by = serializers.HiddenField(default=serializers.CurrentUserDefault())
cancel_comment = serializers.CharField()

@transition(..., custom={'serializer': CancelSerializer})
def cancel(self, cancelled_by, cancel_comment):
...
```

in this case initiator \(automatic\) and required comment will be passed to transition function. in case of missing comment, corresponding validation error will be raised.

view-level permissions In case of nested views it's important to be assured that we have access to nested field. Example - for editing visit attachments we have to be allowed to edit tpmactivity.attachments field. to protect view, drf permissions can be generated with get\_permission\_for\_targets.

```python
class ActivityAttachmentsViewSet(BaseTPMAttachmentsViewSet):
    permission_classes = BaseTPMViewSet.permission_classes + [
        get_permission_for_targets('tpm.tpmactivity.attachments')
    ]
```

