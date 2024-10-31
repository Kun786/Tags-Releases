# Tags-Releases
<p>Working with GitHub Tags and Releases</p>


# Git Tags Guide

<p>Git tags are a useful way to mark specific points in your project’s history. There are two types of tags: **Annotated Tags** and **Lightweight Tags**. Annotated tags are recommended when you need additional metadata, such as a message and author information.</p>

## Annotated Tags

<p>Annotated tags allow you to add a message and other metadata to the tag. They are created using the `-a` option along with a version number and a message.</p>

### Creating an Annotated Tag

<p>To create an annotated tag:</p>

```bash
git tag -a <tag_name> -m "<tag_message>"
For example:
git tag -a v1.2.2 -m "This is my first annotated tag"

In this example, v1.2.2 is the tag name, and "This is my tag no 1" is the message associated with the tag.

```
### Viewing All Tags

<p>To view all tags in a repository along with a short description of each, use the following command:</p>

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

```

### Viewing Tag Details
<p>To get detailed information about a specific tag, use git show <tag_identifier>. This command shows the following information:</p>

1. Tag name
2. Tagger (name and email)
3. Date of the tag
4. Message included with the tag
5. Optional PGP signature if the tag is signed
6. Information about the associated commit

```bash

For example:
git show v1.0

This command would provide output similar to:
tag v1.0
Tagger: Kolosek 
Date:   Fri May 11 10:45:33 2018 +0100

Release version 1.0
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1

iMTvhAA...
-----END PGP SIGNATURE-----

commit 7d44b6bb8abb96dee33f32610f56441496d77e8a
Author: Kolosek 
Date:   Fri May 11 9:50:13 2018 +0100

    Edited the Login form
...

```

#### Breakdown of Information
1. Tagger's name and email: The person who created the tag.
2. Creation date: The date the tag was created.
3. Message: The custom message added when the tag was created.
4. PGP Signature (if available): Signature for verification.
5. Commit Details: Information about the commit the tag points to.

### Lightweight Tags
<p>If you create a tag without the -a option, it will be a lightweight tag. This type of tag does not contain metadata such as the message or tagger details, serving only as a pointer to a specific commit.</p>

### Tag Version Conflicts
<p>If you try to create a tag with an identifier that already exists, Git will throw an error. You must delete or rename the existing tag if you want to reuse the same version name.</p>

### Deleting a Tag

To delete a tag, use the following command:

```bash
To delete a tag, use the following command:

git tag -d <tag_identifier>

For example:

git tag -d v1.0

This command will remove the tag v1.0 from the local repository.
```

# Git Releases Guide
<p>Release are extra information or metadat to the tags which create the Tags more structured and documented you tags, making it easier for teams and users to find, understand, and deploy stable versions of your software. They turn tags into well-documented, downloadable milestones.</p>

Here is the list of information that Release add to tags

#### 1. Enhanced Visibility and Organization:
<p>Releases are more visible on GitHub, with their own section (under the Releases tab), making it easier for users to locate stable versions and download them.
They’re marked with colored, capsule-style labels, improving the clarity and visual appeal of your version history.</p>

#### 2. Detailed Release Notes:
<p>You can add descriptions and release notes to explain what’s new, improved, or fixed in each release. This context is invaluable for team members, contributors, and users who want to understand the changes without diving into the code.
You can summarize key features, bug fixes, or even link to related issues and pull requests.</p>

#### 3. Downloadable Assets:
<p>Releases allow you to attach additional files, like compiled binaries, documentation, or other resources, which are downloadable as part of the release package.
GitHub automatically provides .zip and .tar.gz archives of the code, making it easy for users to download the exact state of the code for that version.</p>

#### 4. Integration with CI/CD and Deployment Pipelines:
<p>Many CI/CD systems can trigger builds or deployments based on GitHub Releases. This makes it easier to automate deployments, tests, or notifications when a new stable version is published.
Releases can signal an official, production-ready version, which helps in automated deployments and managing production versions versus development tags.</p>

#### 5. Versioned History and Rollback:
<p>Releases provide a clear, versioned history of your software, making it easy to identify and roll back to a specific stable version if needed.
They offer a structured way to track progress and document your software’s development over time.</p>

#### Releases can be used as trigger point for CI/CD workflow trigger point which make sure the stablity. 

# How To Release

#### 1.Navigate to Your Repository: Open your GitHub repository.

#### 2.Access the Tags and Releases Section: Select the Tags section. You’ll see options for Releases and Tags.

#### 3.Initiate a New Release: Click on the Releases tab, then select Create a new release.

#### 4.Select the Tag to Release: In the release creation form, choose the tag you want to release from the dropdown. Optionally, add release notes or descriptions for context.

#### 5.Publish the Release: Click Publish release to finalize. Your tag will now be promoted to an official release, indicating it as a stable version.



# How to create tags and update production and staging once releases are created.
```bash
1. git checkout dev or main (which have you latest tested code)
2. git tag -a v1.0.0 -m "Stable-Thu-31-Oct-2024-2:32Pm"
2a. git push origin <speific tage version>
Now you have get a latest snapshot that is tag v1.0.0 which is now released as well

Now in which branch you need to push or uptde with for instance **production**

3 git checkout production
4 git reset --hard v1.0.0

As we know git reset --hard do following things. 1 It will unstage all the commits from staging and 2 It will undo/delete all the changes made to local. How it worked here
   1 The command simply aligns your current branch (production in this case) to the exact commit that v1.0.0 points to.
   2 The production branch now reflects v1.0.0. All previous commits or changes in production beyond v1.0.0 are cleared, and it matches the exact snapshot of v1.0.0.

5 git push --force origin production
```

# How Rollbacks works

```bash
1. Suppose your **production** is now on **v1.0.1**. How you want to rollback to **v1.0.0**.
2. git checkout production
3. git reset --hard v1.0.0
4 git push --force origin production

how it exactly works with **conflicts** as downgrade the code may cause **conflicts**.

    1. git reset --hard v1.0.0 moves the production branch pointer back to the commit tagged as v1.0.0. Any commits made after v1.0.0 (such as those in v1.0.1) are removed from production.

    2. This means the production branch will no longer contain the changes from v1.0.1, effectively rolling back to v1.0.0.

    3. The v1.0.1 tag itself will not be affected. It still points to its original commit, even though production no longer reflects v1.0.1. Tags in Git are independent pointers, so v1.0.1 still exists in the repository history.

    4 git reset --hard does not create a new tag or alter existing tags; it only changes the branch’s commit history.

    Avoiding Conflicts in a Downgrade:

    Force Push: To apply this change on the remote repository (e.g., GitHub), you’ll need to force push the production branch to overwrite its current state with the rolled-back version:
      1. git push --force origin production
      2. This force push ensures that production on the remote matches the exact state of v1.0.0 without any merge conflicts, as it overwrites the remote history.

git reset --hard <to specific version>
it first delete the changes before and after the version vice versa and then exactly match the version you want to rest to

then git push --force origin production his **force ** will make sure that i will forcefully point to the version we wanted.

Since git reset --hard v1.0.0 completely resets production to the state of v1.0.0, it effectively removes any changes after that commit. This rollback means there won’t be conflicts because there’s no merging involved—production is simply reset to the earlier stable snapshot.
```
