<h1>Project: Pagination</h1>
    <h2>Learning Objectives</h2>
    <p>The learning objectives of this project are:</p>
    <ul>
        <li>How to paginate a dataset with simple page and page_size parameters</li>
        <li>How to paginate a dataset with hypermedia metadata</li>
        <li>How to paginate in a deletion-resilient manner</li>
    </ul>
    <h3>0. Simple helper function</h3>
    <p>Write a function named <code>index_range</code> that takes two integer arguments <code>page</code> and <code>page_size</code>.</p>
    <p>The function should return a tuple of size two containing a start index and an end index corresponding to the range of indexes to return in a list for those particular pagination parameters.</p>
    <p>Page numbers are 1-indexed, i.e. the first page is page 1.</p>
    <h3>1. Simple pagination</h3>
    <p>Using the <code>index_range</code> function from task #0 and the following class into your code:</p>
    <pre>
        <code>
import csv
import math
from typing import List

class Server:
    """Server class to paginate a database of popular baby names.
    """
    DATA_FILE = "Popular_Baby_Names.csv"

    def __init__(self):
        self.__dataset = None

    def dataset(self) -> List[List]:
        """Cached dataset
        """
        if self.__dataset is None:
            with open(self.DATA_FILE) as f:
                reader = csv.reader(f)
                dataset = [row for row in reader]
            self.__dataset = dataset[1:]

        return self.__dataset

    def get_page(self, page: int = 1, page_size: int = 10) -> List[List]:
        pass
</code>
    </pre>
    <p>Implement a method named <code>get_page</code> that takes two integer arguments <code>page</code> with default value 1 and <code>page_size</code> with default value 10.</p>
    <p>Use <code>assert</code> to verify that both arguments are integers greater than 0.</p>
    <p>Use <code>index_range</code> to find the correct indexes to paginate the dataset correctly and return the appropriate page of the dataset (i.e. the correct list of rows).</p>
    <p>If the input arguments are out of range for the dataset, an empty list should be returned.</p>
    <h3>2. Hypermedia pagination</h3>
    <p>Replicate code from the previous task.</p>
    <p>Implement a <code>get_hyper</code> method that takes the same arguments (and defaults) as <code>get_page</code> and returns a dictionary containing the following key-value pairs:</p>
    <ul>
        <li><code>page_size</code>: the length of the returned dataset page</li>
        <li><code>page</code>: the current page number</li>
        <li><code>data</code>: the dataset page (equivalent to return from the previous task)</li>
        <li><code>next_page</code>: number of the next page, <code>None</code> if no next page</li>
        <li><code>prev_page</code>: number of the previous page, <code>None</code> if no previous page</li>
        <li><code>total_pages</code>: the total number of pages in the dataset as an integer</li>
    </ul>
    <p>Make sure to reuse <code>get_page</code> in your implementation.</p>
    <h3>3. Deletion-resilient hypermedia pagination</h3>
    <p>The goal here is that if between two queries, certain rows are removed from the dataset, the user does not miss items from dataset when changing page.</p>
    <p>Start <code>3-hypermedia_del_pagination.py</code> with this code:</p>
    <pre>
        <code>
#!/usr/bin/env python3
"""
Deletion-resilient hypermedia pagination
"""

import csv
import math
from typing import List
        </code>
    </pre>
    <p>Implement a <code>get_hyper_index</code> method with two integer arguments: <code>index</code> with a <code>None</code> default value and <code>page_size</code> with default value of 10.</p>
    <p>The method should return a dictionary with the following key-value pairs:</p>
    <ul>
        <li><code>index</code>: the current start index of the return page. That is the index of the first item in the current page. For example if requesting page 3 with page_size 20, and no data was removed from the dataset, the current index should be 60.</li>
        <li><code>next_index</code>: the next index to query with. That should be the index of the first item after the last item on the current page.</li>
        <li><code>page_size</code>: the current page size</li>
        <li><code>data</code>: the actual page of the dataset</li>
    </ul>
    <p>Requirements/Behavior:</p>
    <ul>
        <li>Use <code>assert</code> to verify that <code>index</code> is in a valid range.</li>
        <li>If the user queries index 0, page_size 10, they will get rows indexed 0 to 9 included.</li>
        <li>If they request the next index (10) with page_size 10, but rows 3, 6, and 7 were deleted, the user should still receive rows indexed 10 to 19 included.</li>
    </ul>