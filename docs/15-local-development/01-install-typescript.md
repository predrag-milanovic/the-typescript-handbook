Install TypeScript
===================

In this chapter we will move from running TypeScript in the browser to running it directly on your machine.

This guide assumes that you already have [**Node.js** and **npm**](https://nodejs.org/en/) installed. If you do not, install them first from the official Node.js website or your system package manager.

Global installation
-------------------

To install the TypeScript compiler globally, run the following command:

```bash
npm install -g typescript
```

After this completes, you should be able to use the TypeScript compiler via the `tsc` command.

Verifying the installation
--------------------------

Check that `tsc` is available and see which version you have installed:

```bash
tsc -v
```

You should see a version string such as:

```text
Version 5.x.x
```

If you do not see a valid version, either the installation failed or the location where `npm` installs global binaries is not in your `PATH`.

On many systems, `npm` installs global binaries into a directory such as:

- macOS (with nvm): `/Users/<you>/.nvm/versions/node/<node-version>/bin`
- Linux (with nvm): `/home/<you>/.nvm/versions/node/<node-version>/bin`

Make sure that the appropriate directory is included in your `PATH` environment variable. Once `tsc` is available on your `PATH`, you are ready to compile TypeScript from the command line.


