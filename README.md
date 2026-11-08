





# Setup notes

There's a misalignment between the handling of project directory in codex (based on the filesystem) and in the ChatGPT app (using a library system not accessible as a filesystem AFAIK). So for now, we'll use the specific instructions.

* For codex, add in the AGENT.md:

```Any rerefence to `project-directory` should be resolved as the project's current directory.```

* For ChatGPT, add to the project setup:

```Any reference to `project-directory` refers to `<library>/<project-name>`.```

