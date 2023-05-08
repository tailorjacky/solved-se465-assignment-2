Download Link: https://assignmentchef.com/product/solved-se465-assignment-2
<br>
<h1>Question 1 : More Selenium</h1>

In your repository, you will find a JavaScript application at <sub>shared/calc/index.html</sub>. I wrote this application (or at least ported it from the Internet). It uses a Pratt parser to parse a simple expression language and evaluate the given expression.

Here is a grammar for this application. The <sub>^ </sub>operator is supposed to denote exponentiation.

⟨<em>expr</em>|<sub>|</sub>|| ⟨⟨‘‘-<sub>+</sub>⟩<em>expr</em><em><sub>expr</sub></em>’’::=⟨⟨<em>exprexpr</em>⟩number‘+⟩⟩’ ⟨<em>exprexpr</em>⟩⟩

⟩ ‘-’ ⟨

||| ⟨⟨<em>exprexpr</em>⟩⟩ ‘‘‘^*/’’’ ⟨‘⟨⟨)<em>exprexprexpr</em>’     ⟩⟩⟩

| ⟨<em>expr</em>⟩

‘(’ ⟨<em>expr</em>⟩

⟨<em>number</em>⟩ ::= [‘<sub>0</sub>’ – ‘<sub>9</sub>’]<sup>+</sup>

Your task is to manually (or otherwise) generate a set of test cases for this application and to use Selenium to automate these test cases. You shouldn’t need to look at the application source code, but you do need to look at the HTML of shared/calc/index.html.

In your test suite, I recommend setting <sub>baseUrl </sub>to one of:

<ul>

 <li>baseUrl = “file://” + System.getProperty(“user.dir”) + “/../calc/index.html”; baseUrl = “https://patricklam.ca/files/calc.html”;</li>

</ul>

Specifically:

<ul>

 <li>(2 points) Generate 10 test cases for the application. Specify the input along with the actual and expected output. Some of the inputs must be valid strings for the application, while others must be invalid. Be sure to choose interesting test cases.</li>

 <li>(3 points) The following test case exposes a bug in the application:</li>

</ul>

2+(8*3/4)^4*(1+3+5)*2-4*(3/2)+9*3

Minimize this test case. That is, produce a minimal-length subset of this test case—not necessarily using contiguous characters—which shows the same error. Explain the cause of the bug as well as the expected output.

<ul>

 <li>(2.5 points) Use Selenium to automate your 10 test cases. In the <sub>shared/selenium </sub>directory in your repo, you will find a <sub>SeleniumExample</sub>. You can run tests from this example using the command: mvn test “-Dtest=se465.SeleniumExample#test*” -Dwebdriver.base.url=http://www.google.com</li>

</ul>

Your test suite should be called <sub>se465.CalcSuite </sub>and we should be able to run your tests with this command: mvn test “-Dtest=se465.CalcSuite#test*”

We will check that your tests exercise the functionality that you specified in the first part. Assert on all fields on the calculator page. <strong>HINT: </strong>You can’t get the text from an input element with <sub>getText()</sub>. See instead <a href="https://www.w3schools.com/jsref/prop_text_value.asp">http://www.w3schools.com/jsref/prop_text_value.asp</a>. Useful reference: <a href="https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/WebElement.html">https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/WebElement.html</a>

Note: You are allowed to modify the application to add observability.

<h1>Question 2 : Page Objects</h1>

Recall the Page Object design pattern from Lecture 9. Your task is to create Page Objects for the JavaScript calculator. This will allow your tests to generalize to <sub>francais.html </sub>(and even <sub>eval.html</sub>, though we won’t use that).

<ul>

 <li>(10 points) In this part, we’ll create page objects. Create a generic Page Object interface <sub>CalculatorPage</sub>, along with an implementation <sub>se465.OriginalCalculatorPage</sub>, which encapsulates the UI elements on the index.html page. (I created the implementation first and then reverse-engineered the interface). These objects should allow you to access the controls that your tests from Question 4 need. Also, create an additional Page Object se465.FrancaisCalculatorPage which implements the same interface but which works with francais.html.</li>

 <li>(10 points) Copy CalcSuite to se465.RefactoredCalcSuite. Modify the refactored suite to use both of the page objects that you created for the first part; you should have two tests in the refactored suite for each test in the original suite. It’s OK for your English and French tests to essentially be the same except for the choice of the WebDriver, or you could be more clever. (This could be done via JUnit Parameters, but we haven’t talked about that.)</li>

</ul>

References for this question:

1 <a href="http://www.seleniumhq.org/docs/06_test_design_considerations.jsp#chapter06-reference">http://www.seleniumhq.org/docs/06_test_design_considerations.jsp#chapter06-reference </a><a href="https://martinfowler.com/bliki/PageObject.html">https://martinfowler.com/bliki/PageObject.html</a>

<h1>Question 3 : FSM-Based Testing</h1>

Consider the following FSM for the authentication part of a web app. (inspired by <a href="https://css-tricks.com/finite-state-machines-with-react/">https://css-tricks.com/finite</a><a href="https://css-tricks.com/finite-state-machines-with-react/">state-machines-with-react/</a>)

(2.5 points) Write out a single sequence of steps (i.e. one test case) that achieves Complete Round Trip Coverage on this FSM, including necessary context. For example, one of your steps could be “Log out of the web application”.

(5 points) A good authentication system must have anti-brute-forcing provisions. A brute-forcing attack on this system would repeatedly try passwords for a user until finding one that works. Describe briefly a fix to the implementation that would prevent the attack. Does my FSM still describe your fixed system? Write down why or why not; i.e. are my nodes and edges still appropriate? If not, provide a modified FSM that does.

(0 points) Think about how just looking at a model might not tell you how to construct a test case for the brute-forcing attack.

<h1>Question 4: Random Testcase Generation</h1>

Your task is to write code to randomly generate valid iCalendar <sub>.ics </sub>files. You can find the specification at

<a href="https://tools.ietf.org/html/rfc5545">https://tools.ietf.org/html/rfc5545</a>

<sup>1</sup>use a <sub>WebDriver </sub>rather than a <sub>Selenium </sub>object as in the example.

Although you will be marked against the full specification, following the description of the subset here will suffice.

<ul>

 <li>an ics file starts with a BEGIN:VCALENDAR line and ends with an END:VCALENDAR It must also contain a VERSION and <sub>PRODID </sub>line. (The provided code generates these for you.)</li>

 <li>your <sub>ics </sub>file should contain a sequence of events. Each event starts with <sub>BEGIN:VEVENT </sub>and ends with <sub>END:VEVENT </sub>and contains a set of components. Each event must contain UID, DTSTAMP and DTSTART components. Valid iCalendar events may contain other components, and we’ll be checking that your events do contain some other components.</li>

 <li>the <sub>UID </sub>must be a string that is unique per-event;</li>

 <li>the <sub>DTSTAMP </sub>and <sub>DTSTART </sub>components must contain dates/times, which are yyyymmddThhmmssZ, with T and Z literal and dates/times as appropriate.</li>

 <li>other valid components include LOCATION, SUMMARY, and DTEND.</li>

</ul>

You will find a <sub>generate.py </sub>file with skeleton code in the <sub>q1 </sub>directory of your repo. You can also find a number of sample ics files in the shared/icalendarlib directory. I can run the Python file with python generate.py at a prompt.

You are not required to use the skeleton <sub>generate.py</sub>; if you choose to write your own generator, email me (Patrick) to let me know. The path of least resistance is using the provided skeleton. You just need to add new rules to the CFG at the end of generate.py and new special productions to generate_special_production. (My solution adds 4 special productions and 9 <sub>add_prod </sub>lines to the CFG; you don’t really need to know Python to solve this problem, just pattern-match against what’s there already.)

<strong>Marking scheme. </strong>We will mark this by running your code 20 times to generate <sub>ics </sub>files. We then check that the files are different and that they include more than zero events and also more than zero optional components. Finally, we’ll check your generated files for validity against the iCal spec using an automated tool.

<strong>Bonus (0 marks).                </strong>Can you create valid <sub>ics </sub>files that break the app in <sub>shared/icalendarlib</sub>? (I can’t.) You can find links to more sample <sub>ics </sub>files here:

<a href="https://apple.stackexchange.com/questions/125338/calendar-ical-ics-format">http://apple.stackexchange.com/questions/125338/calendar-ical-ics-format</a>

<h1>Question 5 : Mutation Testing</h1>

Consider the following implementation of the cycle-finding algorithm<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>. (We’ve included the complete implementation from there in the skeleton at q5/cycle-finder.c, including a test harness.) In your q5/mutants.pdf file, propose two non-stillborn and non-equivalent mutants of this function. Clearly indicate where you’ve mutated the ground string. Write down test inputs which strongly kill these mutants (syntax doesn’t matter) and the expected output of your test cases on the original code and on the mutant.

typedef struct node_s { <strong>void </strong>*data; struct node_s *next;

} NODE;

<strong>int </strong>list_has_cycle(NODE *list)

{

NODE *fast=list; <strong>while</strong>(1) { <strong>if</strong>(!(fast=fast-&gt;next)) <strong>return </strong>0; <strong>if</strong>(fast==list) <strong>return </strong>1; <strong>if</strong>(!(fast=fast-&gt;next)) <strong>return </strong>0; <strong>if</strong>(fast==list) <strong>return </strong>1; list=list-&gt;next;

} <strong>return </strong>0; }

<a href="#_ftnref1" name="_ftn1">[1]</a> A more verbose implementation: <a href="https://en.wikipedia.org/wiki/Cycle_detection">https://en.wikipedia.org/wiki/Cycle_detection</a>.