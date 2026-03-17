---
name: spec-generate
description: Generates features and acceptance criteria for the currently selected spec file. Triggers when a user indicates that they want to generate features and/or acceptance criteria from the current spec.
---

# Generate Specification

## Pre-requisites

### 1. The current project must have specs initialized.

If the current project doesn't have the directories established by the `spec-init` script, then this skill must stop and notify the user that they must run the `spec-init` skill first.

### 2. A Spec File Must be Selected

If the currently selected file is not a spec file in the /.claude/specs folder then this skill must stop and notify the user to select a specf file to run this kill against.


## Instructions

### 1. Check for pre-requisites

Make sure that the current project meets the pre-requisites established for this skill. If it doesn't react accordingly.

### 2. Generate a List of Features from the Spec File

Read the `Title`, `Purpose` and `Requirements` sections and extrapolate a set of features.  Document the features in the `Features` section of the spec file.

If there is ambiguity about a feature or how it should be implemented, stop and ask the user to clarify.  Offer a few suggestions, but also let them define their own response as well.

### 3. Generate a set of Acceptance Criteria from Features

Given the features generate in Step 2, generate a set of Acceptance Criteria to prove that the features were built out properly.

### 4. Generate a set of Tests from the Acceptance Criteria

Generate a series of tests and validations that can be performed that can prove that the work that was done is functioning properly. 

### 5. Write the data to the Spec File.

Update the Spec file content with the Features, Acceptance Criteria and Tests that were generated previously. Confirm the changes with the user. 

If the does not confirm the changes, stop the skill immediately.

Otherwise write the changes to the spec file.

