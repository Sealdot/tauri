---
"tauri": patch:bug
---

Fix the iOS debug stdout/stderr redirector deadlocking when `OS_ACTIVITY_DT_MODE` is set: os_log mirrors each record to stderr in a plain format without the `OSLOG-` prefix, so the recursion guard let every mirrored line feed back through os_log until the pipe filled. Mirrored lines are now also recognized by their `<process>[<pid>:` header and passed to the original fd.
