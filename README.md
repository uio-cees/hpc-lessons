#Using the CEES HPC resources

See <https://uio-cees.github.io/hpc-lessons>.

**Work in progress**  
Once we have some contents in place, we welcome pull requests.

Many thanks to [Software Carpentry](software-carpentry.org) for the template to this lesson material:

> Please see [https://github.com/swcarpentry/lesson-example][swc-lesson-example]
> for instructions on formatting, building, and submitting lessons,
> or run `make` in this directory for a list of helpful commands.


### LICENSE

This instructional material is derived from the Software Carpentry lesson template and made available under the same license. See the [LICENSE.md](LICENSE.md) file in this repository.

### Contributing

If you don't have commit rights, fork the repository and submit a pull request.

If you are a member of [this uio-cees team on github](https://github.com/orgs/uio-cees/teams/cees-hpc-core), you can use the following workflow.

If you haven't done so already, clone the repository to your local PC:

```
git clone https://github.com/uio-cees/hpc-lessons.git
cd hpc-lessons
```

If you have already cloned the repo, pull in the latest changes from github:

```
git pull
```

Create a new branch for your work:

```
git checkout -b name_of_branch
```

Note that this also switches you to your new branch.

Now make the changes you want, and commit them. To preview the webpages, run these commands, which should finish without warnings:

```
make check
make preview
```

Now you can check the html pages by opening them in your browser. Make sure to do this before you submit the pull request!

Once you're ready to submit a pull request, push your branch up to github:

```
git push
```

Note that the first time you do this, you'll get the following message:

```
fatal: The current branch name_of_branch has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin name_of_branch
```

Then perform the command git suggests.

On [github](https://github.com/uio-cees/hpc-lessons), you'll see a message saying 'Your recently pushed branches' with a button to *'Compare and & pull request'*. Click that button and follow the instructions for submitting the changes as a pull request.

What if you started working but forgot to make a new branch?

* if you have not yet committed anything, see [this stack overflow answer](http://stackoverflow.com/questions/1394797/move-existing-uncommited-work-to-a-new-branch-in-git)
* if you already made commits, see [this stack overflow answer](http://stackoverflow.com/questions/1628563/move-the-most-recent-commits-to-a-new-branch-with-git)


###Editing tips
See the FAQ at <https://github.com/swcarpentry/lesson-example/blob/gh-pages/FAQ.md>
