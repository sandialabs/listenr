listenr Workflow
================
<br> Updated on March 21, 2024

### Branch types

There are three “types” of branches in `listenr`:

- `master`: This is where only “clean” and “solidified” code goes to
  live. When code is moved to `master`, the version number also updates.
- `dev`: This is the most up to date “working” version of `listenr`.
  Code goes to live in `dev` when it’s working but not quite ready for
  `master`.
- other: Any other branch can be created as a sandbox for trying out
  ideas and updating `listenr`. It’s good to generate these based on
  `dev` and when ready - merge into `dev`.

### Steps for updating `listenr`

Consider following these steps to help avoid merge conflicts.

**Initial Steps**

1.  Create a new branch based on the `dev` branch.
2.  Update code in the new branch.
3.  When feeling good about changes, merge the new branch to `dev`.

**Merging to `master`**

Repeat steps 1-3 until a “significant” change has been made to `listenr`
and it feels like time to merge to `master`. Then…

4.  Start by running a “check” on the package using `devtools`:
    - This is easiest done from within RStudio.
    - When you have the package open in RStudio, change to the `dev`
      branch.
    - Then either run `devtools::check(document = FALSE)` in the
      console, or hit the “check” button under the “build” tab.
    - Address the errors, warnings, and notes that are returned. (Notes
      are less important but nice to address, if possible.)
    - Keep running `devtools::check` until all issues are gone.
5.  Update the version number in the DESCRIPTION file.
    - There will (probably) be a 9 after the third decimal (i.e.,
      x.x.x.9), which indicates that this is a development version.
    - Delete the ‘.9’, so you now have x.x.x.
    - Now update the version. The decimal place that gets updated is
      based on how major the update it. For example, the first one is a
      major overhaul of the package, the middle is a big update but
      still following the same “conventions” of the previous version,
      and the third decimal is for small updates.
6.  Build the package one more time (now that the version number has
    been updated to make sure all is well).
7.  Merge `dev` into `master`.
8.  Create a “release” of the package within GitLab.
    - Go to “Deploy” on the side panel, and click “Releases”.
    - Click “New release”, and fill in the information.
    - I’ve been tagging the releases using their version number (i.e.,
      “vx.x.x”) and naming the releasing using a fun word related to
      sound (e.g., reverb), but it’s not a requirement.
    - Under “Release notes”, it’s helpful to add a description of what
      changed in this version of the package.
    - I haven’t been putting any “Milestones” or “Release assets”.
    - Click “Create release”!
9.  Bonus points: Lastly, go to the DESCRIPTION file in the `dev` branch
    and add a “.9” behind the version number in the `dev` branch. If you
    deleted `dev` when merging `dev` into `master`, no worries! Create a
    new branch called `dev` based on `master`, and update the version
    number.

### Working with older versions of listenr

Versions of `listenr` that are at a good state will be “released” and
“tagged” on GitLab. These releases can be found
[here](https://gitlab-ex.sandia.gov/cldera/cldera-obs/listenr/-/releases).

There are various ways to go about making use of the different versions
of `listenr`. One possible option is described below.

1.  Download the `Source code (tar.gz)` file under the release of
    interest.

2.  Save this file in nice location on your computer.

3.  When you want to make use of this version of the package, start by
    running the following code where you need to replace `path-to-file`
    based on where the file is stored and the version numbers in the
    file name:

        install.packages("~/path-to-file/listenr-vX.X.X.tar.gz", repos = NULL, type="source")

4.  Then you can access this version of `listenr` by running the
    command:

        library(listenr)

Note: If you want to switch to a different version of `listenr`, you may
need to restart R Studio or your R session. I’m still trying to
understand if there is a better way to do this. (Let me know if you know
of one!)

See [this
notebook](https://gitlab-ex.sandia.gov/cldera/cldera-obs/sandbox-goode/-/blob/master/notebooks/17-era5-pfi-with-esn-listenr.Rmd)
for an example where an older version of `listenr` is used.