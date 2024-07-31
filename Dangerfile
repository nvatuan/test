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

UNSAFE_MAX_DISPLAY = 10
curr = 0
if unsafe_files.any?
  unsafe_files.each { |file|
    if curr >= UNSAFE_MAX_DISPLAY
      fail("... and #{unsafe_files.length - UNSAFE_MAX_DISPLAY} more")
      break
    end
    fail("`#{file}`")
    curr += 1
  }

  markdown << ":warning: **Require manual reviews. Found above unsafe files on PR.**"
    << "_Despite the failure, you can still manually merge the PR. The failure is for disable automatic merge._"
end
