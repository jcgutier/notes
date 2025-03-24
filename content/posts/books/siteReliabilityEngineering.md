# Site Reliability Engineering

Authors: Niall Richard Murphy, Besty Beyer, Chris Jones, Jennifer Petoff

## Troubleshooting

Iteratively hypothesize potential causes for a failure and try to test those hypotheses
	- Look at system's telemetry and logs to understand it's current state, combined with the knowledge of how system is built, how it should operate ans its failure modes
	- Undestanding of the system
	- Undestanding of the metrics
	- Undestanding on how to change the system
	- Do not assume that causes for similar past problems are the causes for todays problems
	- Try to disapprove the hypothesis, try to probe that hypothesis are wrong, falsifiable

Troubleshooting is an implementation of [Hypothetico-deductive model](https://en.wikipedia.org/wiki/Hypothetico-deductive_model)

An effective report should tell you the expected behavior, the actual behavior, and, if possible, how to reproduce the behavior

Ideally, the reports should have a consistent form and be stored in a searchable location, such as a bug tracking system.

Take clear notes of what ideas you had, which test you ran and the result you saw when troubleshooting. Could be useful to send updates on slack channels when actions occurs or shared document with timestamps

## Emergency Response

How to train the team to be in good shape to respond to incidents or emergencies?

What to do when system break ?
Do not panic, you are a professional and trained to handle this sort of situations, no one is on physical danger.
If you feel overwhelmed pull in more people. Make sure that you are familiar with the incident response process on you company and follow that process.

Adopt a proactive approach to disaster and emergency testing, with proper communication to all customers.

Oftentimes, the person with the most state is the one whose actions somehow triggered the event. Utilize that person.

## When to Declare an Incident

If any of the following is true, the event is an incident:

- Do you need to involve a second team in fixing the problem?
- Is the outage visible to customers?
- Is the issue unsolved even after an hour’s concentrated analysis?

Best Practices for Incident Management
Prioritize. Stop the bleeding, restore service, and preserve the evidence for root-causing.
Prepare. Develop and document your incident management procedures in advance, in consultation with incident participants.
Trust. Give full autonomy within the assigned role to all incident participants.
Introspect. Pay attention to your emotional state while responding to an incident. If you start to feel panicky or overwhelmed, solicit more support.
Consider alternatives. Periodically consider your options and re-evaluate whether it still makes sense to continue what you’re doing or whether you should be taking another tack in incident response.
Practice. Use the process routinely so it becomes second nature.
Change it around. Were you incident commander last time? Take on a different role this time. Encourage every team member to acquire familiarity with each role.

## Postmortem

Review and learn from postmorterms

## Disaster Role Playing

Once a week we have a meeting where a victim is chosen to be on the spot in front of the group, and a scenario—often a real one taken from the annals of Google history—is thrown at him or her. The victim, whom I think of as a game show contestant, tells the game show host what s/he would do or query to understand or solve the problem, and the host tells the victim what happens with each action or observation

## Types of software testing

Software tests broadly fall into two categories: traditional and production
	- Traditional: Evaluates the correctness of software offline, during development
	- Production: Are performed on a live web service to evaluate whether a deployed software system is working correctly

Traditional test consist in 3 layer from bottom to top: Unit test, integration test and system tests

	- Unit tests: Is the smallest testing. This asses a separable unit of software, such as class or function for correctness independent of the larger software system that containers the unit. Unit tests are also employed as a form of specification to ensure that a function or module exactly perform the behaviour required by the system
	- Integration tests: Software components that pass indicudual unit tests are assembled into larger compnents. Engineers then run an integration test on an assembled component to verify that it functions correctly. Dependency injection is a powerful technique for creating mocks of complex dependencias so that engineer can cleanly test a component, as an example a dependency injection si to ro replace  a stateful datatbase with a light weight mock that has precisely specified behaviour.
	- System test: Is the largest scale test for an undeployes system. Engineer test the end to end functonality of the system, there are many different systm tests:
		○ Smoke test: Test very simple but critical behaviour
		○ Performance test: Its a variant of smoke test that ensure the performance of the system stays acceptable over the duration of its lifecycle. Test the memory usage, CPU, latency, errors.
		○ Regression tests: This involves searching back the bugs that were there to document those bugs as test at the system or integration level, so they do not re-appear again.
Production Tests

This type of test interacts with a live prodution system, they are similar to black-box monitoring

