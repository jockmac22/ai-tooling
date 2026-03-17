---
name: spec-new
description: Generates a new spec documents in the current project.  Spec documents guide Claude in how to build out new code. Triggered when a user asks to generate a new spec document, or when a user asks to add a new feature.
---

# New Specification/Feature

## Pre-requisites

### 1. The current project must have specs initialized.

If the current project doesn't have the directories established by the `spec-init` script, then this skill must stop and notify the user that they must run the `spec-init` skill first.

### 2. The current project must have a clean git history

If the current project must currently be in the master branch.

It must not have open git commits, unresolved conflicts or uncommitted files. 

If git these requirements, then this skill must stop and notify the user to clean up their git history before continuing.  Recommend what they might need to do to clean up the history.

## Instructions

### 1. Check for pre-requisites

Make sure that the current project meets the pre-requisites established for this skill. If it doesn't react accordingly.

### 2. Prompt the user for necessary information

#### Ask for a Spec Title 

Prompt the user to provide a title for the spec.  

Stop an wait for them to respond, then label the response as `[Title]` and continue to the next prompt.

#### Ask for a Spec Purpose

Prompt the user to provide a purpose for the spec.  The purpose should be about 1 or 2 paragraphs long, and describe abstractly what will be accomplished.

Stop and wait for them to respond, then label the response `[Purpose]` and continue to the next prompt.

#### Ask for Specific Requirements

Ask the user to define specific requirements as a list where each requirement exists on its own line, and talks specifically about what the spec must accomplish.  The list can be any length it needs to be to achieve the goal.

Stop and wait for them to respond, then label the response `[Requirements]` and continue.

### 3. Rename the current conversation.

Using the `/rename` skill to change the title of the current conversation to match the title of the spec provided in the previous step.

### 4. Generate a template labels and values

Create a short, machine friendly title that is less than 80 characters, all lowercase and kebab-case.  Label this value `[MachineTitle]`. 

Create an ISO date time string using the current time and this template: `YYYYMMDDHHmmSS`.  This value should be numeric only, no month names or abbreviations. Label this value `[ISO-Date-Time]`.

Create a new git branch name using this template: `spec_[ISO-Date-Time]_[MachineTitle]`. Replace the template values in brackets with the labels we've previously defined.  Label this value `[GitBranchName]`

Create a new spec file name using this template: `.claude/specs/[ISO-Date-Time]_spec_[MachineTitle].md`. Replace the template values in brackets with the labels we've previously defined.  Label this value `[SpecFile]`

### 5. Confirm the spec configuration

Show the user the current `[Title]`, `[Purpose]`, `[GitBranchName]` and `[SpecFile]` values and ask them to confirm that this information is correct and that they want to continue.

If they do not confirm, then stop executing this skill.

### 6. Generate spec content

Generate the spec document content using the `spec_template.md` template.  Replace the template values in brackets with the labeled values we've generated previously in this skill.

Confirm the spec content with the user.

### 7. Create Branch and Write Content

Checkout a new git branch using the `[GitBranchName]` value.

Write the spec content to a file name with the `[SpecFile]` value.

### 8. Ask if we should generate the spec

Ask the user if they want to generate the detailed specifications, if they say yes, then run the `spec-generate` skill.