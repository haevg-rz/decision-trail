# 2. Adopting the-way in other project repos

- Status: promoted
- Promoted to: [ADR-0008](../decisions/0008-adopt-the-way-via-a-copied-starter-skeleton.md)

## Idea

Real projects should **not** live in this repository. Each project should have
its own repo, carrying its own `the-way` artifacts and structure (`ideas/`,
`decisions/`, `plans/`), and its own ADR log starting at 0001 — without
inheriting this repo's construction ADRs.

This repo should therefore play the role of the **standard / method**, and there
should be a clear, cheap, borrowed way to start a new project repo that *adopts*
the-way.

Open questions this raises (to be settled by the promoted ADR):

- How is the skeleton delivered — a GitHub template repository, a `starter/`
  folder copied by hand, or a scaffolding tool (copier/cookiecutter)?
- Does an adopting project **copy** the method text (self-contained) or
  **reference** this repo (single source, but a runtime dependency)?
- How does a project cite *which version* of the-way it adopted, given the method
  is "settled (not frozen)" and will evolve?
