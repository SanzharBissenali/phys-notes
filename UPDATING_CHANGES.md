# How to Update Code Changes in Quarto

## Quick Steps to Update Changes

1. **Save your files** - Make sure all `.qmd` and `_quarto.yml` files are saved
2. **Wait for auto-refresh** - Quarto preview should automatically detect changes and refresh
3. **Hard refresh browser** - If you don't see changes: `Cmd+Shift+R` (Mac) or `Ctrl+Shift+R` (Windows/Linux)

## If Website Stops Working

### Step 1: Check for Errors

Look at your terminal where `quarto preview` is running. Common errors:

- **"Book chapter 'file.qmd' not found"** - File is referenced in `_quarto.yml` but doesn't exist
- **Syntax errors** - Check YAML formatting in `_quarto.yml`
- **Broken links** - Check that files referenced in `.qmd` files actually exist

### Step 2: Fix Configuration Issues

If you get "file not found" errors:

1. **Check `_quarto.yml`** - Make sure all files listed in `chapters:` actually exist
2. **Check file paths** - Ensure paths are correct (e.g., `physics5/experiment1.qmd`)
3. **Remove references to deleted files** - If you deleted a file, remove it from `_quarto.yml`

### Step 3: Restart Preview Server

```bash
# Stop the preview server (Ctrl+C in terminal)
# Then restart:
cd /path/to/your/project
quarto preview
```

### Step 4: Clear Cache (if needed)

If changes still don't appear:

```bash
# Clear Quarto cache
rm -rf _book/.quarto .quarto

# Restart preview
quarto preview
```

## Common Issues and Solutions

### Issue: "File not found" error after deleting files

**Solution**: Update `_quarto.yml` to remove references to deleted files, or update references to point to new files.

**Example**: If you deleted `chapter1.qmd` and created `experiment1.qmd`, update:
```yaml
# Before:
- physics5/chapter1.qmd

# After:
- physics5/experiment1.qmd
```

### Issue: Changes not appearing in browser

**Solutions**:
1. **Save the file** (most common issue - unsaved changes)
2. **Hard refresh**: `Cmd+Shift+R` or `Ctrl+Shift+R`
3. **Check terminal** for rendering errors
4. **Clear browser cache**

### Issue: Preview server won't start

**Solutions**:
1. Check for syntax errors in `_quarto.yml`
2. Verify all referenced files exist
3. Check for YAML formatting errors (proper indentation, no tabs)
4. Clear cache: `rm -rf _book/.quarto .quarto`

## File Organization Checklist

Before editing, make sure:

- [ ] All files referenced in `_quarto.yml` exist
- [ ] All links in `.qmd` files point to existing files
- [ ] File paths are correct (case-sensitive on Linux/Mac)
- [ ] YAML syntax in `_quarto.yml` is correct

## Best Practices

1. **Save frequently** - Quarto watches for file changes, but only sees saved files
2. **Check terminal output** - Errors appear in the preview server terminal
3. **Test incrementally** - Make small changes and verify they work
4. **Use version control** - Git helps track what changed if something breaks

## Troubleshooting Checklist

- [ ] Files are saved
- [ ] No unsaved changes in editor
- [ ] `_quarto.yml` syntax is correct
- [ ] All referenced files exist
- [ ] Preview server is running
- [ ] Browser is hard refreshed
- [ ] No errors in terminal
- [ ] Cache cleared (if needed)
