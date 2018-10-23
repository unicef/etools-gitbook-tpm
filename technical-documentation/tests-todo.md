# Tests

### TransitionPermissionsTestCaseMixin

FSM Transitions are important part of functionality, so we need to test them fully. For this purposes TransitionPermissionsTestCaseMixin was built. It automatically scan model for full list of transitions and generate test functions to check that all required transitions are available and the rest are closed when they are not required.  
If some additional arguments are required to perform some transition, they can be added inside custom `create_object` function.  
Final class should implement `do_transition` method, which will perform transition, because statuses flow may vary a lot for different modules and process can be totally different.

### InheritedTrait

For generating instances in all required statuses we use factory arguments, named traits. They work well, but in our case we need all information from previous statuses. So there is a possibility to nest them correctly. Very handy is to use `pre_<status>` traits for testing transitions.  
Example, when value is required to do `complete` transition:

```python
class SomeFactory(factory.DjangoModelFactory):
    class Params:
        pre_completed = factory.Trait(value="test")
        completed = InheritedTrait(
            pre_completed,
            status='completed'
        )
```

