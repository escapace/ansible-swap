# ansible-swap

Prepares a persistent swap file for RHEL-family version 10 golden images. The
role creates and verifies the file, records it in `/etc/fstab`, and configures
`vm.swappiness` for the next boot. It does not activate or deactivate swap and
does not change the running kernel's swappiness.

## Variables

- `swap_file_path` defaults to `/swapfile`. It must be an absolute path without
  whitespace, and its parent directory must already exist.
- `swap_file_size` defaults to `1gb`. It accepts numbers with case-insensitive
  byte suffixes such as `512mb`, `1GB`, or `1.5gb`; a unitless value represents
  MiB. Unit prefixes use binary powers, the minimum size is one MiB, and IEC
  suffixes such as `MiB` are not accepted.
- `swap_swappiness` defaults to `60`; it must be an integer from 0 through 100.

The platform-provided `/etc/sysctl.d` directory must already exist. An existing
swap file can be replaced when its size differs and it is not active. The role
refuses to replace an active swap file or an existing destination that is not a
valid swap file.
