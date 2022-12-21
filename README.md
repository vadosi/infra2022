# ДЗ 1

Theory [2]
As usual, we will start with a few theoretical questions:

[0.5] What is Docker, and how it differs from dependencies management systems? From virtual machines?

[0.5] What are the advantages and disadvantages of using containers over other approaches?

[0.5] Explain how Docker works: what are Dockerfiles, how are containers created, and how are they run and destroyed?

[0.25] Name and describe at least one Docker competitor (i.e., a tool based on the same containerization technology).

[0.25] What is conda? How it differs from apt, yarn, and others?



Anaconda:

[1] Install conda, create a new virtual environment, and install all necessary packages.

[0.75] You won't be able to install some tools - that's fine. List their names, and explain what should be done to make them conda-friendly (conda-forge channel, bioconda channel).

[0.25] Export the environment (example) to the file and verify that it can be rebuilt from the file without problems.


Docker:

[3] Create a Dockerfile for a container with all required dependencies. Conda usage is not allowed, don't forget about comments; test that all tools are accessible and work inside the container. Hints:
If needed, grant rights to execute downloaded/compiled binaries using chmod (chmod a+x BINARY_NAME)
Move all executables to $PATH folders (e.g./usr/local/bin) to make them accessible without specifying the full path.
Typical command to run a container interactively (-it) and delete on exit(--rm): docker run --rm -it name:tag

[1] Use hadolint and remove as many reported warnings as possible.

[0.5] Add relevant labels, e.g. maintainer, version, etc. (hint)
