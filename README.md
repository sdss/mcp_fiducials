# mcp_fiducial

APO Sloan 2.5m telescope fiducial tables

## Updating fiducial tables

To update the fiducial tables first add the new tables to this repository, replacing the old ones. Then commit, tag, and push the changes. For example, if tagging `v1_150` one would do:

```bash
git add .
git commit -m "Update fiducial tables"
git tag -a v1_150 -m "mcp_fiducials v1_150"
git push
git push --tags
```

Then ssh to the MCP computer and navigate to `$HOME/sdss/mcp_fiducials`. Clone the repository with the name of the new tag. Again, for `v1_150`:

```bash
git clone -b v1_150 https://github.com/sdss/mcp_fiducials v1_150
rm -rf v1_150/.git
```

We remove the `.git` directory to make sure the tagged checkout cannot be modified.

Now we create a new module file for this version in `$HOME/sdss/modulefiles/mcp_fiducials`. You can copy a previous version and edit it, but the text for `v1_150` would look like:

```tcl
#%Module1.0

proc ModulesHelp { } {
    global product version
    puts stderr "This module adds $product/$version to your environment."

}

set product mcp_fiducials
set version v1_150

set PRODUCT_DIR /home/mcp/sdss/$product/$version

setenv [string toupper $product]_DIR $PRODUCT_DIR
```

Finally, edit the `.version` file to look like:

```tcl
#%Module1.0
set ModulesVersion "v1_150"
```

If you run `module avail mcp_fiducials` you should see the new version listed and as the default.

You may also want to update the `$HOME/sdss/mcp_fiducials/main` checkout by pulling the latest changes from this repository (`git pull`).
