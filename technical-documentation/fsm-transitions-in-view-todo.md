# FSM Transitions in view \(Review\)

Transitions between FSM states in the module are performed manually, without automation. To work with them, was implemented `etools.applications.utils.common.views.FSMTransitionActionMixin` view mixin which define custom viewset action which is trying to find required transition, checks if transition is allowed and conditions are met and validate input through transition serializer \(if provided\).  
Also, for custom logic were added pre\_transition and post\_transition hooks, which can be easily overriden to provide additional functionality, for example to integrate with Snapshot model, like it's done in the`unicef_snapshot.views.FSMSnapshotViewMixin`.

