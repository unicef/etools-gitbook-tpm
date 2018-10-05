# Serializer Mixins \(Review\)

### Nested serializers

For editing nested data we use nested serializers. Mostly `unicef_restlib.serializers.WritableNestedSerializerMixin` should be used. It consists of three mixins:  


#### DeletableSerializerMixin

This mixin allows us to delete nested instances. This can be done with the `_delete`  flag. For example, when we want to delete nested instances having id 3 and 5, we can make update request with

```javascript
{
    "<some nested serializer>": [
        {"id": 3, "_delete": true},
        {"id": 5, "_delete": true},
        ... some more updates together with delete parts
        {"id": 2, "value": "some new value"}
    ]
}
```

#### WritableNestedParentSerializerMixin

This mixin scan nested serializers during `create` or `update` call and then separate own data from nested.  Then trying to validate nested data using found serializers and save everything atomically. 

#### WritableNestedChildSerializerMixin

Another part of writable serializers, with logic connected to child instances.  Firstly, we set pk field as writable and not required. This allows us to also define instances without pk, which should be created.

```javascript
{
    "<some nested serializer>": [
        {"id": 3, "_delete": true},  # will be removed
        {"id": 2, "value": "some new value"},  # will be updated
        {"value": "some value"}  # new instance
    ]
}
```

Also, we divide validators to simple, which don't require instance and deferred, e.g. unique or unique together. This is required, because we may try to add conflicting information inside one request, for example users with the same unique email.

Parent & Child serializers are designed to be used together, just separated logically for easier understanding.

### 

