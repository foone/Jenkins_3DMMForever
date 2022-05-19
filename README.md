# 3DMMForever Jenkins project

This is a quick Jenkinsfile to enable automatically building [3DMMForever](https://github.com/foone/3DMMForever), the modernized version of the [3D Movie Maker source code released by Microsoft](https://github.com/microsoft/Microsoft-3D-Movie-Maker)


# Usage instructions

Set up a pipeline project that gets the pipeline script from SCM, point it at this repo (or a fork), using the default Jenkinsfile. 

It needs a node with the label "msvc20" which has Microsoft Visual C++ 2.1 installed (or at least the MSVC20 directory from the CD copied into it), and has an environment variable MSVCNT_ROOT defined on the node, pointing at the install of MSVC 2.1 (Preferably without spaces in the path, I used C:\MSVC20).

The system should also have 7zip and git installed and in the path.

Just build and it should work. It checks out the main repo inside the script, and sets other variables based on that, then builds.

# Plugins used

* [Workspace Cleanup](https://plugins.jenkins.io/ws-cleanup/)
* [git](https://plugins.jenkins.io/git/) (is this installed by default? I'm not sure)

