# Fixtures & management commands \(TODO\)

To manage some data we use fixtures & custom commands. Mostly custom commands are used for managing email templates and for updating permissions, because their definitions are complex and hard to control using fixtures.

* `python manage.py tenant_loaddata attachments_file_types` - _load list of file types for attachments_
* `python manage.py loaddata tpm_groups` - _load set of required groups for module_
* `python manage.py update_notifications` - _update email templates_
* `python manage.py update_tpm_permissions` - _update module related permissions_

All commands are designed to be safely executed multiple times without data duplication, so they are recommended to run after every deployment to be sure that actual data will be provided.

\(todo\) audit

* `python manage.py loaddata audit_staff_organization` - _load information about UNICEF audit organization_
* `python manage.py tenant_loaddata attachments_file_types` - _load list of file types for attachments_
* `python manage.py tenant_loaddata audit_risks_blueprints` - _load full set of risk blueprints  questions\) which are used for Micro Assessment questionnaire & for some similar blocks_
* `python manage.py loaddata audit_groups` - _load set of required groups for module_
* `python manage.py update_notifications` - _update email templates_
* `python manage.py update_audit_permissions`  - _update module related permissions_

\(todo\) action points

* `python manage.py update_notifications` - _update email templates_
* `python manage.py update_audit_permissions`  - _update module related permissions_



