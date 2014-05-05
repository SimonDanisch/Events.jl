# Events
Simple event system!

You can register Actions for certain event Types.
The type for this is EventAction{Event} and consists of two functions, one is the condition for the action to be executed and the other is the action itself.
```
immutable EventAction{T}
	#condition(T, conditionArgs...) -> Bool
	condition::Function
	conditionArgs::Tuple
	#action(T, actionArgs...) -> nothing
	action::Function
	actionArgs::Tuple
end
```

The Event type is parametric and the parameter is an ID. 
This makes a nested event Flow possible.

```
testPrint(event::MouseMoved{1}) = println(event)
testPrint(event::MouseMoved{2}) = println("Wow, event id 2")


eventAction3 = EventAction{MouseMoved{1}}(x -> true, (), republishEvent, ())
eventAction1 = EventAction{MouseMoved{1}}(x -> true, (), testPrint, ())
eventAction2 = EventAction{MouseMoved{2}}(x -> true, (), testPrint, ())

registerEventAction(eventAction1)
registerEventAction(eventAction2)
registerEventAction(eventAction3)

publishEvent(MouseMoved{1}(0,0))

deleteEventAction(eventAction1)

clearEventActionQueue()

```

Please feel free to give criticism and feedback! =)