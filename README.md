# Tags-Releases
Working with GitHub Tags and Releases


# Git Tagging Guide

Git tags are a useful way to mark specific points in your project’s history. There are two types of tags: **Annotated Tags** and **Lightweight Tags**. Annotated tags are recommended when you need additional metadata, such as a message and author information.

## Annotated Tags

Annotated tags allow you to add a message and other metadata to the tag. They are created using the `-a` option along with a version number and a message.

### Creating an Annotated Tag

To create an annotated tag:

```bash
git tag -a <tag_name> -m "<tag_message>"
For example:
git tag -a v1.2.2 -m "This is my first annotated tag"

In this example, v1.2.2 is the tag name, and "This is my tag no 1" is the message associated with the tag.

```
### Viewing All Tags

To view all tags in a repository along with a short description of each, use the following command:

```bash
git tag -l -n<number_of_lines>

Where:

-l lists all tags.
-n specifies the number of lines from the message to display with each tag.

For example, to list all tags with the first three lines of each message, use:

git tag -l -n3

v1.0            Release version 1.0
v1.1            Release version 1.1
v1.2            Release version 1.2

Where n3 means show 3 number of lines in the message