# Repository Structure Guide

## Current Repository Structure

This is a **Quarto Book** project that builds a physics course website. Here's how it's organized:

### Core Files

- **`_quarto.yml`** - Main configuration file that defines:
  - Book structure (chapters, appendices)
  - Website appearance and behavior
  - Rendering settings
  
- **`index.qmd`** - The landing/home page of the book

- **`*.qmd` files** - Chapter source files (Quarto Markdown format):
  - `mechanics.qmd`
  - `thermodynamics.qmd`
  - `electromagnetism.qmd`
  - etc.

### Directory Structure

```
notes/
├── _quarto.yml              # Book configuration
├── index.qmd                # Home page
├── *.qmd                    # Chapter files (at root level)
├── _book/                   # Generated HTML output (DON'T EDIT)
├── _extensions/             # Quarto extensions (imagify, pseudocode)
├── figures/                 # Shared figures/templates
├── logo/                    # Website logos and favicons
├── style.css                # Custom CSS styling
└── resources/               # Additional resources (referenced in config)
```

## How to Add a New Page

### Option 1: Add a Simple Chapter at Root Level

1. **Create a new `.qmd` file** in the root directory:
   ```bash
   touch new_chapter.qmd
   ```

2. **Add content** to the file with a heading and section ID:
   ```markdown
   # New Chapter Title {#sec-new-chapter}
   
   Your content here...
   ```

3. **Add it to `_quarto.yml`** under the `chapters:` section:
   ```yaml
   book:
     chapters:
       - index.qmd
       - mechanics.qmd
       # ... existing chapters ...
       - new_chapter.qmd     # Add your new chapter here
     appendices:
       - mathematical_methods.qmd
       - laboratory_techniques.qmd
   ```

4. **Update `index.qmd`** to add a link to your new chapter in the course structure section.

### Option 2: Add to a Specific Part/Folder

See the "Creating Parts/Folders" section below.

---

## How to Create Parts (Folders/Sections)

Quarto supports organizing chapters into **Parts**, which create collapsible sections in the sidebar. This is perfect for organizing "Physics 5", "Physics 6", "Physics 7", etc.

### Method 1: Using Parts in `_quarto.yml`

Edit `_quarto.yml` to organize chapters into parts:

```yaml
book:
  title: Physics Course - Introduction to Physics
  chapters:
    - index.qmd
    
    # Part I: Core Physics Topics
    - part: physics-5
      chapters:
        - physics5/chapter1.qmd
        - physics5/chapter2.qmd
        - physics5/chapter3.qmd
    
    # Part II: Advanced Topics
    - part: physics-6
      chapters:
        - physics6/topic1.qmd
        - physics6/topic2.qmd
    
    # Part III: Specialized Topics
    - part: physics-7
      chapters:
        - physics7/special_topic1.qmd
        - physics7/special_topic2.qmd
    
    # Keep existing chapters (can also move them into parts)
    - mechanics.qmd
    - thermodynamics.qmd
    # etc.
    
```

### Method 2: Using Part Files (Alternative)

You can create part title files:

1. **Create a folder structure:**
   ```
   physics5/
     ├── index.qmd          # Part title/intro
     ├── chapter1.qmd
     ├── chapter2.qmd
     └── chapter3.qmd
   
   physics6/
     ├── index.qmd
     ├── topic1.qmd
     └── topic2.qmd
   ```

2. **In `_quarto.yml`, use part entries:**
   ```yaml
   book:
     chapters:
       - index.qmd
       
       - part: Physics 5
         chapters:
           - physics5/index.qmd
           - physics5/chapter1.qmd
           - physics5/chapter2.qmd
           - physics5/chapter3.qmd
       
       - part: Physics 6
         chapters:
           - physics6/index.qmd
           - physics6/topic1.qmd
           - physics6/topic2.qmd
   ```

3. **Create part intro files** (optional):
   In `physics5/index.qmd`:
   ```markdown
   # Physics 5 {#part-physics5}
   
   Welcome to Physics 5. This section covers...
   
   ## Topics Covered
   
   - [Chapter 1](chapter1.qmd)
   - [Chapter 2](chapter2.qmd)
   ```

### Complete Example: Setting Up Physics 5, 6, 7

Here's a complete example of how to set this up:

**Step 1: Create the folder structure**
```bash
mkdir -p physics5 physics6 physics7
```

**Step 2: Create chapter files in each folder**
```bash
# In physics5/
touch physics5/intro.qmd
touch physics5/chapter1.qmd
touch physics5/chapter2.qmd

# In physics6/
touch physics6/intro.qmd
touch physics6/topic1.qmd
touch physics6/topic2.qmd

# In physics7/
touch physics7/intro.qmd
touch physics7/advanced1.qmd
touch physics7/advanced2.qmd
```

**Step 3: Add content to each file**
Each `.qmd` file should start with:
```markdown
# Chapter Title {#sec-unique-id}

Content here...
```

**Step 4: Update `_quarto.yml`**
```yaml
book:
  chapters:
    - index.qmd
    
    # Physics 5 Section
    - part: Physics 5
      chapters:
        - physics5/intro.qmd
        - physics5/chapter1.qmd
        - physics5/chapter2.qmd
    
    # Physics 6 Section
    - part: Physics 6
      chapters:
        - physics6/intro.qmd
        - physics6/topic1.qmd
        - physics6/topic2.qmd
    
    # Physics 7 Section
    - part: Physics 7
      chapters:
        - physics7/intro.qmd
        - physics7/advanced1.qmd
        - physics7/advanced2.qmd
    
    # Existing chapters (can keep at root or move into parts)
    - mechanics.qmd
    - thermodynamics.qmd
    - electromagnetism.qmd
    - waves.qmd
    - optics.qmd
    - quantum.qmd
    - modern_physics.qmd
```

**Step 5: Restart the preview server**
The website will automatically update when you save changes. If needed, restart:
```bash
# Stop current server (Ctrl+C), then:
quarto preview
```

## Important Notes

1. **File Paths**: When referencing files in folders, use relative paths from the project root.

2. **Cross-references**: Use section IDs for cross-references:
   ```markdown
   See @sec-mechanics for more details.
   ```

3. **Images/Figures**: Place images in a `figures/` folder or alongside your `.qmd` files. Reference them as:
   ```markdown
   ![Caption](path/to/image.png)
   ```

4. **Part Titles**: The `part:` name in `_quarto.yml` will appear as the section title in the sidebar.

5. **Auto-reload**: When running `quarto preview`, changes to `.qmd` files and `_quarto.yml` will automatically refresh the browser.

## Example: Adding a New Chapter to Physics 5

1. Create `physics5/new_topic.qmd`:
   ```markdown
   # New Topic in Physics 5 {#sec-physics5-new}
   
   Content about this new topic...
   ```

2. Add to `_quarto.yml` under the Physics 5 part:
   ```yaml
   - part: Physics 5
     chapters:
       - physics5/intro.qmd
       - physics5/chapter1.qmd
       - physics5/chapter2.qmd
       - physics5/new_topic.qmd  # Add here
   ```

3. Save and the website will update automatically!

---

## Tips

- **Section IDs**: Always use unique IDs in curly braces `{#sec-id}` for each heading. This enables cross-referencing.

- **Part Organization**: Parts create collapsible sections in the sidebar, making navigation easier for large books.

- **Nesting**: You can nest parts, but it's generally better to keep the structure flat for clarity.

- **File Naming**: Use lowercase with underscores or hyphens for file names (e.g., `chapter_1.qmd` or `chapter-1.qmd`).
