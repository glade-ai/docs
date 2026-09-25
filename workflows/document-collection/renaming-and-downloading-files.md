# Renaming and Downloading Files

## Overview

Firm staff can rename documents collected on a case, and Glade keeps the name shown in Glade — along with the correct file type — when a file is downloaded, opened from a link, or imported from another system. This page covers manual renaming and how file names carry through downloads and imports. For bulk AI-suggested renames, see [AI-Suggested File Names](./ai-suggested-file-names.md).

## Key Behaviors

- Documents can be renamed by firm staff working from the dashboard by clicking the document's name in the detail pane. While you edit a name, the full name stays visible even when it is long, the cursor stays where you are typing (it does not jump to the front on fast typing), and pressing the space bar inserts a space rather than opening the document. The updated name saves when you click away and is reflected in the checklist view; leaving the field empty or unchanged keeps the previous name.
- Clients viewing the same documents in the client portal do not see a rename affordance — file names submitted by clients are not editable from the client side. The submit-for-review AI rename prompt is also limited to firm dashboard users.
- When you download a renamed file from the dashboard, it downloads under the name shown in Glade, keeping the original file extension. Previously a download reverted to the file's underlying storage name (often a string of random letters and numbers), which meant staff had to rename the file by hand after every download. Files that were never renamed continue to download under their stored name.
- **A file opened from a shared or emailed link keeps its name too.** Documents reached this way used to save to your computer as a string of letters and numbers with no file extension, so a PDF did not open by double-clicking it and had to be renamed by hand. They now open in the preview as they should, and save under the name and file type Glade holds for them.
- **Documents brought over from MyCase keep their names and open in the preview.** MyCase hands its files across without saying what type they are, so imported PDFs and images arrived unreadable in the preview and downloaded without an extension. Imported files now carry their real file name and type.

## Edge Cases & Limitations

- The MyCase import fix applies to imports run after the change — if your firm was migrated earlier and has documents that will not preview, contact support.

## Related Features

- [Document Collection](./README.md)
- [AI-Suggested File Names](./ai-suggested-file-names.md)
- [Previewing Documents](./previewing-documents.md)
- [The Documents Tab](./documents-tab.md)
