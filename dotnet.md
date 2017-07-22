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
