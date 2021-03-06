---
title: allocate
---
*allocate* - allocate virtual memory

# LIBRARY
library "libcgc"

# SYNOPSIS

~~~ c
#include <libcgc.h>

int allocate(size_t length, int is_X, void **addr)
~~~

# DESCRIPTION
The `allocate` system call creates a new allocation in the virtual address
space of the calling process. The length argument specifies the length of
the allocation in bytes which will be rounded up to the hardware page size
(4KB for IA32).

The kernel chooses the address at which to create the allocation;
the address of the new allocation is returned in `*addr`
as the result of the call, and is always page aligned.

All newly allocated memory is zero-filled, readable, and writeable.
In addition, the `is_X` argument is a boolean that allows newly allocated
memory to be marked as executable (non-zero) or non-executable (zero).

The allocate function is invoked through system call number 5.

# RETURN VALUE
On success, `allocate` returns zero and a pointer to the allocated area
is returned in `*addr`. Otherwise, an error code is returned and
`*addr` is undefined.

# ERRORS

`EINVAL`
: `length` is zero.

`EINVAL`
: `length` is too large.

`EFAULT`
: `addr` points to an invalid address.

`ENOMEM`
: No memory is available or the process' maximum number of allocations would have been exceeded.


# SEE ALSO
[cgcabi(2)](/libcgc/cgcabi/),
[deallocate(2)](/libcgc/deallocate/),
[fdwait(2)](/libcgc/fdwait/),
[random(2)](/libcgc/random/),
[receive(2)](/libcgc/receive/),
[_terminate(2)](/libcgc/terminate/),
[transmit(2)](/libcgc/transmit/)
