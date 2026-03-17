---
name: spec-changelog
description: Generates a changelog file from the current conversation and the changes in the current project. Triggered when the user asks to generate a changelog from the spec.
---

# Generate Specficiation Changelog

## Pre-requisites

### 1. The current project must have specs initialized.

If the current project doesn't have the directories established by the `spec-init` script, then this skill must stop and notify the user that they must run the `spec-init` skill first.

### 2. A Spec File Must be Selected

If the currently selected file is not a spec file in the /.claude/specs folder then this skill must stop and notify the user to select a specf file to run this kill against.

### 3. Confirm Spec Alignment

Examine the changes in the project and compare them against the work that the specification and the plan outline. If they are not similar, stop and let the user know that there are significant differences between the Spec/Plan and Project Changes. 

Ask them to confirm that they want to continue generating the changelog.

## Instructions

### 1. Check for pre-requisites

Make sure that the current project meets the pre-requisites established for this skill. If it doesn't react accordingly.

### 3. Generate a template labels and values

Exctract the machine friendly title from the spec file.  Label this value `[MachineTitle]`. 

Create an ISO date time string using the current time and this template: `YYYYMMDDHHmmSS`.  This value should be numeric only, no month names or abbreviations. Label this value `[ISO-Date-Time]`.

Create a new changelog file name using this template: `.claude/changelog[ISO-Date-Time]_changelog_[MachineTitle].md`. Replace the template values in brackets with the labels we've previously defined.  Label this value `[ChangelogFile]`


### 4. Generate a Title and Summary
Generate a brief title from the Spec File. Label this value `[Title]`

Generate a summary of work done from the spec file.  Label this value `[SpecSummary]`


### 5. Generate a Bug List

Examine the conversation and the spec file and identify any bug fixes that were executed.  Summarize them as a bulleted list of items, with 1-2 sentence descriptions. If links to a specific bug reports are available, include them at the beginning of the list items.  Label this list `[BugList]`

### 6. Generate the Changelog

Using the changes in the project, and the current conversation, generate a numerically bulleted list of changes, where each bullet is a 1 sentence summary of the change.  Label this list `[ChangeList]`

Using the same changes in the project, and the current conversation, generate a more detailed change log for each bullet in the list above. Generate a new sub-heading for entry and number the heading to match the number in the list above.  The content below the heading should be details about the changes that were made for that item.

### 7. Parse the template

Use the `changelog-template.md` template file, in the skill folder, and replace the labels in the template with the matching values generated in the previous steps.
 
### 8. Confirm and write

Confirm the changes with the user.  If they agree to the changes, write them to a changelog file named for the label `[ChangelogFile]`.  Make sure this file is in the `/.claude/changelog` path as determined above.

