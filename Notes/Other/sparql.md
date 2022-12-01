Here's some other queries I made that don't fit in the above because they work but I barely understand them myself but they might contain wisdom somewhere

```sql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
prefix mo: <http://purl.org/ontology/mo/>
prefix dc: <http://purl.org/dc/elements/1.1/>


SELECT ?title (SUM(?duration)/1000/60 AS ?total_duration_in_min) {
  ?record a mo:Record;
    dc:title ?title;
    mo:track ?track.
  ?track mo:duration ?duration.
}
GROUP BY ?title
HAVING((SUM(?duration)/(1000.0*60.0)) < 60)
ORDER BY DESC(?total_duration_in_min)
LIMIT 10
```
(Thanks Claire, Riad and Niels for dealing with my spam about this)