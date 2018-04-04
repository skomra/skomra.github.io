This section describes how to do a new input-wacom release.

0.   Merge master into all current branches, and then merge those branches into master. Use the '--no-ff' option with 'git merge' to force a commit message.
0.    Change configure.ac to reflect the new version number and commit: <code>git commit -sm "input-wacom VERSION" configure.ac</code>. You must not have uncommitted changes when releasing a new version.
0.   Tag the module: <code>git tag -m "input-wacom VERSION" -s input-wacom-VERSION</code>. You will use your PGP key for this step. (This step is necessary to get the modinfo version (eg. v2.00-0.37.0.11.gd0b76d0) correct.)
0.    Run <code>make dist</code>. Verify the name of the tarball (<code>input-wacom-VERSION.tar.bz2</code>). If this is a clean clone of the repository, you will need to first run <code>autogen.sh</code> to generate the Makefile. It is also possible you may need to run <code>make distclean</code> if something goes wrong with <code>make dist</code>.
0.    Build, install, and load the driver from the tarball.
0.    Verify the version number of the loaded driver with <code>modinfo wacom | grep version</code>.
0.    Push to the remote: <code>git push origin master</code>.
0.    By default, the git push command doesn’t transfer tags to remote servers. Push the tag to the remote: <code>git push origin input-wacom-VERSION</code>.
0. Make sure you have the dependencies for the release script: <code>jq</code> and <code>curl</code>.
0. Run the release script: <code>release.sh</code> with the correct arguments. This script will push the tag and upload the tarball to the remote. example: 
<code> ./release.sh --github skomra:de0e4dc3efbf2d008053027708227b365b7f80bf --sourceforge skomra@ . </code> See below for an explanation of the parameters to the script.
0.    Sign off the generated .announce email and add a short announcement summarizing the new features in this version. Check that the tarball url in the .announce email is a valid link. Send it to the linuxwacom-announce list using <code>git send-email</code>.
0.    Close all Sourceforge and Github bugs that were fixed in this release and which are fixed in an upstream Linux release by setting the status to "closed-fixed" and posting the following message: "Fix available in Linux <version> and input-wacom <version>" 

#### Release script Parameters ####
| Parameter | Value | Exaplanation |
| ---------- | ---------- | ---- |
| <code>--sourceforge</code> | `<Sourceforge username>`@ | for the Sourceforge release |
| <code>--github</code> |  `<your Github username>` | If you do not use 2 Factor Authentication (2FA), you will be prompted for your password. If you use 2FA you need to append ":KEY" to your username where ":KEY" is an authentication token you can generate here: https://github.com/settings/tokens |
| | 'dot' (<code>.</code>) | takes the place of the project name |