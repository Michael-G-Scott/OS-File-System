# Filesystem Design Overview

## Filesystem Initialization (`mkfs`)
- **Initialize Components**:
  - Superblock, inodes, and data blocks in the os file.
  - Root inode setup as directory.

- **Superblock**:
  - Disk size, root inode, block sizes, bitmaps.
  - Initialize root directory inode.

## Mounting the Filesystem
- **Mapping**:
  - Map os file to a drive letter (e.g., C:).
  - Update root inode name to match drive letter.

## Copy Command (`cp`)
- **Two Cases**:
  - Copying from os file to filesystem.
  - Copying within filesystem.

- **Process**:
  - Read source file.
  - Write data to available data blocks.
  - Update inode and superblock metadata.

## Key Structures

- **Superblock**:
  - Disk size, block sizes, start locations, bitmaps.

- **Inode**:
  - Type, name, size, data block references.

- **Metadata**:
  - File name, type, inode number, permissions.

## Commands Implementation

### `mkfs`
- Allocate superblock, inodes, and data blocks.
- Initialize root directory inode.

### Mounting
- Map drive name, update root inode.

### `cp`
- Read source file, copy data to data blocks.
- Update inode and superblock.

## Example Usage

```python
# Initialize filesystem
create_filesystem("osfile", 1024, 1048576)

# Mount filesystem as C:
mount_filesystem("osfile", "C:")

# Copy file into filesystem
cp("sourcefile", "C:targetfile")
