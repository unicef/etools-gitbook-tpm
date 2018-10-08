# FSM Transitions in view

Transitions between FSM states in the module are performed manually, without automation. To work with them, `etools.applications.utils.common.views.FSMTransitionActionMixin` view mixin was implemented, that define custom viewset action which is trying to find the required transition, checks if the transition is allowed and conditions are met and validates input through the transition serializer \(if provided\).  
Also, for custom logic were have added pre\_transition and post\_transition hooks, which can be easily overriden to provide additional functionality, for example to integrate with Snapshot model, like it's done in the`unicef_snapshot.views.FSMSnapshotViewMixin`.

