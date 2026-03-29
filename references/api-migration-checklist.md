# API Migration Checklist

Check items in the following order, apply minimal fixes when issues are found:

## 1. File/Proc Interfaces
- Check if `struct file_operations` needs migration to new field naming
- Check if `proc_create` scenarios should be changed to `proc_ops`
- Verify `open`, `release`, `read`, `write`, `ioctl` function signatures
- Check `llseek` and `poll` implementations for compatibility

## 2. Timer and Deferred Execution
- Verify `timer_setup` callback signature matches kernel version
- Check if tasklet/workqueue still符合 current context constraints
- Update `setup_timer` to `timer_setup` if needed
- Verify `del_timer` and `mod_timer` usage patterns

## 3. Resources and Lifecycle
- Prefer `devm_*` resource management functions
- Ensure `probe` failure paths completely release resources
- Check `remove` function symmetry with `probe`
- Verify `shutdown` and `suspend`/`resume` callbacks if present

## 4. Memory and Userspace Copy
- Properly handle `copy_to_user`/`copy_from_user` return values
- Check differences between old and new `get_user_pages*` calls
- Verify `vmalloc`/`kalloc` usage and error handling
- Check DMA mapping APIs (`dma_alloc_coherent`, etc.)

## 5. Interrupts and Concurrency
- Ensure `request_irq`/`free_irq` parameter consistency
- Verify spinlock/atomic/barrier semantics still valid
- Check IRQ handler signatures and return types
- Update `IRQF_*` flags to modern equivalents

## 6. Logging and Diagnostics
- Use `pr_*` functions instead of bare `printk` style
- Error paths must provide locatable logs
- Add appropriate log levels (`pr_err`, `pr_warn`, `pr_info`, `pr_debug`)
- Ensure `dev_*` logging functions are used with device context

## 7. Regression Points
- Module loading/unloading (`insmod`/`rmmod`)
- Basic IO path functionality
- `suspend`/`resume` if applicable
- Hotplug scenarios if supported
- Error injection and recovery testing

## 8. Security and Safety
- Use `strlcpy`/`strscpy` instead of `strncpy`
- Replace `snprintf` with `scnprintf` where appropriate
- Use `min_t`/`max_t` for type-safe comparisons
- Add bounds checking for array accesses
- Initialize variables before use

## 9. Compatibility Macros
- Check for `#ifdef CONFIG_` compatibility blocks
- Update deprecated macro usage
- Add version checks for conditional compilation
- Use `IS_ENABLED()` macro for config checks

## 10. Build System
- Verify `Kbuild`/`Makefile` dependencies
- Check module licensing (`MODULE_LICENSE`)
- Update `MODULE_AUTHOR` and `MODULE_DESCRIPTION`
- Ensure `MODULE_VERSION` if used