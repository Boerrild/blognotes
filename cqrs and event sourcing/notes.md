DDD, CQRS and Event Sourcing
============================


## Testing for Uniqueness

When it comes to creating aggregates one question that is quickly raised is how 
and when to test uniqueness of "non-UUID" attributes like e.g. UserName.

The following threads discuss this:

[1] http://stackoverflow.com/questions/9495985/cqrs-event-sourcing-validate-username-uniqueness?rq=1 
and 
[2] http://stackoverflow.com/questions/2015451/domain-queries-in-cqrs

Pay special attention to the reply of David Masters in [1] and Udi Dahans 
answer to David Masters question in [2].

The excerpt (in my own interpretation) is:

In for instance your REST service controller (perhaps delegating to a 
traditional Application Service) we add the logic for testing the uniqueness 
of the specified attribute, for instance by using the querying model (read 
model). Keep in mind, though, that this is only a convenience last-minute-
attempt-to-avoid-a-duplicate-instance-manouvre as the read model is per 
definition "stale" data. 

The up-front test probably need to be followed up by an after the fact 
"compensating action" triggered by the event, if it turns out that the name is 
no longer unique, then go and change it to something unique.   

An alternative to letting an Application Service/Web service handle this could 
be to use a CommandInterceptor to validate the Command prior to dispatching it 
as they claim to have applied in the AxonTrader sample application (see e.g. 
'AxonsFramework). 

Allard Buijze also wrote:
"Best practice is to simply do a query before you send the command. That
means you do a query for the username before creating a new user.
Alternatively, in your event handler, you can also write some logic to
block a second user account with the same username if it happens.
It's a matter of risk versus cost.

The ddd/cqrs mailinglist contains a number of interestin discussions about
this."


## Enriching Events

The ones preparing the events may choose to enrich them with additional data needed for views.
See this discussion: https://groups.google.com/forum/#!topic/dddcqrs/Xq1H2zJh3LU
