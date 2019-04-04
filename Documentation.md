<span id="collections_index"> Collections Documentation </span>

* [List](#List)
* [LinkedList](#LinkedList)
* [Stack](#Stack)
* [Queue](#Queue)
* [Deque](#Deque)
* [Heap](#Heap)
* [TreeSet](#TreeSet)
* [TreeMap](#TreeMap)
* [HashSet](#HashSet)
* [HashMap](#HashMap)

# [List](#collections_index)

A contiguous growable array. Elements can be added and removed from both ends of the array and also in the middle. This list can also be used to implement other data structures like stack, queues and deques, although queues and deques are implemented as a circular buffer, therefore being more efficient.

### Generation Macro

* `LIST_GENERATE(PFX, SNAME, FMOD, V)`
    * `PFX` - Functions namespace or prefix.
    * `SNAME` - Structure name.
    * `FMOD` - Function modifier (static or empty).
    * `V` - Element type.

### Defined Structures

* `struct SNAME##_s` - Structure Name (represents a list structure)
    * `V *buffer` - Internal storage.
    * `size_t capacity` - Storage capacity.
    * `size_t count` - Total elements in the list.
* `struct SNAME##_iter_s` - Structure Iterator (represents a list iterator)
    * `struct SNAME##_s *target` - List being iterated over.
    * `size_t cursor` - Index pointing to the next or previous element in the iteration.
    * `bool start` - If the iterator reached the start of the list.
    * `bool end` - If the iterator reached the end of the list.

### Typedefs

* `typedef struct SNAME##_s SNAME`
* `typedef struct SNAME##_iter_s SNAME##_iter`

### <span id="list_function_index"> Defined Functions </span>

* [\_new()](#list_new)
* [\_free()](#list_free)
* [\_push\_front()](#list_push_front)
* [\_push()](#list_push)
* [\_push\_back()](#list_push_back)
* [\_pop\_front()](#list_pop_front)
* [\_pop()](#list_pop)
* [\_pop\_back()](#list_pop_back)
* [\_push\_if()](#list_push_if)
* [\_pop\_if()](#list_pop_if)
* [\_front()](#list_front)
* [\_get()](#list_get)
* [\_back()](#list_back)
* [\_empty()](#list_empty)
* [\_full()](#list_full)
* [\_count()](#list_count)
* [\_capacity()](#list_capacity)
* [\_iter\_new()](#list_iter_new)
* [\_iter\_start()](#list_iter_start)
* [\_iter\_end()](#list_iter_end)
* [\_iter\_tostart()](#list_iter_tostart)
* [\_iter\_toend()](#list_iter_toend)
* [\_iter\_next()](#list_iter_next)
* [\_iter\_prev()](#list_iter_prev)

## [<span id="list_new"> \_new() </span>](#list_function_index)

Allocates and returns a new list with an internal capacity of `size`. If allocation fails, `NULL` is returned.

#### Declaration

> `FMOD SNAME *PFX##_new(size_t size);`

#### Parameters

1. `size_t size` - The initial capacity for the list.

#### Returns

1. `SNAME *` - A pointer to a heap allocated list.
2. `NULL` - If allocation fails.

#### Complexity

* O(1)

## [<span id="list_free"> \_free() </span>](#list_function_index)

Frees from memory the list internal buffer and the structure itself. Note that if the elements inside the list are pointers to allocated memory, this function might cause memory leaks as it does not deals with its elements.

#### Declaration

> `FMOD void PFX##_free(SNAME *_list_);`

#### Parameters

1. `SNAME *_list_` - Target list to be freed from memory.

#### Complexity

* O(1)

## [<span id="list_push_front"> \_push\_front() </span>](#list_function_index)

Shifts all elements one position to the right and adds an element at the front of the list (index `0`).

#### Declaration

> `FMOD bool PFX##_push_front(SNAME *_list_, V element);`

#### Parameters

1. `SNAME *_list_` - Target list.
2. `V element` - Element to be added.

#### Returns

1. `true` - If the element was successfully added to the list.
2. `false` - If buffer reallocation failed.

#### Complexity

* O(n)

## [<span id="list_push"> \_push() </span>](#list_function_index)

Adds an element at a given index in the list. After it is successfully added to the list, the element is accessible at the index passed to the function.

#### Declaration

> `FMOD bool PFX##_push(SNAME *_list_, V element, size_t index);`

#### Parameters

1. `SNAME *_list_` - Target list.
2. `V element` - Element to be added.
3. `size_t index` - Index to add the new element.
    * Can't be greater than the list `count`.

#### Returns

1. `true` - If the element was successfully added to the list.
2. `false` - If buffer reallocation failed, or if `index` is greater than the list `count`.

#### Complexity

* O(n)

## [<span id="list_push_back"> \_push\_back() </span>](#list_function_index)

Adds an element at the back of the list (index `count` where count is the amount of elements in the list). No shifts are required.

#### Declaration

> `FMOD bool PFX##_push_back(SNAME *_list_, V element);`

#### Parameters

1. `SNAME *_list_` - Target list.
2. `V element` - Element to be added.

#### Returns

1. `true` - If the element was successfully added to the list.
2. `false` - If buffer reallocation failed.

#### Complexity

* O(1)

## [<span id="list_pop_front"> \_pop\_front() </span>](#list_function_index)

Removes the first element in the list (located at index `0`) and shifts all remaining elements to the left.

#### Declaration

> `FMOD bool PFX##_pop_front(SNAME *_list_);`

#### Parameters

1. `SNAME *_list_` - Target list.

#### Returns

1. `true` - If the element was successfully removed from the list.
2. `false` - If the list is empty.

#### Complexity

* O(n)

## [<span id="list_pop"> \_pop() </span>](#list_function_index)

Removes the element located at a given index and shifts all the elements to its right to the left.

#### Declaration

> `FMOD bool PFX##_pop(SNAME *_list_, size_t index);`

#### Parameters

1. `SNAME *_list_` - Target list.
3. `size_t index` - The index of the element to be removed.
    * Can't be greater than or equal to the list `count`.

#### Returns

1. `true` - If the element was successfully removed from the list.
2. `false` - If the list is empty, or if `index` is greater than or equal to the list `count`.

#### Complexity

* O(n)

## [<span id="list_pop_back"> \_pop\_back() </span>](#list_function_index)

Removes the last element in the list (located at index `count - 1`). No shifts are required.

#### Declaration

> `FMOD bool PFX##_pop_back(SNAME *_list_);`

#### Parameters

1. `SNAME *_list_` - Target list.

#### Returns

1. `true` - If the element was successfully removed from the list.
2. `false` - If the list is empty.

#### Complexity

* O(1)

## [<span id="list_push_if"> \_push\_if() </span>](#list_function_index)

Adds an element at a given index if the condition evaluates to true.

#### Declaration

> `FMOD bool PFX##_push_if(SNAME *_list_, V element, size_t index, bool condition);`

#### Parameters

1. `SNAME *_list_` - Target list.
2. `V element` - Element to be added.
3. `size_t index` - Index to add the new element.
    * Can't be greater than the list `count`.
4. `bool condition` - Condition for the element to be added.

#### Returns

1. `true` - If the element was successfully added to the list.
2. `false` - If the condition evaluated to false, if `index` is greater than the list `count`, or if buffer reallocation failed.

#### Complexity

* O(n)

## [<span id="list_pop_if"> \_pop\_if() </span>](#list_function_index)

Removes an element from a given index if the condition evaluates to true.

#### Declaration

> `FMOD bool PFX##_pop_if(SNAME *_list_, size_t index, bool condition);`

#### Parameters

1. `SNAME *_list_` - Target list.
2. `size_t index` - The index of the element to be removed.
    * Can't be greater than or equal to the list `count`.
3. `bool condition` - Condition for the element to be removed.

#### Returns

1. `true` - If the element was successfully removed from the list.
2. `false` - If the condition evaluated to false, if the list is empty, or if the index is greater than or equal to the list `count`.

#### Complexity

* O(n)

## [<span id="list_front"> \_front() </span>](#list_function_index)

Returns the first element (located at index `0`) if the list is not empty.

#### Declaration

> `FMOD V PFX##_front(SNAME *_list_);`

#### Parameters

1. `SNAME *_list_` - Target list.

#### Returns

1. `V` - The first element in the list.
2. `0` or `NULL` - If the list is empty.

#### Complexity

* O(1)

## [<span id="list_get"> \_get() </span>](#list_function_index)

Returns the element located at the given index if the list is not empty.

#### Declaration

> `FMOD V PFX##_get(SNAME *_list_, size_t index)`

#### Parameters

1. `SNAME *_list_` - Target list.
2. `size_t index` - Index to retrieve an element.
    * Can't be greater than or equal to the list `count`.

#### Returns

1. `V` - The element in the list located at the given index.
2. `0` or `NULL` - If the list is empty, or if `index` is greater than or equal to the list `count`.

#### Complexity

* O(1)

## [<span id="list_back"> \_back() </span>](#list_function_index)

Returns the last element (located at index `count - 1`) if the list is not empty.

#### Declaration

> `FMOD V PFX##_back(SNAME *_list_)`

#### Parameters

1. `SNAME *_list_` - Target list.

#### Returns

1. `V` - The last element in the list.
2. `0` or `NULL` - If the list is empty.

#### Complexity

* O(1)

## [<span id="list_empty"> \_empty() </span>](#list_function_index)

Returns true if the list is empty, otherwise false.

#### Declaration

> `FMOD bool PFX##_empty(SNAME *_list_);`

#### Parameters

1. `SNAME *_list_` - Target list.

#### Returns

1. `true` - If the list is empty.
2. `false` - If there is at least one element in the list.

#### Complexity

* O(1)

## [<span id="list_full"> \_full() </span>](#list_function_index)

Returns true if the list is full, otherwise false. The list is considered full when its internal buffer is filled up, so the next element added to the list will required a resizing of the buffer, but note that the list can grow indefinitely.

#### Declaration

> `FMOD bool PFX##_full(SNAME *_list_);`

#### Parameters

1. `SNAME *_list_` - Target list.

#### Returns

1. `true` - If the list internal buffer is full.
2. `false` - If the list internal buffer is not full.

#### Complexity

* O(1)

## [<span id="list_count"> \_count() </span>](#list_function_index)

Returns the amount of elements in the list.

#### Declaration

> `FMOD size_t PFX##_count(SNAME *_list_);`

#### Parameters

1. `SNAME *_list_` - Target list.

#### Returns

1. `size_t` - The amount of elements in the list.

#### Complexity

* O(1)

## [<span id="list_capacity"> \_capacity() </span>](#list_function_index)

Returns the internal buffer's current capacity.

#### Declaration

> `FMOD size_t PFX##_capacity(SNAME *_list_);`

#### Parameters

1. `SNAME *_list_` - Target list.

#### Returns

1. `size_t` - The internal buffer's current capacity.

#### Complexity

* O(1)

## [<span id="list_iter_new"> \_iter\_new() </span>](#list_function_index)

Initializes an iterator with a given target list. The iterator's cursor will be positioned at the beginning of the list.

#### Declaration

> `FMOD void PFX##_iter_new(SNAME##_iter *iter, SNAME *target);`

#### Parameters

1. `SNAME##_iter *iter` - Iterator to be initialized.
2. `SNAME *target` - Target list.

#### Complexity

* O(1)

## [<span id="list_iter_start"> \_iter\_start() </span>](#list_function_index)

Returns true if the iterator has reached the start of the list. If false, the iterator is still possible to iterate to a previous element.

#### Declaration

> `FMOD bool PFX##_iter_start(SNAME##_iter *iter);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.

#### Returns 

1. `true` - If the iterator has reached the start of the list.
2. `false` - If the iterator has not reached the start of the list.

#### Complexity

* O(1)

## [<span id="list_iter_end"> \_iter\_end() </span>](#list_function_index)

Returns true if the iterator has reached the end of the list. If false, the iterator is still possible to iterate to a next element.

#### Declaration

> `FMOD bool PFX##_iter_end(SNAME##_iter *iter);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.

#### Returns 

1. `true` - If the iterator has reached the end of the list.
2. `false` - If the iterator has not reached the end of the list.

#### Complexity

* O(1)

## [<span id="list_iter_tostart"> \_iter\_tostart() </span>](#list_function_index)

Moves the cursor of the target iterator to the start of the list.

#### Declaration

> `FMOD void PFX##_iter_tostart(SNAME##_iter *iter);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.

#### Complexity

* O(1)

## [<span id="list_iter_toend"> \_iter\_toend() </span>](#list_function_index)

Moves the cursor of the target iterator to the end of the list.

#### Declaration

> `FMOD void PFX##_iter_toend(SNAME##_iter *iter);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.

#### Complexity

* O(1)

## [<span id="list_iter_next"> \_iter\_next() </span>](#list_function_index)

This function is used to iterate to the next element, retrieving the current one, along with an index that represents how many iterations have passed. When the index is `0` it means that the current result is the first element in the list; if it equals `count - 1` then it is the last element in the list.

#### Declaration

> `FMOD bool PFX##_iter_next(SNAME##_iter *iter, V *result, size_t *index);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.
2. `V *result` - Resulting value from the list.
3. `size_t *index` - Resulting index.

#### Returns 

1. `true` - If the iterator has retrieved a valid `result` and `index`.
2. `false` - If the iterator has not retrieved a valid `result` and `index`. Here, iteration to the next element has ended.

#### Complexity

* O(1)

## [<span id="list_iter_prev"> \_iter\_prev() </span>](#list_function_index)

This function is used to iterate to the previous element, retrieving the current one, along with an index that represents how many iterations have passed. When the index is `0` it means that the current result is the first element in the list; if it equals `count - 1` then it is the last element in the list.

#### Declaration

> `FMOD bool PFX##_iter_prev(SNAME##_iter *iter, V *result, size_t *index);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.
2. `V *result` - Resulting value from the list.
3. `size_t *index` - Resulting index.

#### Returns 

1. `true` - If the iterator has retrieved a valid `result` and `index`.
2. `false` - If the iterator has not retrieved a valid `result` and `index`. Here, iteration to the previous element has ended.

#### Complexity

* O(1)

# [LinkedList](#collections_index)

A list where each element is linked by nodes. Elements can be added and removed from both ends of the list and also in the middle. The linked list can be used to implement other data structures like queues, stacks and deques.

# [Stack](#collections_index)

A LIFO/FILO structure backed by a growable array. All elements are added and removed from the top of the stack.

### Generation Macro

* `STACK_GENERATE(PFX, SNAME, FMOD, V)`
    * `PFX` - Functions namespace or prefix.
    * `SNAME` - Structure name.
    * `FMOD` - Function modifier (static or empty).
    * `V` - Element type.

### Defined Structures

* `struct SNAME##_s` - Structure Name (represents a stack structure)
    * `V *buffer` - Internal storage.
    * `size_t capacity` - Storage capacity.
    * `size_t count` - Total elements in the stack.
* `struct SNAME##_iter_s` - Structure Iterator (represents a stack iterator)
    * `struct SNAME##_s *target` - Stack being iterated over.
    * `size_t cursor` - Index pointing to the next or previous element in the iteration.
    * `bool start` - If the iterator reached the start of the stack.
    * `bool end` - If the iterator reached the end of the stack.

### Typedefs

* `typedef struct SNAME##_s SNAME`
* `typedef struct SNAME##_iter_s SNAME##_iter`

### <span id="stack_function_index"> Defined Functions </span>

* [\_new()](#stack_new)
* [\_free()](#stack_free)
* [\_push()](#stack_push)
* [\_pop()](#stack_pop)
* [\_push\_if()](#stack_push_if)
* [\_pop\_if()](#stack_pop_if)
* [\_top()](#stack_top)
* [\_empty()](#stack_empty)
* [\_full()](#stack_full)
* [\_count()](#stack_count)
* [\_capacity()](#stack_capacity)
* [\_iter\_new()](#stack_iter_new)
* [\_iter\_start()](#stack_iter_start)
* [\_iter\_end()](#stack_iter_end)
* [\_iter\_tostart()](#stack_iter_tostart)
* [\_iter\_toend()](#stack_iter_toend)
* [\_iter\_next()](#stack_iter_next)
* [\_iter\_prev()](#stack_iter_prev)

## [<span id="stack_new"> \_new() </span>](#stack_function_index)

Allocates and returns a new stack with an internal capacity of `size`. If allocation fails, `NULL` is returned.

#### Declaration

> `FMOD SNAME *PFX##_new(size_t size);`

#### Parameters

1. `size_t size` - The initial capacity for the stack.

#### Returns

1. `SNAME *` - A pointer to a heap allocated stack.
2. `NULL` - If allocation fails.

#### Complexity

* O(1)

## [<span id="stack_free"> \_free() </span>](#stack_function_index)

Frees from memory the stack internal buffer and the structure itself. Note that if the elements inside the stack are pointers to allocated memory, this function might cause memory leaks as it does not deals with its elements.

#### Declaration

> `FMOD void PFX##_free(SNAME *_stack_);`

#### Parameters

1. `SNAME *_stack_` - Target stack to be freed from memory.

#### Complexity

* O(1)

## [<span id="stack_push"> \_push() </span>](#stack_function_index)

Adds an element on top of the stack.

#### Declaration

> `FMOD bool PFX##_push(SNAME *_stack_, V element);`

#### Parameters

1. `SNAME *_stack_` - Target stack.
2. `V element` - Element to be added.

#### Returns

1. `true` - If the element was successfully added to the stack.
2. `false` - If buffer reallocation failed.

#### Complexity

* O(1)

## [<span id="stack_pop"> \_pop() </span>](#stack_function_index)

Removes the top element from the stack.

#### Declaration

> `FMOD bool PFX##_pop(SNAME *_stack_);`

#### Parameters

1. `SNAME *_stack_` - Target stack.

#### Returns

1. `true` - If an element was successfully removed from the stack.
2. `false` - If the stack is empty.

#### Complexity

* O(1)

## [<span id="stack_push_if"> \_push\_if() </span>](#stack_function_index)

Adds an element on top of the stack if the condition evaluates to true.

#### Declaration

> `FMOD bool PFX##_push_if(SNAME *_stack_, V element, bool condition);`

#### Parameters

1. `SNAME *_stack_` - Target stack.
2. `V element` - Element to be added.
3. `bool condition` - Condition for the element to be added.

#### Returns

1. `true` - If the element was successfully added to the stack.
2. `false` - If the condition evaluated to false, or if buffer reallocation failed.

#### Complexity

* O(1)

## [<span id="stack_pop_if"> \_pop\_if() </span>](#stack_function_index)

Removes the top element from the stack if the condition evaluates to true.

#### Declaration

> `FMOD bool PFX##_pop_if(SNAME *_stack_, bool condition);`

#### Parameters

1. `SNAME *_stack_` - Target stack.
3. `bool condition` - Condition for the element to be removed.

#### Returns

1. `true` - If the element was successfully added to the stack.
2. `false` - If the condition evaluated to false, or if the stack is empty.

#### Complexity

* O(1)

## [<span id="stack_top"> \_top() </span>](#stack_function_index)

Returns the element at the top of the stack if available.

#### Declaration

> `FMOD V PFX##_top(SNAME *_stack_);`

#### Parameters

1. `SNAME *_stack_` - Target stack.

#### Returns

1. `V` - The element at the top of the stack.
2. `0` or `NULL` - If the stack is empty.

#### Complexity

* O(1)

## [<span id="stack_empty"> \_empty() </span>](#stack_function_index)

Returns true if the stack is empty, otherwise false.

#### Declaration

> `FMOD bool PFX##_empty(SNAME *_stack_);`

#### Parameters

1. `SNAME *_stack_` - Target stack.

#### Returns

1. `true` - If the stack is empty.
2. `false` - If there is at least one element in the stack.

#### Complexity

* O(1)

## [<span id="stack_full"> \_full() </span>](#stack_function_index)

Returns true if the stack is full, otherwise false. The stack is considered full when its internal buffer is filled up, so the next element added to the stack will required a resizing of the buffer, but note that the stack can grow indefinitely.

#### Declaration

> `FMOD bool PFX##_full(SNAME *_stack_);`

#### Parameters

1. `SNAME *_stack_` - Target stack.

#### Returns

1. `true` - If the stack internal buffer is full.
2. `false` - If the stack internal buffer is not full.

#### Complexity

* O(1)

## [<span id="stack_count"> \_count() </span>](#stack_function_index)

Returns the amount of elements in the stack.

#### Declaration

> `FMOD size_t PFX##_count(SNAME *_stack_);`

#### Parameters

1. `SNAME *_stack_` - Target stack.

#### Returns

1. `size_t` - The amount of elements in the stack.

#### Complexity

* O(1)

## [<span id="stack_capacity"> \_capacity() </span>](#stack_function_index)

Returns the internal buffer's current capacity.

#### Declaration

> `FMOD size_t PFX##_capacity(SNAME *_stack_);`

#### Parameters

1. `SNAME *_stack_` - Target stack.

#### Returns

1. `size_t` - The internal buffer's current capacity.

#### Complexity

* O(1)

## [<span id="stack_iter_new"> \_iter\_new() </span>](#stack_function_index)

Initializes an iterator with a given target stack. The iterator's cursor will be positioned at the top element of the stack.

#### Declaration

> `FMOD void PFX##_iter_new(SNAME##_iter *iter, SNAME *target);`

#### Parameters

1. `SNAME##_iter *iter` - Iterator to be initialized.
2. `SNAME *target` - Target stack.

#### Complexity

* O(1)

## [<span id="stack_iter_start"> \_iter\_start() </span>](#stack_function_index)

Returns true if the iterator has reached the start of the stack (top element). If false, the iterator is still possible to iterate to a previous element.

#### Declaration

> `FMOD bool PFX##_iter_start(SNAME##_iter *iter);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.

#### Returns 

1. `true` - If the iterator has reached the start of the stack.
2. `false` - If the iterator has not reached the start of the stack.

#### Complexity

* O(1)

## [<span id="stack_iter_end"> \_iter\_end() </span>](#stack_function_index)

Returns true if the iterator has reached the end of the stack (bottom element). If false, the iterator is still possible to iterate to a next element.

#### Declaration

> `FMOD bool PFX##_iter_end(SNAME##_iter *iter);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.

#### Returns 

1. `true` - If the iterator has reached the end of the stack.
2. `false` - If the iterator has not reached the end of the stack.

#### Complexity

* O(1)

## [<span id="stack_iter_tostart"> \_iter\_tostart() </span>](#stack_function_index)

Moves the cursor of the target iterator to the start (top element) of the stack.

#### Declaration

> `FMOD void PFX##_iter_tostart(SNAME##_iter *iter);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.

#### Complexity

* O(1)

## [<span id="stack_iter_toend"> \_iter\_toend() </span>](#stack_function_index)

Moves the cursor of the target iterator to the end of the stack (bottom element).

#### Declaration

> `FMOD void PFX##_iter_toend(SNAME##_iter *iter);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.

#### Complexity

* O(1)

## [<span id="stack_iter_next"> \_iter\_next() </span>](#stack_function_index)

This function is used to iterate to the next element, retrieving the current one, along with an index that represents how many iterations have passed. When the index is `0` it means that the current result is the top-most element of the stack; if it equals `count - 1` then it is the bottom-most element of the stack.

#### Declaration

> `FMOD bool PFX##_iter_next(SNAME##_iter *iter, V *result, size_t *index);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.
2. `V *result` - Resulting value from the stack.
3. `size_t *index` - Resulting index.

#### Returns 

1. `true` - If the iterator has retrieved a valid `result` and `index`.
2. `false` - If the iterator has not retrieved a valid `result` and `index`. Here, iteration to the next element has ended.

#### Complexity

* O(1)

## [<span id="stack_iter_prev"> \_iter\_prev() </span>](#stack_function_index)

This function is used to iterate to the previous element, retrieving the current one, along with an index that represents how many iterations have passed. When the index is `0` it means that the current result is the top-most element of the stack; if it equals `count - 1` then it is the bottom-most element of the stack.

#### Declaration

> `FMOD bool PFX##_iter_prev(SNAME##_iter *iter, V *result, size_t *index);`

#### Parameters

1. `SNAME##_iter *iter` - Target iterator.
2. `V *result` - Resulting value from the stack.
3. `size_t *index` - Resulting index.

#### Returns 

1. `true` - If the iterator has retrieved a valid `result` and `index`.
2. `false` - If the iterator has not retrieved a valid `result` and `index`. Here, iteration to the previous element has ended.

#### Complexity

* O(1)

# [Queue](#collections_index)

A FIFO/LILO structure backed by a circular buffer. Elements are added in one end and removed from the other.

# [Deque](#collections_index)

A double-ended queue backed by a circular buffer. Elements can be added and removed from both ends but not in the middle. Can also be used as a queue.

# [Heap](#collections_index)

A heap is a nearly complete binary tree backed by a growable array. The first element of the array (or the root element of the tree) is the highest/lowest element. The min-heap is commonly used as a priority-queue and a max-heap is commonly used to sort an array of elements.

# [TreeSet](#collections_index)

A balanced binary tree that contains only unique elements to the set. Its elements are ordered.

# [TreeMap](#collections_index)

A balanced binary tree that maps a key `K` to a value `V`. The difference from a hashmap is that its keys are ordered.

# [HashSet](#collections_index)

A hashtable that contains only unique elements to the set. Its elements are not ordered.

# [HashMap](#collections_index)

A hashtable that maps a key `K` to a value `V`.
