# Unit Testing

### It isn't putting information in a database or reading files stored on disks
##### It also doesn't include things that can fail if a machine is not "properly setup"
##### It is also a specific test, it doesn't include tests that make lots of requests.
##### They don't generate data and hurl themselves at your app and are not executed by QA
##### They also don't utilize several components of your system to check their ability to act

### What Unit Testing Is

##### Unit tests test specific units of code
##### In C#, methods are units, therefore unit tests test methods
##### Unit tests test something specifi in units isolated from the rest of the code
##### Example:

##### public class Calculator
##### {
#####     public int Add(int x, int y)
#####     {
#####         return x + y;
#####     }
##### }

##### Once you have some code like this, you make a console project and give it a reference to the project, like it has in the picture on the resource site.

##### class Program
##### {
#####     static void Main(string[] args)
#####     {
#####         var calculator = new Calculator();

#####         int result = calculator.Add(5, 6);

#####         if (result != 11)
#####             throw new InvalidOperationException();
#####     }
##### }

### Unit Test Framework

##### Instead of making tests for every single unit, you can use a framework for all of them to fit under
##### Delete the old test, right click on the solution to add a project, and choose "Unit Test Project Template"

##### Call the new test something like "UnitTest1"
##### Example:

##### [TestClass]
##### public class UnitTest1
##### {
#####     [TestMethod]
#####     public void TestMethod1()
#####     {
#####         var calculator = new Calculator();

#####         int result = calculator.Add(4, 3);

#####        Assert.AreEqual(7, result);
#####     }
##### }

##### Click Ctrl-R, T to run the test

# xUnit.net

### this is a free, open source, community-focused unit testing tool for the .NET framework.

##### check this link for packages and builds https://xunit.github.io/#packages

##### This is the link to the config files https://xunit.github.io/docs/configuration-files

##### Link to the JSON package https://xunit.github.io/schema/current/xunit.runner.schema.json

# The Art of Readme

### Originally came from informative punchcards with READ ME! written on them

##### The jist was that the user should read before acting

##### the Node ecosystem is powered by modules. NPM makes it all happpen. 
##### since you can get access easy, it follows that quality is varied. Some tools are good, others less so

##### Modules can be named weird things that hinder their use
##### All sorts of problems can result from not understanding whats going on

##### To combat this, things such as curated lists of quality modules have been created. Social graphs (based on use) have been created to show whats popular and who's using them.

##### For all of these remedial actions, the first thing one will see is a README.

##### README's say the following: tells what the thing is, show what the thing looks like in action, shows how to use the thing, and tell others relevant data about the thing.

##### The above is YOUR job. as a creator you have to prove your work.

##### Brevity is key, as README's could otherwise go on forever

# README best practices

### Use this link for a default practice README curl https://raw.githubusercontent.com/jehna/readme-best-practices/master/README-default.md > README.md

##### atom README.md is utilized if you use Atom code editor

##### After you wrote the README.md, push to github

##### You can bootstrap your project effectively, ensure users know what you were trying to do, and follow good instructions for a good README
