[![Build Status](https://travis-ci.org/sha1n/scala-time.svg?branch=master)](https://travis-ci.org/sha1n/scala-time)

scala-time
==========
This is a small library which provide execution time measurement and reporting design in Scala.

Check out the Demo console app for a full usage example .

Here is a quick example of the core features:

```scala
    // this method is called for each collected time 
    implicit val reporter: ReportSample = yourTimeReportingHandler 
    
    // that name represents the series of execution time samples you're going to collect 
    val seriesName = "Your Action"
    
    // and here is how you hook your method 'yourAction' to the time sampler
    yourAction() withTimeSampleAs seriesName
```  

There are also utility classes for buffered and async sample reporting, that can be composed to provide better performance. Here is how you use them:

```scala
    // Composing a buffered reporter with an async reporter using a single reporting thread
    implicit val bufferedReporter: ReportSample =
        BufferedReporter(bufferSize = 5)
        (AsyncReporter(report = yourTimeReportingHandler, queueCapacity = 10, reporterThreads = 1))
```
Enjoy...
