# pytest-numba
Pytest plugin to support testing numba related code.

## WIP todo list
- numba seeding fixture
- numba cache clearing mark (for testing that code compiled)
- fixture to validate that a function compiled

## Notes
seeding for `prange` requires setting the seed for each iteration somewhat deterministically  

```python
@njit
def seed_numba(seed: int) -> None:
    random.seed(seed)
    np.random.seed(seed)

@njit(parallel=True)
def some_func():
    ...
    seed_offset = np.random.randint(low=1, high=500)
    for i in prange(1000):
        seed_numba(i + seed_offset)
```
