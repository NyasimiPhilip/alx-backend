  <h1>Tasks</h1>
  <h2>0. Basic dictionary</h2> 
  <p>Create a class <code>BasicCache</code> that inherits from <code>BaseCaching</code> and is a caching system:</p>
  <ul>
    <li>You must use <code>self.cache_data</code> - dictionary from the parent class <code>BaseCaching</code></li>
    <li>This caching system doesn't have a limit</li>
  </ul>
  <pre><code>
class BasicCache(BaseCaching):
    def put(self, key, item):
        # Must assign to the dictionary self.cache_data the item value for the key key.
        # If key or item is None, this method should not do anything.

    def get(self, key):
        # Must return the value in self.cache_data linked to key.
        # If key is None or if the key doesn't exist in self.cache_data, return None.
  </code></pre>
  <h2>1. FIFO caching</h2>  
  <p>Create a class <code>FIFOCache</code> that inherits from <code>BaseCaching</code> and is a caching system:</p>
  <ul>
    <li>You must use <code>self.cache_data</code> - dictionary from the parent class <code>BaseCaching</code></li>
    <li>You can overload <code>def __init__(self):</code> but don't forget to call the parent init: <code>super().__init__()</code></li>
    <li>...</li>
  </ul>
  <pre><code>
class FIFOCache(BaseCaching):
    def __init__(self):
        super().__init__()

    def put(self, key, item):
        # Must assign to the dictionary self.cache_data the item value for the key key.
        # If key or item is None, this method should not do anything.
        # If the number of items in self.cache_data is higher than BaseCaching.MAX_ITEMS:
        #   - you must discard the first item put in cache (FIFO algorithm)
        #   - you must print DISCARD: with the key discarded and following by a new line

    def get(self, key):
        # Must return the value in self.cache_data linked to key.
        # If key is None or if the key doesn't exist in self.cache_data, return None.
  </code></pre>
  <h2>2. LIFO Caching</h2>  
  <p>Create a class <code>LIFOCache</code> that inherits from <code>BaseCaching</code> and is a caching system:</p>
  <ul>
    <li>You must use <code>self.cache_data</code> - dictionary from the parent class <code>BaseCaching</code></li>
    <li>You can overload <code>def __init__(self):</code> but don't forget to call the parent init: <code>super().__init__()</code></li>
    <li>...</li>
  </ul>
  <pre><code>
class LIFOCache(BaseCaching):
    def __init__(self):
        super().__init__()

    def put(self, key, item):
        # Must assign to the dictionary self.cache_data the item value for the key key.
        # If key or item is None, this method should not do anything.
        # If the number of items in self.cache_data is higher than BaseCaching.MAX_ITEMS:
        #   - you must discard the last item put in cache (LIFO algorithm)
        #   - you must print DISCARD: with the key discarded and following by a new line

    def get(self, key):
        # Must return the value in self.cache_data linked to key.
        # If key is None or if the key doesn't exist in self.cache_data, return None.
  </code></pre>

  <h2>3. LRU Caching</h2>

  <p>Create a class <code>LRUCache</code> that inherits from <code>BaseCaching</code> and is a caching system:</p>
  <ul>
    <li>You must use <code>self.cache_data</code> - dictionary from the parent class <code>BaseCaching</code></li>
    <li>You can overload <code>def __init__(self):</code> but don't forget to call the parent init: <code>super().__init__()</code></li>
    <li>...</li>
  </ul>
  <pre><code>
class LRUCache(BaseCaching):
    def __init__(self):
        super().__init__()

    def put(self, key, item):
        # Must assign to the dictionary self.cache_data the item value for the key key.
        # If key or item is None, this method should not do anything.
        # If the number of items in self.cache_data is higher than BaseCaching.MAX_ITEMS:
        #   - you must discard the least recently used item (LRU algorithm)
        #   - you must print DISCARD: with the key discarded and following by a new line

    def get(self, key):
        # Must return the value in self.cache_data linked to key.
        # If key is None or if the key doesn't exist in self.cache_data, return None.
  </code></pre>

  <h2>4. MRU Caching</h2>  
  <p>Create a class <code>MRUCache</code> that inherits from <code>BaseCaching</code> and is a caching system:</p>
  <ul>
    <li>You must use <code>self.cache_data</code> - dictionary from the parent class <code>BaseCaching</code></li>
    <li>You can overload <code>def __init__(self):</code> but don't forget to call the parent init: <code>super().__init__()</code></li>
    <li>...</li>
  </ul>
  <pre><code>
class MRUCache(BaseCaching):
    def __init__(self):
        super().__init__()

    def put(self, key, item):
        # Must assign to the dictionary self.cache_data the item value for the key key.
        # If key or item is None, this method should not do anything.
        # If the number of items in self.cache_data is higher than BaseCaching.MAX_ITEMS:
        #   - you must discard the most recently used item (MRU algorithm)
        #   - you must print DISCARD: with the key discarded and following by a new line

    def get(self, key):
        # Must return the value in self.cache_data linked to key.
        # If key is None or if the key doesn't exist in self.cache_data, return None.
  </code></pre>

  <h2>5. LFU Caching</h2>
  <p><strong>#advanced</strong></p>
  <p>Create a class <code>LFUCache</code> that inherits from <code>BaseCaching</code> and is a caching system:</p>
  <ul>
    <li>You must use <code>self.cache_data</code> - dictionary from the parent class <code>BaseCaching</code></li>
    <li>You can overload <code>def __init__(self):</code> but don't forget to call the parent init: <code>super().__init__()</code></li>
    <li>...</li>
  </ul>
  <pre><code>
class LFUCache(BaseCaching):
    def __init__(self):
        super().__init__()

    def put(self, key, item):
        # Must assign to the dictionary self.cache_data the item value for the key key.
        # If key or item is None, this method should not do anything.
        # If the number of items in self.cache_data is higher than BaseCaching.MAX_ITEMS:
        #   - you must discard the least frequency used item (LFU algorithm)
        #   - if you find more than 1 item to discard, you must use the LRU algorithm to discard only the least recently used
        #   - you must print DISCARD: with the key discarded and following by a new line

    def get(self, key):
        # Must return the value in self.cache_data linked to key.
        # If key is None or if the key doesn't exist in self.cache_data, return None.
  </code></pre>