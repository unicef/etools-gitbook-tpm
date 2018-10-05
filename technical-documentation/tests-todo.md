# Tests \(TODO\)

### TransitionPermissionsTestCaseMixin

FSM Transitions are important part of functionality, so we need to test them fully. For this purposes TransitionPermissionsTestCaseMixin was built. It automatically scan model for full list of transitions and generate test functions to check that all required transitions are available and the rest are closed when they are not required.  
If some additional arguments are required to perform some transition, they can be added inside custom `create_object` function.  
Final class should implement `do_transition` method, which will perform transition, because flow may vary a lot for different modules and process can be totally different.

Factories & InheritedTraits

