
## Modify Snapshot Files

The `create-pullreq.yml` file in this folder has an extra step that overwrites specific fields in a snapshot file when a pull request is created. This can be useful when we have differences between environments in specific configuration keys.

The workflow file as it is now demonstrates overriding the cookie settings in `project.json` to ensure they're not changed by whatever is exported from the staging project. As another example, we might want to have an HTTP connector that uses a different base URL when deployed to staging or production.

You can customize the workflow by changing or removing the calls to `modifyFile` with whatever you need. You can then copy the `create-pullreq.yml` file over to the `.github/workflows` folder to overwrite the existing file there.
