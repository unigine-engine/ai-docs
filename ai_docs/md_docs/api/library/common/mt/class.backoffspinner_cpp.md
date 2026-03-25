# Unigine::BackoffSpinner Class (CPP)

**Header:** #include <UnigineThread.h>

This class implements exponential backoff mechanism for the [SpinLock](../../../../api/library/common/class.unigine.namespace_cpp.md#SpinLockTemplate_volatiletmplptr_consttmpl_consttmpl) reducing the impact on CPU performance.


## BackoffSpinner Class

### Members

---

## static BackoffSpinner ( )

Constructor. Creates a new Backoff Spinner.
## void spin ( )

Implements adaptive backoff by progressively increasing wait intervals. Begins with exponentially growing CPU pause instructions based on an internal counter; after reaching a threshold, yields to allow other threads to execute. Increments the backoff counter on each invocation.
## void clear ( )

Resets the internal backoff counter to zero, restarting the exponential backoff sequence from the beginning.
