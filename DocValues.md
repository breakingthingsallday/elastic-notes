DocValues are column data structure to store all values of a particular field in a segment together to facilitate sorting, faceting operations.


DocValues look for a field like 

<doc_id1>: <value1>
<doc_id1>: <value2>

They are binary encoded and depending on data type different compressions techniques are used.

As far as sorting is concerned here's how DocValues help:
1. After search, you have a bunch of doc-ids
2. Luecene will then use DocValues for the field to sort on and get the correspodning values to sort on
3. It also intializes a heap (min/max) and uses a comparator depending on the data type to only get the TOP hits needed
4. The above steps were for each segment in a lucene index
5. Another min/max heap is initialized and results from all the segments are merged to result in final list of documents
