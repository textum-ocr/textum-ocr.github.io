# Review Interface

Verify and correct recognized text in the side-by-side review interface.

<figure style="margin-bottom: 0;">
  <img src="/resources/screens/review.png" alt="Review Interface" style="border: 1px solid #ccc;">
  <figcaption style="text-align: center; font-style: italic; color: #666; margin-top: 0.5em; margin-bottom: 0;">Review interface with side-by-side text and image view. The cursor is on line 4 and the corresponding line is marked in the original image</figcaption>
</figure>

## Access

1. Go to [Job Control](job-control.md) view
3. Click the `Review` button on a job
4. Interface opens in new window

## Layout

- **Left** - Recognized text (editable)
- **Right** - Original image with detected text boxes (so-called _bounding box_)
- **Navigation** - Arrow keys or buttons to move between pages

## Editing (Left)

1. Click the text block to edit
2. Modify text
3. Save your changes using the `Save` button

The current line will be highlighted in the original image as a red box. You can turn off this behaviour using the `Show bounding boxes` switch.

The editing view preserves the original document's line breaks exactly as they appear in the source image. This means if a word was split across lines in the original document, it will remain split in the recognized text.

**Example**: If the original document has a line break in the middle of a word, like this:
```txt
The quick brown fox jumps ov-
er the lazy dog.
```
The word "over" appears split across two lines (`ov-` and `er`) because that's how it appeared in the original document. Textum preserves this formatting to match the original layout.

**Note**: No automatic merging of lines or words is performed. You can manually edit the text to combine split words or adjust line breaks if needed.

## Image view (Right)

- This is where the corresponding original input file will be displayed
- Zooming and panning is supported using the mouse and mouse wheel
- You can also use the `Zoom` buttons
- Double-click the image to reset the zoom level

### Unknown Words

If you selected a language during job creation, unknown words will be highlighted if they are not found in the language's dictionary file. This behaviour can be disabled by selecting `Unset` as a language during job creation. It is not possible to automatically remove all highlights for a completed job. It is also not possible to change the language used for spellchecking after the job was created.

The yellow highlighting is implemented using a special syntax. Every word or phrase that is enclosed by two equal signs (`==`) will be highlighted in yellow.

The highlighting is done so you can find possible text recognition mistakes quickly.

To correct a phrase and remove the highlighting, simply remove the enclosing equal signs (`==`). For example:

**Before** (with highlighting):
<pre style="background-color: #f5f5f5;"><code>The quick brown ==<mark style="background-color: #ffeb3b;">foxx</mark>== jumps over the lazy dog.</code></pre>

**After** (typo fixed, highlighting removed):
```txt
The quick brown fox jumps over the lazy dog.
```

<div style="background-color:rgb(254, 249, 232); padding: 10px; border-radius: 4px; margin: 10px 0;">
<strong>Visual example:</strong> The word <mark style="background-color: #ffeb3b;">foxx</mark> would appear highlighted in yellow in the interface. After correcting it to "fox" and removing the <code>==</code> markers, the highlighting disappears.
</div>

Because the highlighting is implemented in text text editor itself, you can also create your own highlightings! Just enclosed any word you are not sure of in equal signs: `==check this later==`. This is particularly useful if you need to do later research about a historical term, for example.

## Workflow

- Quickly scan some pages to make sure no grave errors happened

Review each page:

1. First check all highlights and correct them. Also remove the `==` markers.
2. Then go in depth and check each line
3. Save your progress on the current page using `Save` button
4. Mark the page as Done
5. Continue with the next page
6. After you're done reviewing all pages, export the whole transcription to various formats

The Mark as Done functionality is particularly useful for large inputs, as it allows you to track your progress within the document and continue at a later stage, exactly where you left off.
When you mark a page as done, a little checkmark shows up next to it in the page selector dropdown.

## Export

After reviewing, click Export or return to Job Control to export. Always save your progress.
