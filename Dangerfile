## Add prefix of files that are safe to change
## Note that this is "prefix", so "folder/test" still matches with "folder/test123"
SAFE_PREFIXES = [
  "README.md",
  "safe/",
  "unsafe/safenote"
]

## git.added_files, git.modified_files are automatically available
changed_files = (git.added_files + git.modified_files)

### Danger rules below:

unsafe_files = changed_files.reject { |file|
  SAFE_PREFIXES.any? { |prefix|
    file.start_with?(prefix)
  }
}

if unsafe_files.any?
  fail("Require manual reviews. Found these unsafe files on PR: #{unsafe_files}")
end