
Intro
Not all tests are made equal, they have advantages and limitations which is why coverage at different phases of the development pipeline is important.
As a team we give these types of tests a name so we have a common language and expectation for each type.
What they cover is important. For example, if we did all our tests just before putting something into production our feedback loop is long and the time to remediate is also long. We can illustrate this using the famous Testing Pyramid which shows the relationship between test coverage, time and cost.
  
Test Pyramid
 
Test definitions and phases 
 
Test Type	Definition	Phase	Branch	Account / Cluster	Owner
Unit	Does this bit of code behave the way I want given these inputs?	BUILD 	FEATURE BRANCH	nbs-tmw-dev / feature-test	Developer
Functional	Does the component run and behave the way I expect given this input?
Service is running like it would in production, but external interactions are stubbed out providing reliability and control over test scenarios
BUILD	FEATURE BRANCH	nbs-tmw-dev / feature-test	Developer
Feature / Acceptance	Does the new feature behave as it should for our users?
New feature is tested against business defined acceptance criteria, may include performance testing
post Deploy	FEATURE BRANCH	nbs-tmw-dev / feature-test	QA/Product Owner
End user	Does the service run as intended with other dependent services?
Give verification that configurations are correct for the given environment and interactions with other services
All known features are tested against business defined acceptance criteria, cross browser/device coverage	post Deploy	FEATURE BRANCH	nbs-tmw-dev / intergration-test	QA
Load	How do the applications perform under load?
What is the peak load?	post Deploy	Main BRANCH	nbs-tmw-test / staging	QA
Performance / Fitness	How quick does the page and components load?	post Deploy	Main BRANCH	nbs-tmw-test / staging	QA
Production Tests/Monitoring	Once deployed to production are the key user journeys working	Scheduled 	Main BRANCH	nbs-tmw-prod / apps	 
 
Test frameworks and scope
 
Component	Test Type	Framework	Scope / Good For	Not good for
UI components (Storybook)
	Unit	Jest	1.	Inputs and outputs of component (Non static text)
a.	Events
b.	States
c.	Props	1.	Does not cover the integration of said component
	Functional	Snapshot/Visual	1.	Branding
a.	Fonts
b.	Typography
2.	Responsive layouts	 
NPM libraries	Unit	Jest	1.	Class/method level unit tests
2.	Calculations / business rules and logic	 
Websites	Unit	Jest	1.	Class/method level unit tests
2.	Calculations / business rules and logic	 
	Functional	Cypress	1.	Integration of components work based on the expected data under test (mocked API responses)
2.	End to end user journey’s within the component
3.	Detailed UI assertions
4.	Failure scenarios
5.	Expected API requests	1.	Unable to cover real external integrations as these are mocked out
	End user (per build / fortnightly)	Selenium / SpecFlow / BrowserStack	1.	Full user journey’s which span across multiple websites
2.	Integration of websites and APIs
3.	Cross browser
4.	Cross device	1.	Detailed level asserts which should be covered earlier in the pipeline as these will cause slow test runs and is expensive way to find out that some text is not what is expected for example
APIs / Console apps etc	Unit	xUnit	1.	Class/method level unit tests
2.	Calculations / business rules and logic	 
	Functional	xUnit	1.	All API inputs and outputs should be covered
a.	Expected external calls (using WireMock)
b.	Expected database reads/writes
c.	Expected HTTP response codes	1.	Actual points of integration as these are mocked
	Integration	Postman	1.	Covers key scenarios once deployed proving the wider integration of the start service	1.	Detailed coverage which should be covered earlier i.e. in the functional tests


