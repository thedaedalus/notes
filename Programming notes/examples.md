# Example code

## recursive function to get the largest word in a string

```python
def find_longest_word(document, longest_word=""):
    if not document or document == " ":
        return longest_word
    parts = document.split(maxsplit=1)
    first_word = parts[0]
    rest = parts[1] if len(parts) > 1 else ""
    if len(first_word) > len(longest_word):
        longest_word=first_word
    if rest:
        return find_longest_word(rest, longest_word)
    return longest_word
```

## traverse nested data structure

```Python
def list_files(parent_directory, current_filepath=""):
    file_path = []
    for sub_dir in parent_directory:
        new_path = current_filepath + "/"+(f"{sub_dir}")
        if parent_directory[sub_dir] is None:
           file_path.append(new_path)
        if parent_directory[sub_dir]:
            file_path.extend(list_files(parent_directory[sub_dir], new_path))
    return file_path
```

## traverse nested dict and count level

```Python
def count_nested_levels(nested_documents, target_document_id, level=1):
    for document_id in nested_documents:
        if document_id == target_document_id:
            return level
        found_level = count_nested_levels(
            nested_documents[document_id], target_document_id, level + 1
        )
        if found_level != -1:
            return found_level
    return -1
```

## queue implementation

```Python
class Queue:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)   # tail at the end

    def pop(self):
        if not self.items:
            return None
        return self.items.pop(0)  # head at index 0

    def peek(self):
        if not self.items:
            return None
        return self.items[0]      # look at head, index 0

    def size(self):
        return len(self.items)
```

## Prime Factoring

```Python
def prime_factors(n):
    prime_factors = []
    while n % 2 == 0:
        n /= 2
        prime_factors.append(2)
    for i in range(3, int(math.sqrt(n)) + 1, 2):
        while n % i == 0:
            n /= i
            prime_factors.append(i)
    if n > 2:
        prime_factors.append(int(n))
    return prime_factors
```
