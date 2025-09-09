Пример реализации [[Хэш-таблицы|хеш - таблицы]] ([[dict]])

```python
class HashTable:
    def __init__(self, size: int):
        self.size = size
        self.buckets = [[] for _ in range(size)]

    def _hash(self, key: str) -> int:
        return sum(ord(c) for c in key) % self.size

    def set(self, key: str, value):
        idx = self._hash(key)
        for i, (k, _) in enumerate(self.buckets[idx]):
            if k == key:
                self.buckets[idx][i] = (key, value)
                return
        self.buckets[idx].append((key, value))

    def get(self, key: str):
        idx = self._hash(key)
        for k, v in self.buckets[idx]:
            if k == key:
                return v
        return None

    def delete(self, key: str):
        idx = self._hash(key)
        self.buckets[idx] = [(k, v) for k, v in self.buckets[idx] if k != key]
```

```python
d = HashTable(10)
d.set("apple", 42)
print(d.get("apple"))  # 42
d.delete("apple")
print(d.get("apple"))  # None
```

