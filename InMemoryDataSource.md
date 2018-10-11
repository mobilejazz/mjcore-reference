# InMemoryDataSource

`InMemoryDataSource<T>` is a key-value storage that implements `GetDataSource`, `PutDataSource` and `DeleteDataSource` storing values as live references during the instance life cycle.

## Usage

```swift
// Swift
let dataSource = InMemoryDataSource<Double>()
dataSource.put(3.14159265359, forId: "pi")
dataSource.get("pi").then { pi in print("pi: \(pi)") }.fail { error in }
dataSource.delete("pi")
```

```kotlin
// Kotlin
// TODO
```

Note that the example above is using the extension methods of DataSoruce that encapsulate queries of type `IdQuery<T>`/`ByIdentifierQuery<T>`.

## Query Types

All queries must adopt the [`KeyQuery`](query.md) interface as the `InMemoryDataSource<T>` is based on a key-value pattern.

## Object Types

Any object of type T can be stored in a `InMemoryDataSource<T>`, and there are no restrictions of type.

## Implementation Notes

All objects and arrays are stored in dictionaries that are kept alive as long as the  `InMemoryDataSource<T>` instance is alive.

Objects interfaced with the `get`, `put` and `delete` functions are stored in separate dictionaries than arrays of objects interfaced via the `getAll`, `putAll` and `deleteAll` functions.

```swift
// Swift
public class InMemoryDataSource<T> : GetDataSource, PutDataSource, DeleteDataSource  {

    private var objects : [String : T] = [:] // get, put delete
    private var arrays : [String : [T]] = [:] // getAll, putAll, deleteAll
    
    [ ... ] // The rest of the class implementation
}
```

```kotlin
// Kotlin
// TODO
```