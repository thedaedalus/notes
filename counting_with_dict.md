# Pattern: Counting Things with a Dictionary

Pattern: Counting Things with a Dictionary

1. **Start an empty dictionary** for counts:

      ```Python
        counts = {}
    ```

2. **Loop over the collection** of items you want to count:

    ```Python
    for item in items:
    ```

3. **Update the count for each item** using `dict.get`:

    ```python
    counts[item] = counts.get(item, 0) + 1
    ```

    - `counts.get(item, 0)`:
      - returns the current count if `item` is aldready in the dictionary
      - otherwise returns `0`
    - Then you add `1` and store it back
4. **Return or use the** `counts` dictionary:

```python
return counts
```

This pattern works any time you’re:

- looping over data
- and want a frequency table / histogram of how often each value occurs
