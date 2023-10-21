# Development CLI

This project contains a simple Devcontainers configuration that allows usage of development tools on any machine without
requiring dependencies (other than Docker, Git, and VSCode) to be installed on the host itself. Because many of these
tools desire the latest versions of common tooling like pip, npm, cargo, or go, containerizing these one-off operations
is an easy and repeatable way to make sure that I can use these functions whenever necessary.

This should not be used for dependencies that are required _within_ a project's development cycle; those should always
be installed directly within the Devcontainer associated with the project.
