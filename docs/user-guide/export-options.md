# Export Options

Export recognized text in multiple formats from the Review Interface or Job Control.

<div style="display: flex; gap: 1em; flex-wrap: wrap; margin: 1em 0;">
  <figure style="flex: 0 0 30%; margin: 0;">
    <img src="/resources/screens/export-picker.png" alt="Export Picker" style="border: 1px solid #ccc; width: 100%;">
    <figcaption style="text-align: center; font-style: italic; color: #666; margin-top: 0.5em; margin-bottom: 0;">Export selector</figcaption>
  </figure>
  <figure style="flex: 0 0 60%; margin: 0;">
    <img src="/resources/screens/export-dialog.png" alt="Export Dialog" style="border: 1px solid #ccc; width: 100%;">
    <figcaption style="text-align: center; font-style: italic; color: #666; margin-top: 0.5em; margin-bottom: 0;">Export formats</figcaption>
  </figure>
</div>

## Formats

### Plain Text (.txt)
- Basic text only
- Smallest file size
- Universal compatibility
- Pages are delimited by `===== Page X =====`

### DOCX (Microsoft Word)
- Editable in Word
- Preserves basic structure
- Pages are delimited by a new headline `Page X`

### PDF
- This export option is mostly provided for cross-platform compatibility
- Pages are delimited by `===== Page X =====`

## Export Process

1. Click Export button. Select if only current page (available from Review) or all pages (available from Review and Job Control View) should be exported.
2. Choose format: Plain Text, DOCX, or PDF
3. If you selected a language during job creation, unknown words were highlighted using word lists. Per default, highlight markers (`==this text will be highlighted==`) are not exported.
4. Select destination
5. Export complete
