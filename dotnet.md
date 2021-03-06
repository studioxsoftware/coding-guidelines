# StudioX .NET Coding Standards

<!-- TOC -->
- [1. Purpose](#1-purpose)
- [2. Naming](#2-naming)
    - [2.1 Casing Style](#21-casing-style)
    - [2.2 Capitalization Rules for Identifiers](#22-capitalization-rules-for-identifiers)
    - [2.3 Capitalizing Compound Words and Common Terms](#23-capitalizing-compound-words-and-common-terms)
    - [2.4 General Naming Conventions](#24-general-naming-conventions)
        - [2.4.1 Word Choice](#241-word-choice)
        - [2.4.2 Using Abbreviations and Acronyms](#242-using-abbreviations-and-acronyms)
    - [2.5 Names of Assemblies and DLLs](#25-names-of-assemblies-and-dlls)
    - [2.6 Names of Namespaces](#26-names-of-namespaces)
        - [2.6.1 General rules](#261-general-rules)
        - [2.6.2 Namespaces and Type Name Conflicts](#262-namespaces-and-type-name-conflicts)
    - [2.7 Names of Classes, Structs, and Interfaces](#27-names-of-classes-structs-and-interfaces)
        - [2.7.1 Names of Generic Type Parameters](#271-names-of-generic-type-parameters)
        - [2.7.2 Naming Enumerations](#272-naming-enumerations)
    - [2.8 Names of Type Members](#28-names-of-type-members)
        - [2.8.1 Names of Methods](#281-names-of-methods)
        - [2.8.2 Names of Property](#282-names-of-property)
        - [2.8.3 Names of Events](#283-names-of-events)
        - [2.8.4 Names of Fields](#284-names-of-fields)
     - [2.9 Naming Resources](#29-naming-resources)
- [3. Layout and Indentation](#3-layout-and-indentation)
- [4. Methods](#4-methods)
- [5. Exceptions](#5-exceptions)
    - [5.1 Exception Throwing](#51-exception-throwing)
    - [5.2 Exception Handling](#52-exception-handling)
    - [5.3 Exceptions and Performance](#53-exceptions-and-performance)
        - [5.3.1 Tester-Doer Pattern](#531-tester-doer-pattern)
        - [5.3.2 Try-Parse Pattern](#532-try-parse-pattern)
- [6. Logging](#6-logging)
- [7. Code Comments](#7-code-comments)
- [8. String Manipulation](#8-string-manipulation)
- [9. Unit Test](#9-unit-test)
- [10. Miscellaneous](#10-miscellaneous)

<!-- /TOC -->

## 1. Purpose

- Develop reliable and maintainable application code.
- The naming conventions, coding standards and best practices described in this document are compiled from StudioX developers own experiences and by referring to Microsoft guidelines.


## 2. Naming
### 2.1 Casing Style

- Pascal Casing: The first letter in the identifier and the first letter of each subsequent concatenated word are capitalized. You can use Pascal case for identifiers of three or more characters. For example: BackColor, FrontColor.
- Camel Casing: The first letter of an identifier is lowercase and the first letter of each subsequent concatenated word is capitalized. For example: backColor, foreColor
- Uppercase: All letters in the identifier are capitalized. For example: IO, DB.

### 2.2 Capitalization Rules for Identifiers

- **DO** use Pascal casing for all public member, type, and namespace names consisting of multiple words.
- **DO** use Camel casing for parameter names.

<table>
<tr>
  <th>Identifier</th><th>Casing</th><th>Example</th>
</tr>
<tr>
  <td>Namespace</td>
  <td>Pascal</td>
  <td>namespace StudioX.CodingStandard {....}</td>
</tr>
<tr>
  <td>Type</td>
  <td>Pascal</td>
  <td>public class BinaryStreamWriter {....}</td>
</tr>
<tr>
  <td>Interface</td>
  <td>Pascal</td>
  <td>public interface IStreamWriter {....}</td>
</tr>
<tr>
  <td>Method</td>
  <td>Pascal</td>
  <td>
    <pre>public class BinaryStreamWriter 
{
    public void Write(byte[] data)  {....}
}</pre>
  </td>
</tr>
<tr>
  <td>Property</td>
  <td>Pascal</td>
  <td>
    <pre>public class Stream 
{
    public long Length  { get; }
}</pre>
  </td>
</tr>
<tr>
  <td>Event</td>
  <td>Pascal</td>
  <td>
    <pre>public class Process 
{
    public EventHandler Existed;
}</pre>
  </td>
</tr>
<tr>
  <td>Public Field</td>
  <td>Pascal</td>
  <td>
    <pre>public class MessageQueue
{
    public static readonly TimeSpan Timeout;
}</pre>
  </td>
</tr>
<tr>
  <td>Private Field</td>
  <td>Camel</td>
  <td>
    <pre>public class MessageQueue
{
    public Queue&lt;Message&gt; internalQueue;
}</pre>
  </td>
</tr>
<tr>
  <td>Constant</td>
  <td>Pascal</td>
  <td>
    <pre>public class MessageQueue
{
    public const int MaxQueueLength = 500;
}</pre>
  </td>
</tr>
<tr>
  <td>Enum</td>
  <td>Pascal</td>
  <td>
    <pre>public enum FileMode
{
    CreateNew,
    Append,
    ...
}</pre>
  </td>
</tr>
<tr>
  <td>Parameter</td>
  <td>Camel</td>
  <td>
    <pre>public class Converter
{
    public int ToInt32(string value) {...}
}</pre>
  </td>
</tr>
</table>

### 2.3 Capitalizing Compound Words and Common Terms

- **DO NOT** capitalizes each word in so-called closed-form compound words. For example: use endpoint, Endpoint, not EndPoint, nor endPoint.

| Pascal | Camel | Not |
| --- | --- | --- |
| BitFlag | bitFlag | Bitflag |
| Callback | callback | CallBack |
| Email | email | EMail |
| FileName | fileName | Filename |
| Hashtable | hashtable | HashTable |

### 2.4 General Naming Conventions

- **DO** use self-explanatory names for everything (interfaces, classes, methods, variables etc.)
- **DO NOT** sacrifice length for clarity. Long but communicative names are much better than short but convoluted names.

#### 2.4.1 Word Choice

- **DO** choose easily readable identifier names. For example, a property named HorizontalAlignment is more English-readable than AlignmentHorizontal.
- **DO** favor readability over brevity. The property name CanScrollHorizontally is better than ScrollableX (an obscure reference to the X-axis).
- **DO NOT** use underscores, hyphens, or any other non-alphanumeric characters.
- **DO NOT** use Hungarian notation, e.g. bConfirm, iCount.
- **CONSIDER** prefix Boolean variables and properties with &quot;can&quot;, &quot;is&quot; or &quot;has&quot;. Example:
```csharp
  public class Command
  {
    private bool canExecute = false;
    
    public bool CanExecute { get; }
    
    public bool HasExecute { get; }
  }
```

- Do not include the parent class name within a property name. Example:
```csharp
  public class Customer
  {
    // DO
    public string Address { ... }
    
    // DO NOT
    public string CustomerAddress {...}
  }
```

- **AVOID** using identifiers that conflict with keywords of widely used programming languages. Uses the **@** sign as an escape mechanism in this case, for example @class, @dynamic. However, it is still a good idea to avoid common keywords because it is much more difficult to use a method with the escape sequence than one without it.

#### 2.4.2 Using Abbreviations and Acronyms

- **DO NOT** use abbreviations or contractions as part of identifier names. For example, use GetWindow rather than GetWin.
- **DO NOT** uses any acronyms that are not widely accepted, and even if they are, only when necessary.
- **DO** use a generic CLR type name, rather than a language-specific name, in the rare cases when an identifier has no semantic meaning beyond its type.
```csharp
  // DO 
  long ConvertToInt64(object value)
  
  // DO NOT
  long ConvertToLong(object value)
```

- **DO** use a common name, such as value or item, rather than repeating the type name, in the rare cases when an identifier has no semantic meaning and the type of the parameter is not important.
```csharp
  // DO 
  long ConvertToInt64(object value)
  
  // DO NOT
  long ConvertToInt64(object valueObject)
```

### 2.5 Names of Assemblies and DLLs

- **DO** choose names for your assembly DLLs that suggest large chunks of functionality, such as System.Data, System.IO.
- **CONSIDER** name DLLs according to the following pattern: &lt;Company&gt;.&lt;Component&gt;.dll where &lt;Component&gt; contains one or more dot-separated clauses. For example: Web.Controls.dll

### 2.6 Names of Namespaces

#### 2.6.1 General rules

- **DO** follow the template : &lt;Company&gt;.(&lt;Product&gt;|&lt;Technology&gt;)[.&lt;Feature&gt;][.&lt;Subnamespace&gt;]. For example: StudioX.Security.Authentications.
- **DO** prefix namespace names with a company name to prevent namespaces from different companies from having the same name.
- **DO NOT** use organizational hierarchies as the basis for names in namespace hierarchies, because group names within corporations tend to be short-lived. Organize the hierarchy of namespaces around groups of related technologies.
- **DO** use Pascal casing, and separate namespace components with periods (e.g., QualityAssurance.qTest). If your brand employs nontraditional casing, you should follow the casing defined by your brand, even if it deviates from normal namespace casing (e.g. use qTrace instead of QTrace or Qtrace).
- **CONSIDER** using plural namespace names where appropriate. For example, use Collections instead of Collection. Brand names and acronyms are exceptions to this rule, however. For example, use IO instead of IOs.
- **DO NOT** use the same name for a namespace and a type in that namespace.

#### 2.6.2 Namespaces and Type Name Conflicts

- **DO NOT** introduce generic type names such as Element, Node, Log, and Message. You should qualify the generic type names (FormElement, XmlNode, EventLog, SoapMessage).
- **DO NOT** give the same name to types in namespaces within a single application model.

### 2.7 Names of Classes, Structs, and Interfaces

- **DO** name classes and structs with nouns or noun phrases, using Pascal casing.
- **DO** prefix interface names with the letter I, to indicate that the type is an interface.
- **DO** name interfaces with adjective phrases, or occasionally with nouns or noun phrases.
```csharp
  public interface IExecutable {...}
  public class Command : IExecutable {...}
```

- **DO NOT** give class names a prefix (e.g., &quot;C&quot;).
- **CONSIDER** ending the name of derived classes with the name of the base class. Example:
```csharp
  public abstract class Repositoty {...}
  public sealed class EmployeeRepository : Repositoty {...}
```

#### 2.7.1 Names of Generic Type Parameters

- **CONSIDER** using T as the type parameter name for types with one single-letter type parameter.
```csharp
  public int IComparer<T> {...}
  public delegate bool Predicate<T>(T item);
  public struct Nullable<T> where T:struct {...}
```

- **DO** prefix descriptive type parameter names with T.
```csharp
  public interface ISessionChannel<TSession> 
    where TSession : ISession {...}
```

#### 2.7.2 Naming Enumerations

- **DO** use a singular type name for an enumeration unless its values are bit fields.
```csharp
  public enum UserRole
  {
    Guest,
    Subsriber,
    Administrator
  }
  [Flags]
  public enum Permissions
  {
    Read = 0,
    Write =1
  }
```

- **DO NOT** use a prefix on enumeration value names (e.g., &quot;ad&quot; for ADO enums, &quot;rtf&quot; for rich text enums, etc.).

### 2.8 Names of Type Members
#### 2.8.1 Names of Methods

- **DO** give methods names that are verbs or verb phrases.
```csharp
  public class String
  {
    public int CompareTo(...){...}
    public string[] Split(...) {...}
    public string Trim() {...}
  }
```

- DO suffix asynchronous method name by &quot;Async&quot;
```csharp
  private static async Task FooAsync()
  {
    await Task.Delay(1000);
    Console.WriteLine("Done with first delay");
    await Task.Delay(1000);
  }
```

#### 2.8.2 Names of Property

- **DO** name properties using a noun, noun phrase, or adjective.
- **DO NOT** have properties that match the name of &quot;Get&quot; methods as in the following example:
```csharp
  public string Body { get;set }
  public string GetBody() {....}
```
- **DO** name collection properties with a plural phrase describing the items in the collection instead of using a singular phrase followed by &quot;List&quot; or &quot;Collection&quot;.
```csharp
  // DO
  public ICollection<Person> Persons { get;set; }
  // DO NOT
  public ICollection<Person> PersonCollection { get;set; }
```

#### 2.8.3 Names of Events

- **DO** name events with a verb or a verb phrase. For example: Clicked, Painting, DroppedDown.
- **DO** give events names with a concept of before and after, using the present and past tenses.
- **DO NOT** use &quot;Before&quot; or &quot;After&quot; prefixes or postfixes to indicate pre- and post-events. Use present and past tenses as just described.

#### 2.8.4 Names of Fields

- **DO** name fields using a noun, noun phrase, or adjective.


### 2.9 Naming Resources

- **DO** use Pascal casing in resource keys.
- **DO** use only alphanumeric characters and underscores in naming resources.
- **DO** use the following naming convention for exception message resources: &lt;ExceptionType&gt;&lt;SpecificError&gt;. For example: ArgumentExceptionIllegalCharacters, ArgumentExceptionInvalidName.

## 3. Layout and Indentation

- **DO** use 4 whitespaces for each nested level of code.
- **DO NOT** nest code any more than 3 levels of depth.
- **DO** use one blank line to separate blocks of code.
- **CONSIDER** break single long line of code to multiple lines of code with level indentations.
```csharp
  using <ReferenceNamespacesAndAlias>
  namespace <Namespace>
  {
    public class <ClassName>
    {
      public void Method()
      {
        // Method content
      }
      
      public void MethodWithManyParameters(
          string <parameter1>,
          string <parameter2>,
          long <parameter3>,
          bool <parameter4>)
        {
           // Method content
        }
    }
  }
```


## 4. Methods

- **DO** write methods which do one and only one job.
- **AVOID** methods which have more than 30 lines of code.
- Public methods must validate their input arguments. Use the prescribed Design By Contract (DBC) library to perform such validation. For example:
```csharp
  public ICollection<Person> SearchPersons(string firstName, string lastName)
  {
    // Do validate input parameter
    if(string.IsNullOrEmpty(firstName))
      throw new ArgumentNullException("firstName");
    if(string.IsNullOrEmpty(lastName))
      throw new ArgumentNullException("lastName"); 
    
    // Do actual method logic  

  }
```

- **AVOID** writing methods accepting any more than 5 parameters. Consider use a class or struct to wrap those parameters instead.
```csharp
  // DO NOT
  public ICollection<Person> SearchPerson(
    string firstName,
    string lastName,
    DateTime? dateOfBirth,
    string email,
    bool isActive,
    bool hasChild)
  {
    ...
  }
  // DO 
  public ICollection<Person> SearchPerson(SearchPersonCriteria criteria)
  {
    ...
  }
```

- DRY (Don&#39;t Repeat Yourself). That is NEVER allowing duplication in code. Refactor duplicated code into new methods of same or different class.
- **DO** return empty collection instead of null.
- To return (or receive) data as collection of objects, use interface (IEnumerable&lt;T&gt; , ICollection&lt;T&gt;, IList&lt;T&gt;, ..) instead of concrete class. Prefer using ICollection&lt;T&gt; for common case.
```csharp
  // DO 
  public IList<Person> GetAllPersons() {...}
  // DO NOT
  public List<Person> GetAllPersons() {...}
```
## 5. Exceptions
### 5.1 Exception Throwing

- **DO** report execution failures by throwing exceptions.
- **DO NOT** return error codes.
```csharp
  // DO NOT 
  public void Execute(out int errorCode)
  {
    // Case 1 failed
    errorCode = 100;
    ...
    // Case 2 failed 
    errorCode = 200;
    ...
    // Success
    errorCode = 0;
  }
  // DO 
  public void Execute()
  {
    // Case 1 failed
    throw new ABCException("Case 1 failed");
    ...
    // Case 2 failed 
    throw new CDEException("Case 2 failed");
    ...
    // Success
    ...
  }
```

- **DO NOT** use exception as a flow control structure. Exceptions are for exceptional cases only.
```csharp
  // DO NOT 
  public void Execute()
  {
    try
    {
      // Execute normal case 
      ...
      // If failed 
      throw new ABCException();
    }
    catch(ABCException)
    {
      // Execute alternative case
      ...
    }
  }
```

- **DO** throw the most specific exceptions which match the current level of abstraction. For examples:

- Do not throw [SqlException](https://www.assembla.com/wiki/show/pe_gameworld/SqlException) to the GUI because that makes the GUI depends on the low-level implementation details. Throw a high-level exception like [InsufficientBalance](https://www.assembla.com/wiki/show/pe_gameworld/InsufficientBalance) instead
- Never throw Exception. Use a more specific exception (either custom-built or built-in) instead.

- **DO NOT** throw or derive from ApplicationException, use Exception instead. It was originally thought that custom exceptions should derive from the ApplicationException class; however in practice this has not been found to add significant value.
- **DO NOT** give error messages like &quot;Error in Application&quot;, &quot;There is an error&quot; etc. Instead give specific messages like &quot;Failed to update database. Please make sure the login id and password are correct&quot;.
- **DO** show short and friendly message to the user. But log the actual error with all possible information. This will help a lot in diagnosing problems.
- **DO** not put critical information in the message field of exception objects.
- **DO NOT** use throw ex, instead use throw to rethrow an exception to avoid the call stack from being erased.
```csharp
  public void X()
  {
    try
    {
      ...
    }
    catch(Exception ex)
    {
      // DO 
      throw;

      //DO NOT
      throw ex;

      //DO NOT 
      throw new ABCException(ex);
    }
  }
```


### 5.2 Exception Handling

- **DO NOT** declare an empty catch block.
```csharp
  // DO NOT 
  try
  {
    ...
  }
  catch
  {
    // DO NOTHING
  }
```

- **DO** only use the finally block to release resources from a try statement.
```csharp
  // DO NOT 
  try
  {
    // Open database connection 
    dbConnection.Open();
  }
  catch
  {
    dbConnection.Close();
  }

  // DO 
  try
  {
    // Open database connection 
    dbConnection.Open();
  }
  catch
  {
    // Log exception
  }
  finally
  {
    // This code block is executed for both case of success or failure.
    // Release connection.
    dbConnection.Close();
  }
```
- **DO** catch and handle exceptions (like logging) as late in the call stack as possible, unless a lower level module can catch and do something meaningful about the exception.
- **DO** define a global exception handling policy to intercept all exceptions not caught by low-level modules.
- **NEVER** swallow exceptions. There should always be some indication that an exception occurred. Log trace of the exception is the bare minimum.
- **DO** use using block as a short-hand for the try-finally pattern with IDisposable object.
```csharp
  // DO 
  using (var dbConnection = new DBConnection())
  {
    dbConnection.Open();
    ...
    // Do not need to explicitly release resource.
  }
```

### 5.3 Exceptions and Performance

- **CONSIDER** the performance implications of throwing exceptions. Throw rates above 100 per second are likely to noticeably impact the performance of most applications.

To improve performance, it is possible to use either the Tester-Doer Pattern or the Try-Parse Pattern as described below:

#### 5.3.1 Tester-Doer Pattern

- **CONSIDER** the Tester-Doer Pattern for members that might throw exceptions in common scenarios to avoid performance problems related to exceptions.
```csharp
  ICollection<int> numbers = ...
  if( numbers != null && !numbers.IsReadOnly ) // Tester
  {
    numbers.Add(1); //Doer
  }
```

#### 5.3.2 Try-Parse Pattern

- **CONSIDER** the Try-Parse Pattern for members that might throw exceptions in common scenarios to avoid performance problems related to exceptions.
- **DO** use the prefix &quot;Try&quot; and Boolean return type for methods implementing this pattern.
- **DO** provide an exception-throwing member for each member using the Try-Parse Pattern.
```csharp
  public struct DateTime
  {
    public static DateTime Parse(string dateTime)
    {
      ...
    }
    public static bool TryParse(string dateTime, out DateTime result)
    {
      ...
    }
  }
```


## 6. Logging

- **DO** use Logger class for logging all error, warning, and traces.
- **DO** use the logger class extensively throughout the code to record errors, warning and even trace messages that can help you trouble shoot a problem.
- **DO** log the actual error with all possible information (e.g. parameters, SQL statement, file data). This will help a lot in diagnosing problems.
- **AVOID** log the critical information (e.g. credit card number, SSN).Consider encrypt critical information in log if the information logging is required.

## 7. Code Comments

- **DO** use // or /// but never /\* ..\*/ or &quot;flowerbox&quot; comment.
```csharp
  // ***********************************
  // This is a bad code comment format
  // ***********************************

  /* This is another bad code comment format */
  
  // This is good code comment format
  ///<summary>
  /// This is event better code comment format.
  ///<summary>
```

- **DO** add comments only when they make sense, don&#39;t add comments for the sake of having some comments. Bad and/or redundant comments are much worse than no comment at all.
```csharp
  // This is code presents the redundant code comment 
  // The window.Open() is to self-describe what it does.
  public void Execute()
  {
    var window = new Window();

    // Open window 
    window.Open();
  }
```

- **DO** write comments which describe what the code does and/or whyit does that, not how the code works.

- Only describe the how when there are inevitable complicated code like multithreading. On other occasions, if the code is too complicated to understand without lots of comment, chance is that the code is poorly written and should be refactored.

- **DO** use English for all code comments.
- **DO** add comments indicating what changes were made and optionally why, when checking in code into Source Control System (SCS).
- **DO** remove unused code from the source file instead of commenting it out.
- **DO** use // TODO: comment to indicate unfinished tasks.
- **DO** use // HACK: comment to indicate any shortcuts taken in the implementation which need to be fixed or improved later.
- **CONSIDER** usually walk throught //TODO comment to complete the unfinished tasks and remove it after completed.

## 8. String Manipulation

- **DO** use [StringBuilder](https://www.assembla.com/wiki/show/pe_gameworld/StringBuilder) whenever multiple concatenations are required.

```csharp
  // DO 
  var queryBuilder = new StringBuilder();
  queryBuilder.AppendLine("SELECT * FROM dbo.Employees");
  queryBuilder.AppendFormat("WHERE FirstName == N'{0}'", firstName);
  ...
  // DO NOT 
  var query = string.Empty;
  query = query + "SELECT * FROM dbo.Employees" + " " ;
  query = query + "WHERE FirstName = N'" + firstName + "'";
  ...

```

- **DO** use string formatting technique to parameterize strings.

```csharp
  // DO 
  var fullName = string.Format("{0} {1}",firstName,lastName);

  // DO NOT
  var fullName = firstName + " " + lastName;

```

- **DO** use string.Empty instead of &quot;&quot;.
```csharp
  // DO 
  var title = string.Empty;

  // DO NOT 
  var tile = "";
```

- **CONSIDER** use the &quot;@&quot; prefix for string literals instead of escaped strings.
```csharp
  // DO
  @"c:\temp"
  // DO NOT 
  "c:\\temp"
```

- **DO** use string. [IsNullOrEmpty](https://www.assembla.com/wiki/show/pe_gameworld/IsNullOrEmpty)()/string.IsNullOrWhitespaces() to detect null or empty string/whitespace.
- **DO** be aware of case sensitive in string comparison. This will ensure the string will match even if the string being compared has a different case.

```csharp 
  string a = ...
  string b = ...
  if( string.Equals(a, b, StringComparison.InvariantCultureIgnoreCase))
  {
    ...
  }
```
## 9. Unit Test

- Although not required, it is recommended that test code is written before production code (i.e. test-first approach). Whether test-first or test-last is applied, never delay the act of writing test code.
- Write one or more unit test cases to reproduce any defect found by QA team.
- Follow these principles when writing unit test code

- **Automatic:** The whole testing process must be automated. Do not rely on any manual process such as data population, environment configuration etc. Test code must do all those things.
- **Complete:** Test anything that can possibly break. When you are in doubt whether something can possibly go wrong or not, write a test.
- **Repeatable:** All test cases must be able to run and rerun repeatedly and produce the same result every time. If it doesn&#39;t, they are not reliable and must be fixed.
- **Independent:** Each test case must be configured and run in isolation from one another. Do not make any assumption that one test must be executed before another.
- **Production-like:** Test code must be treated like production code and subject to strict review. That means each and every coding convention in this document is very well applicable to test code.
- **Fast:** Test cases must run fast. If they do not, mock out the heavy dependencies (like database) to make them run fast.

## 10. Miscellaneous

- Use foreach-style loop instead of for loop when possible.

```csharp
  // DO
  foreach( var person in persons)
  {
    ...
  }

  // DO NOT  
  for (int index=0; index < persons.Count(); index++)
  {
    var person = person[0];
    ...
  }

```
- A switch statement must always contain a default branch which handles unexpected cases.

```csharp
  switch (accessMode)
  {
    case FileAccess.Read:
      ...
      break;
    case FileAccess.Write: 
      ...
      break;
    default:
      throw new NotSupportedException();
  }
```

- Never, ever, use a magic number/string.

```csharp
  // DO 
  const int MaxCount = 300;
  if(totalCount > MaxCount)
  {
    ...
  }

  // DO NOT 
  if(totalCount > 300)
  {
    ...
  }
```

- Use prescribed tools to add loggingcode throughout the application to facilitate debugging.
- Consider using AOP to inject logging code when applicable.
- Fix all issuesreported by static analysis tool(s). An issue can be waived with the authority of Team Lead or Technical Lead.
- Always check Event &amp; Delegate instances for null before invoking.

 ```csharp
    public class Window
    {
      public EventHandler Opening { get;set; }
      public void DoSomething()
      {
        ...
        if(Opening != null)
        {
          Opening(this, new EventArgs());
        }
      }
    }
 ```

- Do not omit access modifiers. Explicitly declare all identifiers with the appropriate access modifier instead of allowing the default.

```csharp
  // DO NOT
  class Window
  {
    string title;
    int width;
    int height;
  } 
  // DO 
  internal class Window
  {
    private string title;
    private int width;
    private int height;
  }
```

- Do not hardcode text in UI. Use resource files.
- Never hardcode a path or drive name in code. Get the application path programmatically and use relative path.
- Never assume that your code will run from drive &quot;C:&quot;. You may never know, some users may run it from network or from a &quot;Z:&quot;.
- In the application start up, do some kind of &quot;self-check&quot; and ensure all required files and dependencies are available in the expected locations. Check for database connection in start-up, if required. Give a friendly message to the user in case of any problems.
- If a wrong value found in the configuration file, application should throw an error or give a message and also should tell the user what are the correct values.
- Avoid having very large files. If a single file has more than 1000 lines of code, it is a good candidate for refactoring. Split them logically into two or more classes.

