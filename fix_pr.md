This is a demo of using **usethis** functions to modify a pull request. Without these functions, the process is *much more complicated and error prone*. Note that the preferred workflow is to ask the person who submitted the changes to make the modifications that you request. You would do this yourself, as described below, in a situation in which the contributor is not responding, or does not have the skills to make the changes you need. It will only work (need to test this) if the contributor has checked the "Allow edits from maintainers." box in their pull request.

First install the dev version of `usethis`:

```{r}
devtools::install_github("r-lib/usethis")
```

```
Skipping install of 'usethis' from a github remote, the SHA1 (c5f9b3e8) has not changed since last install.
  Use `force = TRUE` to force installation
```  

Open the local project for the repo and pull changes, either by clicking on the PULL button in RStudio or as follows:

```{r}
git2r::pull()
```

```
Already up-to-date
```

Look for the pull request number in the [list of pull requests](https://github.com/jtr13/springishere/pulls). We see that the [pull request we want](https://github.com/jtr13/springishere/pull/6) is number 6.

Bring the pull request into your workspace:

```{r}
usethis::pr_fetch(6)
```

```
✔ Checking out PR 'jtr13/springishere/#6' (@nbrgraphs): 'convert to line graph'
✔ Switching to branch 'nbrgraphs-patch-2'
```


You are now effectively working as the person who submitted the pull request.  Make changes to files as desired. In this case, I added `col = "red"` to the `pressure` plot in `pressure.Rmd` since `@nbrgraphs` did not respond to my request to do so.

Commit the changes, either by clicked the staged box next to `pressure.Rmd` and then the COMMIT button, or as follows:

```{r}
git2r::add(path = "pressure.Rmd")
git2r::commit(message = "change line color")
```

Push the commit to the pull request branch:

```{r}
usethis::pr_push()
```

Clean up:

```{r}
usethis::pr_finish()
```



