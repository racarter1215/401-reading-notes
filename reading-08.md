# LINQ

### Or Language-Integrated Query, a set of technologies based on the integration of query capabilities directly into C#.

##### Utilizing LINQ offers language constructs such as classes, methods, events. LINQ provides queries experience for objects, relational databases, and XML.

##### LINQ works with C# for SQL Server databases, XML documents, ADO.NET Datasets, and IEnumerable or the generic IEnumerable<T> interface. 

##### Example of using LINQ:

##### class LINQQueryExpressions
##### {
#####     static void Main()
#####     {

#####         // Specify the data source.
#####         int[] scores = new int[] { 97, 92, 81, 60 };

#####         // Define the query expression.
#####         IEnumerable<int> scoreQuery =
#####             from score in scores
#####             where score > 80
#####             select score;

#####         // Execute the query.
#####         foreach (int i in scoreQuery)
#####         {
#####             Console.Write(i + " ");
#####         }
#####     }
##### }

### LINQ Queries

##### Query: expression that retrieves data from a data source.

##### LINQ simplifies queries by giving a consistent model for working with data across data sources and formats.

##### Query Operation: Three Parts
###### Obtain the data source.
###### Create the query.
######Execute the query.

##### Query Operation Example:

##### class IntroToLINQ
##### {
#####     static void Main()
#####     {
#####         // The Three Parts of a LINQ Query:
#####         // 1. Data source.
#####         int[] numbers = new int[7] { 0, 1, 2, 3, 4, 5, 6 };

#####         // 2. Query creation.
#####         // numQuery is an IEnumerable<int>
#####         var numQuery =
#####             from num in numbers
#####             where (num % 2) == 0
#####             select num;

#####         // 3. Query execution.
#####         foreach (int num in numQuery)
#####         {
#####             Console.Write("{0,1} ", num);
#####         }
#####     }
##### }

##### Data Source Examples: See https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq-queries

### Basic LINQ query operations

##### Obtaining Data Source

#####  In a LINQ query, "from" comes first to introduce data source and the range variable.

##### Example:

##### //queryAllCustomers is an IEnumerable<Customer>
##### var queryAllCustomers = from cust in customers
#####                         select cust;

##### Filtering: causes the query to return only those elements for which the expression is true.

##### Example:

##### var queryLondonCustomers = from cust in customers
#####                            where cust.City == "London"
#####                            select cust;

### Walkthrough: Writing Queries in C# (LINQ)

##### Creating C# Project with LINQ:

##### Start Visual Studio.

##### On the menu bar, choose File, New, Project.

##### The New Project dialog box opens.

##### Expand Installed, expand Templates, expand Visual C#, and then choose Console Application.

##### In the Name text box, enter a different name or accept the default name, and then choose the OK button.

##### The new project appears in Solution Explorer.

##### Notice that your project has a reference to System.Core.dll and a using directive for the System.Linq namespace.

##### Creating in-Memory Data Source

##### Example:

##### public class Student
##### {
#####     public string First { get; set; }
#####     public string Last { get; set; }
#####     public int ID { get; set; }
#####     public List<int> Scores;
##### }

##### // Create a data source by using a collection initializer.
##### static List<Student> students = new List<Student>
##### {
#####     new Student {First="Svetlana", Last="Omelchenko", ID=111, Scores= new List<int> {97, 92, 81, 60}},
#####     new Student {First="Claire", Last="O'Donnell", ID=112, Scores= new List<int> {75, 84, 91, 39}},
#####     new Student {First="Sven", Last="Mortensen", ID=113, Scores= new List<int> {88, 94, 65, 91}},
#####     new Student {First="Cesar", Last="Garcia", ID=114, Scores= new List<int> {97, 89, 85, 82}},
#####     new Student {First="Debra", Last="Garcia", ID=115, Scores= new List<int> {35, 72, 91, 70}},
#####     new Student {First="Fadi", Last="Fakhouri", ID=116, Scores= new List<int> {99, 86, 90, 94}},
#####     new Student {First="Hanying", Last="Feng", ID=117, Scores= new List<int> {93, 92, 80, 87}},
#####     new Student {First="Hugo", Last="Garcia", ID=118, Scores= new List<int> {92, 90, 83, 78}},
#####     new Student {First="Lance", Last="Tucker", ID=119, Scores= new List<int> {68, 79, 88, 92}},
#####     new Student {First="Terry", Last="Adams", ID=120, Scores= new List<int> {99, 82, 81, 79}},
#####     new Student {First="Eugene", Last="Zabokritski", ID=121, Scores= new List<int> {96, 85, 91, 60}},
#####     new Student {First="Michael", Last="Tucker", ID=122, Scores= new List<int> {94, 92, 91, 91}}
##### };

##### Create query example:

##### // Create the query.
##### // The first line could also be written as "var studentQuery ="
##### IEnumerable<Student> studentQuery =
#####     from student in students
#####     where student.Scores[0] > 90
#####     select student;

##### Executing Query example:

##### // Execute the query.
##### // var could be used here also.
##### foreach (Student student in studentQuery)
##### {
#####     Console.WriteLine("{0}, {1}", student.Last, student.First);
##### }

##### // Output:
##### // Omelchenko, Svetlana
##### // Garcia, Cesar
##### // Fakhouri, Fadi
##### // Feng, Hanying
##### // Garcia, Hugo
##### // Adams, Terry
##### // Zabokritski, Eugene
##### // Tucker, Michaelf

