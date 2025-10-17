### Session Service:
- Session createSession(user_id, connection_id)
- List<Session> getSessions(user_id)
- void logoutSession(session_id)
### Call State Manager:
- Call initiateCall(caller_number, callee_number)
- Validations and checks here. Find their profile. Find a route. Check for balance.
- Boolean extendLease(Call)
### Switch:
- Call initiateCall(StateMachine callStateMachine)
- StateMachine is an object, where different state transitions are mapped to actions.
- This defines the state machine for a single call. For example, state change of
- terminated leads to action of "freeUpBandwidth".
- State changeState(Call, CurrentState, ChangeToState)
### Invoice Service:
- Invoice createInvoice(call_id, talk_time, price_per_minute, currency)
- addBalance(user_id, amount, currency)
- lockBalance(user_id, amount, currency)
- getBalance(user_id)
### Router Service:
- Provider getRoute(User A, User B)
- Provider is a phone service provider's routing address. The call paths will now be
- patched using this address.
