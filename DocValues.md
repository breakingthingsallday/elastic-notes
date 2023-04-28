DocValues are column data structure to store all values of a particular field in a segment together to facilitate sorting, faceting operations.


DocValues look for a field like 

<doc_id1>: <value1>
<doc_id1>: <value2>

They are binary encoded and depending on data type different compressions techniques are used.

# The sorting process can be divided into the following steps:

* Perform the search: Lucene first performs the search based on the user's query, which results in a set of matching documents.

* Retrieve field values: For each matching document, Lucene retrieves the field value from DocValues storage for the specified sorting field.

* Compare field values: Lucene compares the field values of the documents using the appropriate comparator based on the specified sorting order. For example, if sorting by a numeric field in ascending order, Lucene uses a numeric comparator to compare the field values and determine their relative order.

## Use of heap:
A heap data structure is employed in Lucene to efficiently manage the top-ranked documents during the sorting process. Heaps, specifically min-heap or max-heap, are used because they allow for efficient access to the minimum or maximum element in the dataset, respectively.

* In the context of sorting search results in Lucene, a priority queue is used, which is an abstract data type that generalizes the concept of a heap. Here's how the heap is used in the sorting process:

* Initialize priority queue: A priority queue (min-heap or max-heap, depending on the sorting order) is initialized with a size equal to the number of top results requested (e.g., top 10 results).

* Process search results: As Lucene processes the search results, it retrieves the field values for the sorting field from the DocValues storage and adds the documents to the priority queue. The priority queue efficiently maintains the top-ranked documents based on their field values.

* Manage top-ranked documents: When a new document is added to the priority queue, it either displaces a lower-ranked document or is discarded, depending on its field value and the sorting order. This ensures that the priority queue always contains the top-ranked documents as the search progresses.

* Extract sorted results: Once the search is complete, the top-ranked documents can be extracted from the priority queue in the desired sorted order.

### The use of a heap (priority queue) in the sorting process provides several benefits:

* Efficient management of top-ranked documents: The heap data structure allows for quick access to the minimum or maximum element, making it easy to maintain the top-ranked documents during the search process.
* Space efficiency: Since the priority queue only keeps track of the top-ranked documents, it uses less memory compared to alternative data structures like a fully sorted list or array.
* Time efficiency: The time complexity of inserting and deleting elements in a heap is O(log n), where n is the number of elements in the heap. This makes the heap an efficient data structure for managing search results, particularly when dealing with large datasets.
