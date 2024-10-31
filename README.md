# Tags-Releases
Working with GitHub Tags and Releases


# Git Tagging Guide

Git tags are a useful way to mark specific points in your project’s history. There are two types of tags: **Annotated Tags** and **Lightweight Tags**. Annotated tags are recommended when you need additional metadata, such as a message and author information.

## Annotated Tags

Annotated tags allow you to add a message and other metadata to the tag. They are created using the `-a` option along with a version number and a message.

### Creating an Annotated Tag

To create an annotated tag:

```bash
git tag -a v1.2.2 -m "This is my first annotated tag"