# Effective Modern C++
## Deducing Types
### 1. Understand template type deduction
### 2. Understand auto type deduction
### 3. Understand decltype
### 4. Know how to view deduced types

## auto
### 5. Prefer auto to explicit type declarations
### 6. Use the explicitly typed initializer idiom when auto deduces undesired types

## Moving to Modern C++
### 7. Distinguish between () and {} when creating objects
### 8. Prefer nullptr to 0 or NULL
### 9. Prefer alias declarations to typedefs
### 10. Prefer scoped enums to unscoped enums
### 11. Prefer deleted functions to private undefined ones
### 12. Declare overriding functinos override
### 13. Prefer const_iterators to iterators
### 14. Declare functions noexcept if they won't emit exceptions
### 15. Use constexpr whenever possible
### 16. Make const member functions thread safe
### 17. Understand special member function generation.

## Smart Pointers
### 18. Use std::unique_ptr for exclusive-ownership resource management
### 19. Use std::shared_ptr for shared-ownership resource management
### 20. Use std::weak_ptr for std::shared_ptr-like pointers that can dangle
### 21. Prefer std::make_unique and std::make_shared to direct use of new
### 22. When using the Pimpl Idiom, define special member functions in the implementation file

## Rvalue References, Move Semantics, and Perfect Forwarding
### 23. Understand std::move and std::forward
### 24. Distinguish universal references from rvalue references
### 25. Use std::move on rvalue references, std::forward on universal references
### 26. Avoid overloading on universal references
### 27. Familiarize yourself with alternatives to overloading on universal references
### 28. Understand reference collapsing
### 29. Assume that move operations are not present, not cheap, and not used.
### 30. Familiarize yourself with perfect forwarding failure cases


## Lambda Expressions
### 31. Avoid default capture modes
### 32. Use init capture to move objects into closures
### 33. Use decltype on auto&& parameters to std::forward them
### 34. Prefer lambdas to std::bind


## The Concurrency API
あんまり使ったことがないため改でちゃんと見る必要がある
### 35. Prefer task-based programming to thread-based.
### 36. Specify std::launch::async if asynchronicity is essential
### 37. Make std::treads unjoinable on all paths
### 38. Be aware of varying thread handle destructor behavior
### 39. Consider void futures for one-shot event communication
### 40. Use std::atomic for concurrency, volatile for special memory

## Tweaks
### 41. Consider pass by value for copyable parameters that are cheap to move and always copied
### 42. Consider emplacement instead of insertion

# Effective C++
