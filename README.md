About
=====================

This is an example of building an immutable architecture. This practice is described in Vladimir Khorikov [Applying Functional Principles in C#][L1] Pluralsight course.

Licence
--------------
[Apache 2 License][L2]


Docs
=====================
[Immutable architecture, Article, Vladimir Khorikov, 2016/05/12]


Update ToDo to the code
=====================
from  [VK comment] to [Immutable architecture, Article, Vladimir Khorikov, 2016/05/12]

> Q:
> In your code in GitHub you only implement tests for the immutable part. This is because you think it is not useful having unit tests for the persistent code or it has just to simplify the code?
> 
> A:
> This code is from my Pluralsight course where I didn't want to shift the focus from the immutability topic and didn't introduce integration tests because of that. I do find them useful, however, and I actually implemented one when I prepared this sample code. Here it is:

```
public class IntegrationTests
{
    [Fact]
    public void Application_service_adds_a_new_record()
    {
        string directory = Environment.CurrentDirectory;
        string logFilePath = Path.Combine(directory, "Audit_1.txt");
        File.WriteAllText(logFilePath, "1;Peter Peterson;2016-04-06T16:30:00");
        var service = new ApplicationService(directory);

        service.AddRecord("Jane Smith", new DateTime(2016, 04, 07, 12, 0, 0));

        string text = File.ReadAllText(logFilePath);
        Assert.Equal("1;Peter Peterson;2016-04-06T16:30:00\r\n2;Jane Smith;2016-04-07T12:00:00\r\n", text);
    }
}
```

  [Immutable architecture, Article, Vladimir Khorikov, 2016/05/12]: <http://enterprisecraftsmanship.com/2016/05/12/immutable-architecture/>
  [L1]: http://pluralsight.com/courses/csharp-applying-functional-principles
  [L2]: http://www.apache.org/licenses/LICENSE-2.0
  [L4]: src/DatabaseUpgradeTool/App.config
  [L5]: src/DatabaseUpgradeTool/Migrations
  [VK comment]: <http://disq.us/p/18xjnd6>
