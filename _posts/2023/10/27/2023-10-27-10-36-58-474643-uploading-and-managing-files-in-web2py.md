---
layout: post
title: "[python] Uploading and managing files in Web2py"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Web2py is a versatile Python web framework that allows developers to build web applications efficiently. In this tutorial, we will explore how to upload and manage files using Web2py.

## Table of Contents
- [File Upload](#file-upload)
  - [HTML Form](#html-form)
  - [Server-side Handling](#server-side-handling)
  - [Storing Uploaded Files](#storing-uploaded-files)
- [File Management](#file-management)
  - [Listing Files](#listing-files)
  - [Deleting Files](#deleting-files)

## File Upload

### HTML Form

To enable file upload, we need to create an HTML form with an input field of type "file". Here's an example:

```html
<form action="{{=URL('upload')}}"
      enctype="multipart/form-data" method="POST">
  <input type="file" name="file">
  <input type="submit" value="Upload">
</form>
```

Make sure to set the `enctype` attribute to `"multipart/form-data"` to enable file uploads.

### Server-side Handling

In the web2py controller function that handles the file upload form submission, we can access the uploaded file using the `request.vars` dictionary. Here's an example:

```python
def upload():
    uploaded_file = request.vars.file
    # Do something with the uploaded file
    return "File uploaded successfully"
```

You can access various attributes of the uploaded file, such as `filename`, `file`, `content_type`, etc., to process and save the file as required.

### Storing Uploaded Files

To store the uploaded file, you can use the built-in `BLOB` field type in Web2py's database model. Create a model with a `BLOB` field to store the file data, and save the uploaded file to the database. Here's an example:

```python
db.define_table('uploaded_files',
                Field('file', 'upload'),
                Field('filename', 'string'),
                Field('content_type', 'string'))

def upload():
    uploaded_file = request.vars.file
    filename = uploaded_file.filename
    content_type = uploaded_file.headers['content-type']
    db.uploaded_files.insert(file=db.uploaded_files.file.store(uploaded_file.file),
                             filename=filename,
                             content_type=content_type)
    db.commit()
    return "File uploaded and saved successfully"
```

## File Management

### Listing Files

To list the uploaded files, retrieve the files from the database model and display them as needed. Here's an example:

```python
def list_files():
    files = db().select(db.uploaded_files.ALL)
    # Display the files in the view
    return dict(files=files)
```

### Deleting Files

To delete a file, you can simply remove the corresponding entry from the database using the `delete()` method. Here's an example:

```python
def delete_file():
    file_id = request.args(0)
    db(db.uploaded_files.id == file_id).delete()
    db.commit()
    return "File deleted successfully"
```

## Conclusion

Web2py provides convenient features for uploading and managing files within your web application. With a few simple steps, you can enable file uploads, handle file storage in the database, and manage the files effectively. Explore these features to enhance the file handling capabilities of your Web2py application.

References:
- [Web2py Framework Documentation](https://www.web2py.com/)
- [Web2py File Handling Documentation](https://www.web2py.com/books/default/chapter/29/09/files)