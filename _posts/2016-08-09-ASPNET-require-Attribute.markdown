---
layout: post
title: ASP.NET [require] 보안.
---

gzak

~~~
Because value types are non-nullable, they are assigned a default value during model binding. So for instance, if you have a Birthday property of type DateTime which is required on your model, and a date isn't supplied in the data posted to the controller, it will be assigned the value of default(DateTime).

At that point, it's too late for model validation to enforce the [Required] attribute on that property, because even default(DateTime) counts as a value and therefore passes the [Required] validator.

One way to handle this is to run model binding in two phases, one pre-phase which only resolves where in the model each posted property will go (along with the validation attributes on the model at that destination), then a post-phase which does the actual assignment. In between, you can run the model validation on the posted object directly, with the validation information coming from the model based on the pre-phase.
~~~

dougbu

~~~
Use the framework-specific [BindRequired] attribute to ensure a value was included in the submission. (MVC pretty much calls IsValid()on ValidationAttributes and does not reinterpret the results.)

FYI the System.ComponentModel.DataAnnotations namespace is part of CoreFx. You can find relevant sources at https://github.com/dotnet/corefx/tree/master/src/System.ComponentModel.Annotations/src/System/ComponentModel/DataAnnotations or file issues at https://github.com/dotnet/corefx/issues.
~~~

gzak

~~~
Is that supposed to be used in conjunction with the regular [Required] attribute? Or does this replace it? FWIW, I just tried using the [BindRequired] attribute, and TryValidateModel still returns true.

What might be happening is that since I'm posting the object from C# in an integration test, and in the C# class it's a value type, it gets submitted with a default value in the request. Which means for C# integration tests at least, there's no way to test for missing properties (at least, not without writing a custom serializer or else posting a hard-coded invalid JSON string).

Let me know if I'm missing something here.
~~~

dougbu

~~~
[BindRequired] affects model binding only and that comes before validation. So nothing will change for your integration test around TryValidateModel(). However a real action will see errors in the ModelStateDictionary if a property with [BindRequired] is not bound (aka no data is provided for it).

used in conjunction with the regular [Required] attribute? Or does this replace it?
The two attributes serve different purposes and should be used however your application requires. If the application needs to confirm data was submitted, use [BindRequired]. If the application needs to confirm a value is not null, use [Required].
~~~

gzak

~~~
Nope, my hypothesis is false. I just tried posting an object of anonymous type with only a subset of the model's fields, so there's no way it could have filled in defaults for them. On the receiving end, TryValidateModel still returned true.
~~~

dougbu

~~~
TryValidateModel() does not model bind and [BindRequired] is not relevant if that's all you're doing. Either add a parameter to your action with the type i.e. do model binding automatically or call TryUpdateModelAsync()
~~~

gzak

~~~
I believe my action already has a parameter with the type, so model binding should be happening automatically. Something like this:

[HttpPost]
public async Task Post(MyModel m) { ... }
If I omit the properties of MyModel which are marked with the [BindRequired] attribute, the action is still invoked and m has defaults filled in.

I think I'm missing something here...
~~~

dougbu

~~~
In the scenario you're describing, there's no need to call TryValidateModel(). Check ModelState.IsValid and it should be false if no data is provided for the [BindRequired] properties.
~~~

gzak

~~~
Aha, perfect, that was exactly my problem. Thank you!
~~~

[참고 github](https://github.com/aspnet/Mvc/issues/4211)
