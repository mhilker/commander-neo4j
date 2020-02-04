# Commander Neo4j

## Create constraints for import
```
CREATE CONSTRAINT ON (e:Event) ASSERT e.event_id IS UNIQUE
```

## Import events
```
LOAD CSV WITH HEADERS FROM 'file:///correlating_events.csv' AS line
CREATE (event:Event {
    event_id: line.event_id,
    correlation_id: line.correlation_id,
    causation_id: line.causation_id,
    aggregate_id: line.aggregate_id,
    topic: line.topic
})
```

```
LOAD CSV WITH HEADERS FROM 'file:///correlating_events.csv' AS line
MATCH (event:Event {id: line.correlation_id })
MATCH (event:Event {id: line.event_id })
```

## Delete everything 
```
MATCH (n)
DETACH DELETE n
```
