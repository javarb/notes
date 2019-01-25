# SOFTWARE ENGINEERING IN JAVA

## Session 23 (22/01/2019)

- 

### Notes


https://site.mockito.org/

Mockito should be used for test big things third party services 
but for own projects could be the best is to use our own implementation 
since we have all the control since Mockito is very big (still is pretty performant)

We did some changes to our Calculator test using mockito

This is not neccesary the interface implementation but as we have this as a dependency in other test we cannot delete it

We created another branch and we can develop it maybe all in Mockito, still isn't in the kanban

TDD, Junit and mocking and integration test -> Testing today

Is needed experience writing own code.

Quality assurance

BDD (behaviour driven development) / acceptance
Gherkin <- language 
Cucumber <- framework 

this is the behaviour expected and can be readed by non technical people:
https://github.com/bugsnag/bugsnag-go/blob/master/features/net_http_features/appversion.feature


this is the translation to technical stuff:
https://github.com/bugsnag/bugsnag-go/blob/master/features/steps/go_steps.rb


As the requirements change in the time these test has to change

Consultancy - client see the results are asked
Make sure top level behaviour

Is expensive and requires big effort/time/money but get a lot in return.


here is another example for java
https://github.com/bugsnag/bugsnag-java



in features are the high level steps legible for non technical people
https://github.com/bugsnag/bugsnag-java/tree/master/features
https://github.com/bugsnag/bugsnag-java/blob/master/features/app_type.feature

In steps there are the actual test implementations
https://github.com/bugsnag/bugsnag-java/blob/master/features/steps/build_steps.rb


And in fixtures are the running applications https://github.com/bugsnag/bugsnag-java/tree/master/features/fixtures/mazerunnerplainspring/src/main/java/com.bugsnag.mazerunnerplainspring



Consistent  and after high 

consistency is more important

8 we will split 
5 considering split
1,2,3 is fine


The branch into api is for test all the endpoints.

We fixed the kanban to this week, we made a feedback session to see what happened what could to improve, but isn't needed to say
something always

This week complete things was 5 and 8 missing because is not completed (revision) so i considered that from those
8, 5 are missing so Roger considered that for this week the mark should be 10 and not 13 so as I had still 5, then I added another 5 in documentation, and if I finish earlier, then I could do somehting about programming.



### Resources

- [][1]


[1]: https://www.mkyong.com/java/how-to-get-current-timestamps-in-java/
