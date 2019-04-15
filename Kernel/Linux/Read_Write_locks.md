Read / Write locks
------

[Article](https://stackoverflow.com/questions/932197/whats-the-best-linux-kernel-locking-mechanism-for-a-specific-scenario)

When you need to operate on critical variables / buffer you need to lock
access to a memory region.

Read lock:
```C
rwlock_t myrwlock = RW_LOCK_UNLOCKED;

read_lock(&myrwlock);             /* Acquire reader lock */
/* ... Critical Region ... */
read_unlock(&myrwlock);           /* Release lock */
```

Write lock:
```
rwlock_t myrwlock = RW_LOCK_UNLOCKED;

write_lock(&myrwlock);            /* Acquire writer lock */
/* ... Critical Region ... */
write_unlock(&myrwlock); /* Release lock */
```