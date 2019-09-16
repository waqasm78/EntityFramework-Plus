# Audit

## Introduction

Entity Framework Core saves entities in a database but doesn't let you easily track changes, for example, a history of all modifications and their author in an audit table.

**EF+ Audit** easily tracks changes, exclude/include entity or property and auto save audit entries in the database.


{% include template-example.html %} 
```csharp

// using Z.EntityFramework.Plus; // Don't forget to include this.

var ctx = new EntityContext();
// ... ctx changes ...

var audit = new Audit();
audit.CreatedBy = "ZZZ Projects"; // Optional
ctx.SaveChanges(audit);

// Access to all auditing information
var entries = audit.Entries;
foreach(var entry in entries)
{
    foreach(var property in entry.Properties)
    {
    }
}

```
[Try it](https://dotnetfiddle.net/dc7v3W)

## Scenarios

 - [AutoSave](/audit-autosave)
 
## Limitations

  - **DO NOT** support relationship
  - **DO NOT** populate EntitySetName value

## Requirements

 - **EF+ Audit:** Full version or Standalone version
 - **Database Provider:** All supported
 - **Entity Framework Core Version:** EFCore 1.0+
 - **Minimum Framework Version:** .NET Core 1.0

## Troubleshooting

Why only my key is added when updating my entity?

This issue often happens for MVC user. They create a new entity through HttpPost values and force the state to "Modified", the context is not aware of the original value and use the current value instead. So, every property has the original value == current value and our auditing only log the key since all other values are equals.

We recommend setting the **IgnorePropertyUnchanged **to false to log every property.

Here is an example of this issue: [Issues #8](https://github.com/zzzprojects/EntityFramework-Plus/issues/8)

## Conclusion

**Auditing** in Entity Framework Core could not be simpler, there are always some entities in an application where an audit table can be crucial to keep track of what's happening, and you now have access to an easy to use library for these situations.

Need help getting started? [info@zzzprojects.com](mailto:info@zzzprojects.com)

We welcome all comments, ideas and suggestions to improve our library.