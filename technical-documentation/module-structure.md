# Module structure

### TPM module files structure

![](../.gitbook/assets/image.png)

`export` - everything that is related to csv & pdf exports  
`management` - specific management commands. in our case there is only command for updating permissions.  
`migrations` - database migrations  
`serializers`- rest framework serializers  
    - `attachments.py` - visit attachments serializers  
    - `partner.py` - tpm partner serializers  
    - `visit.py` - serializers for visit, activity,   
- `templates` - templates to be used in various exports. visit letter & activities pdf export  
- `tests` - tests for models, views, serializers, transitions flow  
-  `tpmpartners` - nested global application to keep shared across the countries information about tpm firm  
- `transitions` - everything that is related to fsm transitions  
    - `conditions.py` - custom checks for transitions. for example in case of submitting report we need to be assured that report attachments are exists.  
    - `serializers.py` - transitions serializers to validate their input arguments \(see more in permissions framework section inside views paragraph\)  
- `admin.py` - admin site definitions for models  
- `apps.py` - python app configuration  
- `conditions.py` - conditions to perform FSM transitions. More in Permissions framework  
- `filters.py` - rest framework views filters  
- `metadata.py` - base metadata class to be used in viewsets. more in API Metadata section  
- `models.py` -  country-related tpm models  
- `signals.py` - app signals. custom logic for user deletion; sending notifications in case of assigning action points  
- `urls.py` - app urls  
- `views.py` - just set of views to work with models

### tpm.tpmpartners app

To store global data that is related to TPM, was implemented nested application named `tpmpartners`.   
Views and serializers are still placed in tpm application to keep consistant place for all module logic.

App consists of:  
- `models.py` - partner with their staff members  
- `synchronizer.py` - VISION partner synchronizer  
- `tasks.py` - periodic, which are responsible to keep partners synced with VISION  


