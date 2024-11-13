---
date: 2024-11-09
excerpt: a convenient way to define cascading behavior for foreign keys when a referenced record is deleted
---
The `cascadeOnDelete()` method is a convenient way to define cascading behavior for foreign keys when a referenced record is deleted.

#### Behavior

- Automatically deletes the rows in the child table if the related row in the parent table is deleted.

#### Example

```
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->foreignId('user_id')->constrained()->cascadeOnDelete();
    $table->timestamps();
});
```

This ensures that if a user is deleted, all their related posts will also be deleted.


Status: #idea
Tags: [[web-programming]]

---
# References