---
layout: post
title: "Can’t figure out how to implement a custom IDataReader to my collection"
description: ""
category: ""
tags: []
---
{% include JB/setup %}

I hope someone can help me here... I've been working on this for 4 days now with barely any luck.

Here's the question:

I know it is possible to create a custom datareader (inferring from the IDataReader interface) which accesses the data in a collection. I've seen it used in other third-party controls and am wanting to do it myself. I've come across an ancient (2004) website of how a guy explains how to do it (<a href="http://blogs.msdn.com/yvesdolc/archive/2004/11/08/254209.aspx">http://blogs.msdn.com/yvesdolc/archive/2004/11/08/254209.aspx</a>) but I am having difficulty implementing his code since he did not provide examples and 2004 C#/.NET2.0 might not be as performance-tuned as the latest and great C#/.NET3.5. Can anyone assist me in either providing some samples on how to do this or providing some sources that can teach me how to do this. I'm googled up and down on a tutorial on how to write a custom datareader but everything I find isn't very helpful... it either lists code that's already complete without good information of how they got there or has code that doesn't do what I need it to do.

Just to make it easy, I've included an example collection in the code so that, if examples are provided, they can reference it.

NOTE: Just an additional item, if this can be generic-ized in a way to support different types of collections, that's a huge plus!

```csharp
public class Person
{
     public int ID {get; set;}

     public string Name {get; set;}

     public string Gender {get; set;}

     public Person()
     {

     }

     public Person (int id, string name, string gender)
     {

          ID = id;
          Name = name;
          Gender= gender;
     }
}

public class People : List<Person>
{
     public People { };
}

 
public void Main()
{
     Person person1 = new Person(1, "John Doe", "Male");
     Person person2 = new Person(2, "Jane Smith", "Female");
     Person person3 = new Person(3, "Tom White", "Male");

     People peeps = new People();

     peeps.Add(person1);
     peeps.Add(person2);
     peeps.Add(person3);

}
```

UPDATE (10/29/2009): Well, I figured out a way to get his code and it was well worth the effort as I noticed an increase in performance (as well as a significant decrease in MEM usage) when using his datareader over converting to a datatable. I'm busy coding away at it and I having yet figured out how to keep it as generic as I'd like but his code works well for now. I'll post the solution (using his code) at a later date so everyone can see. It's actually quite simple....