Nutch Htmlunit Plugin
==============

### Introduction

According to the implementation of [Apache Nutch](http://nutch.apache.org/) 1.7, we can't get dynamic HTML information from fetch pages including AJAX requests as it will ignore all AJAX requests.

This plugin will use [Htmlunit](http://htmlunit.sourceforge.net/) to fetch whole page content with necessary dynamic AJAX requests. 
It developed and tested with Apache Nutch 1.7, you can try it on other Nutch version or refactor the source codes as your design.

### Quick Start

* Using ivy or maven or manually to copy htmlunit dependencies to your apache-nutch-1.7/lib, please refer: http://htmlunit.sourceforge.net/dependencies.html

* Copy runtime/local/plugins/* to your apache-nutch-1.7/plugins

* Change your apache-nutch-1.7/conf/nutch-site.xml to use this plugin 'protocol-htmlunit', as below sample:

```

<property>
  <name>plugin.includes</name>
  <value>protocol-htmlunit|urlfilter-regex|parse-...</value>
  <description>Regular expression naming plugin directory names to
  include.  Any plugin not matching this expression is excluded.
  In any case you need at least include the nutch-extensionpoints plugin. By
  default Nutch includes crawling just HTML and plain text via HTTP,
  and basic indexing and search plugins. In order to use HTTPS please enable 
  protocol-httpclient, but be aware of possible intermittent problems with the 
  underlying commons-httpclient library.
  </description>
</property>

```

* Optionally, you can config apache-nutch-1.7/conf/regex-urlfilter.txt to control htmlunit only fetch specified urls including internal AJAX request. 
See detail: https://github.com/xautlx/nutch-htmlunit/blob/master/src/plugin/lib-htmlunit/src/java/org/apache/nutch/protocol/htmlunit/RegexHttpWebConnection.java

* That's all. Now you can execute: apache-nutch-1.7/bin/nutch crawl urls, and see page contents parsed by htmlunit.
