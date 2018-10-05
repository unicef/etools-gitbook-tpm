# Model Mixins \(Review\)

### ModelHavingTenantRelationsMixin

Sometimes we need to remove some objects. Usually, this is common task without complexity, but when we use Tenants, we can encounter case when we need to delete global object, which has some relations from tenants. Database will not allow this and raise IntegrationError. So before removing parent object, we need to ensure that there is no relations from tenants left.





