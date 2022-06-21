- Start Date: 03-06-2022
- Status: Proposed

# Supporting Apps on Renku

## Summary

Renku projects can currently be homes for sessions, datasets, and workflows. This proposal introduces a new kind of session, the _App_ session (in contrast to the existing _Dev_ sessions), so projects can host interactive applications associated with the work and contents of the project.

## Motivation

One common outcome of a data-science project is an interactive application, such as a dashboard, that supports flexibly viewing and analyzing data. The infrastructure necessary for this is already available with sessions, but, since sessions currently implicitly assume a more code-development-oriented use case, there are many UX improvements that could be realized by directly supporting applications as project outcomes.

### Status Quo

To understand the problems, let us consider how a project can offer an app today. One way would be as follows:

- Start a session and install streamlit into the session
- Develop the app
- Install jupyter server proxy, configure it for streamlit, and and modify the Dockerfile to use it
- Modify the renku.ini to set the streamlit end point as the default
- Update the README.md with a description of your app and provide a badge to start it.

(For an example, see https://renkulab.io/projects/renku-stories/alphapept-gui-streamlit)

Looking at this, there are several problems with the status quo that we can identify:

- By default, the developer will also end up in streamlit when they start a session. Extra work is necessary on the part of the developer to make their own experience using Renku smooth.
- What happens if we want to offer two apps? That becomes cumbersome.
- The app session still contains the dev tools (e.g., JupyterLab) and a casual user can end up in the dev environment by accident.
- An app should not have autosave branches because any changes made are intended to be transient
- How can I search for projects that have apps? The fact that there is an app in this project is invisible to the search.

By supporting apps as a first-class citizens, we can address these problems and more, improving the UX for both developers and users of apps within Renku.

## Design Detail

The proposal to address this gap is to introduce a new project-level entity -- the **App** -- with metadata and operations specifically for those use cases.

The app metadata needs to let users search for apps and understand at a high level what an app does. It also needs to let developers describe the resource requirements for running the app and how the infrastructure should start the app.

### Metadata

An app needs the following metadata:

| Field        | Purpose                                                              |
|--------------|----------------------------------------------------------------------|
| Name*        | The name of the app                                                  |
| Description* | A short description explaining what the app does                     |
| Dockerfile*  | A path to a dockerfile for the container that runs the app           |
| Resources*   | Information matching the _renku "interactive"_ section of renku.ini  |
| Image        | (optional) A path to an image that represents the app                |
| Readme       | (optional) A path to a markdown file with more details about the app |
| Tags         | (optional) Keywords that categorize the app                          |


The metadata for apps should be indexed by the knowledge graph (KG), just as is the case for _datasets_ and _workflows_.

### Wireframes

**TODO**


## Drawbacks

There are no drawbacks to supporting apps, since Renku users are already creating solutions themselves. By making apps first-class citizens, we can provide better support activities that users are already doing in an ad-hoc way.

**TODO**
> There are tradeoffs to choosing any path, please attempt to identify them here.

## Rationale and Alternatives

**TODO**

> Why is this design the best in the space of possible designs?

> What other designs have been considered and what is the rationale for not choosing them?

> What is the impact of not doing this?

## Unresolved questions

**TODO**

> What parts of the design do you expect to resolve through the RFC process before this gets merged?

> What parts of the design do you expect to resolve through the implementation of this feature before stabilisation?

> What related issues do you consider out of scope for this RFC that could be addressed in the future independently of the solution that comes out of this RFC?
