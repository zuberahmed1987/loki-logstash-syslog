# Loki Stack (Filebeat, logstasha and syslog)

This chart is to store logs in loki and also send the logs for SIEM server via syslog, There is no integration of Loki with SIEM servers. It is a example implementation of Loki with SIEM Tool(syslog enabled) at same time.

## Example Configuration `loki-syslog.yaml`
This configuration collected all logs by default, few namespaces are excluded as an example.

## Example Configuration `loki-syslog-autodiscover.yaml`

The configuration in `loki-syslog-autodiscover.yaml` is based on filebeat autodiscovery and hints(enabled). In this configuration logs will be collected with the help of annotations on pod as well as namespace, by default no logs will be collected. You can enable log collected of complete namespace or pod by setting up annotation. Namespace level settings can override with pod annotations.


In both configuration logs will be send on the basis of namespace label `siem`, if it is set to `enabled`
These configurations can be changed as per the usecase.

## Annotations for pod and namespaces

### Annotation to enable log collection of pod or namespace
```yaml
annotations:
  co.elastic.logs/enabled: 'true'
```

### Multiline Java logs
```yaml
annotations:
  co.elastic.logs/enabled: 'true'
  co.elastic.logs/multiline.pattern: '^[[:space:]]+(at|\.{3})[[:space:]]+\b|^Caused by:'
  co.elastic.logs/multiline.negate: false
  co.elastic.logs/multiline.match: after
  # if delay to long or log to long，add these options
  co.elastic.logs/multiline.timeout: 120s #default 5s
  co.elastic.logs/multiline.max_lines: 1000 #default 500
```
Here’s a Java stack trace that presents a slightly more complex example:
```java
Exception in thread "main" java.lang.IllegalStateException: A book has a null property
       at com.example.myproject.Author.getBookIds(Author.java:38)
       at com.example.myproject.Bootstrap.main(Bootstrap.java:14)
Caused by: java.lang.NullPointerException
       at com.example.myproject.Book.getId(Book.java:22)
       at com.example.myproject.Author.getBookIds(Author.java:35)
       ... 1 more
```
