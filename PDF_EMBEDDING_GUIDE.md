# PDF Embedding Guide for Quarto

This guide explains how to add PDF files to your Quarto pages, either as links or as embedded scrollable elements.

## Method 1: Simple Link to PDF

This creates a clickable link that opens the PDF in a new tab or downloads it.

### Syntax:

```markdown
[Link Text](http://example.com/file.pdf){target="_blank"}
```

### Example:

```markdown
[**Download Experiment 1 PDF**](http://sophphx.caltech.edu/Physics_5/Experiment_1.pdf){target="_blank"}
```

The `{target="_blank"}` attribute makes the link open in a new tab, which is recommended for external PDFs.

---

## Method 2: Embedded PDF Viewer (Scrollable)

This embeds the PDF directly in the page as a scrollable element.

### Basic Syntax:

```markdown
<iframe src="http://example.com/file.pdf" width="100%" height="800px" style="border: 1px solid #ddd; border-radius: 4px;">

Your browser does not support PDFs. [Download the PDF instead](http://example.com/file.pdf){target="_blank"}.

</iframe>
```

### Example:

```markdown
<iframe src="http://sophphx.caltech.edu/Physics_5/Experiment_1.pdf" width="100%" height="800px" style="border: 1px solid #ddd; border-radius: 4px;">

Your browser does not support PDFs. [Download the PDF instead](http://sophphx.caltech.edu/Physics_5/Experiment_1.pdf){target="_blank"}.

</iframe>
```

### Attributes:

- `width="100%"` - Makes the iframe span the full width of the container
- `height="800px"` - Sets the height (adjust as needed)
- `style="border: 1px solid #ddd; border-radius: 4px;"` - Adds a nice border (optional)

### Advanced: Responsive Height with CSS

If you want a more responsive solution, you can wrap it in a div with custom CSS:

```markdown
::: {#pdf-embed}

<iframe src="http://example.com/file.pdf" width="100%" height="800px" style="border: 1px solid #ddd; border-radius: 4px; min-height: 600px;">

Your browser does not support PDFs. [Download the PDF instead](http://example.com/file.pdf){target="_blank"}.

</iframe>

:::
```

---

## Method 3: Using Local PDF Files

If you want to store PDFs locally in your repository:

### Step 1: Create a folder for PDFs

```bash
mkdir -p pdfs
```

### Step 2: Copy your PDF into that folder

```bash
cp /path/to/experiment1.pdf pdfs/
```

### Step 3: Reference it in your `.qmd` file

```markdown
<!-- Link method -->
[**Download Experiment 1 PDF**](pdfs/experiment1.pdf){target="_blank"}

<!-- Embed method -->
<iframe src="pdfs/experiment1.pdf" width="100%" height="800px" style="border: 1px solid #ddd; border-radius: 4px;">

Your browser does not support PDFs. [Download the PDF instead](pdfs/experiment1.pdf){target="_blank"}.

</iframe>
```

**Note**: Make sure to add the `pdfs/` folder to your git repository if you want the PDFs to be version controlled.

---

## Important Considerations

### Browser Compatibility

- **Chrome/Edge**: Usually works well with embedded PDFs
- **Firefox**: May require PDF.js or prefer to open in new tab
- **Safari**: Sometimes has issues with embedded PDFs; users may need to download

### CORS (Cross-Origin Resource Sharing)

If you're embedding a PDF from an external server:
- The server must allow embedding (via CORS headers)
- If CORS blocks embedding, users will see an error; provide a fallback link
- Local PDFs don't have this issue

### File Size

- Large PDFs may take time to load
- Consider providing both link and embed options
- For very large files (>50MB), the link method is often better

### Mobile Devices

- Embedded PDFs may not work well on mobile browsers
- Always provide a link as a fallback

---

## Example: Complete Implementation

Here's a complete example combining both methods with proper formatting:

```markdown
## Experiment 1: Introductory Electronics Laboratory

The first experiment covers analog circuits and operational amplifiers.

### Option 1: Link to PDF

[**Download Experiment 1 PDF**](http://sophphx.caltech.edu/Physics_5/Experiment_1.pdf){target="_blank"}

This link will open the PDF in a new browser tab.

### Option 2: Embedded PDF Viewer

The experiment document is also available as an embedded, scrollable viewer below:

::: {#pdf-embed}

<iframe src="http://sophphx.caltech.edu/Physics_5/Experiment_1.pdf" width="100%" height="800px" style="border: 1px solid #ddd; border-radius: 4px;">

Your browser does not support PDFs. [Download the PDF instead](http://sophphx.caltech.edu/Physics_5/Experiment_1.pdf){target="_blank"}.

</iframe>

:::

::: {.column-margin}
**Note**: If the PDF doesn't display in the embedded viewer, your browser may require the PDF to open in a new tab instead. You can always use the download link above.
:::
```

---

## Troubleshooting

### PDF doesn't display in iframe

1. **Check CORS**: The external server may not allow embedding
2. **Try the link method instead**: Some servers block embedding for security
3. **Check browser console**: Look for CORS or security errors
4. **Use local PDF**: Download and host the PDF locally if embedding is required

### PDF loads slowly

1. **Consider file size**: Large PDFs take time to download
2. **Provide link alternative**: Let users choose to download if needed
3. **Lazy loading**: You could add `loading="lazy"` to the iframe (though this may not work for PDFs)

### PDF doesn't work on mobile

1. **Always provide a link**: Mobile browsers often handle PDFs differently
2. **Test on multiple devices**: What works on desktop may not work on mobile
3. **Consider responsive design**: You might want different layouts for mobile

---

## Best Practices

1. **Always provide both options**: Link + embed gives users flexibility
2. **Include fallback text**: The text inside the iframe shows if embedding fails
3. **Use descriptive link text**: "Download Experiment 1 PDF" is better than "Click here"
4. **Test in multiple browsers**: Ensure compatibility across browsers
5. **Consider accessibility**: Screen readers may have issues with embedded PDFs; links are more accessible
6. **Add context**: Explain what the PDF contains before linking/embedding
