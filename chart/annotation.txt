#Annotations for pod and namespaces

##Annotation to enable log collection of pod or namespace
'''yaml
annotations:
  co.elastic.logs/enabled: 'true'
'''

##Multiline Java logs
'''yaml
annotations:
  co.elastic.logs/enabled: 'true'
  co.elastic.logs/multiline.pattern: '^([0-9]{4}-[0-9]{2}-[0-9]{2})'
  co.elastic.logs/multiline.negate: true
  co.elastic.logs/multiline.match: after
  # if delay to long or log to long，add these options
  co.elastic.logs/multiline.timeout: 120s #default 5s
  co.elastic.logs/multiline.max_lines: 10000 #default 500
'''
