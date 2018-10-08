# Model Mixins \(Review\)

### ModelHavingTenantRelationsMixin

Sometimes we need to remove some objects. Usually, this is common task but with Tenants we can encounter case when global object having relations from tenants needs to be removed. Database will not allow this and raise IntegrationError. So before removing parent object, we need to ensure there is no related objects left in tenants.



