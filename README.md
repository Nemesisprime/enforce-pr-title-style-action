# Enforce Pull Request Title Style Action

This action analyses the titles of Pull Requests to ensure they start with a Jira Issue Key.  Issue Keys are a combination of a Project Key, a hyphen, and a number designating which issue it is.  In general, Project Keys are two capital letters but Jira does allow for [custom Project Keys](https://confluence.atlassian.com/adminjiraserver/changing-the-project-key-format-938847081.html) and this issue attempts to abide by the custom format. If you want to be specific to your project, use the `projectKey` input for the action.

For example, if your project key were `AB` then the following would be allowed

```
AB-1  Initialize Project
```

Colons are also acceptable after the project key and ticket number: 

```
AB-1:  Initialize Project
```

However, the following examples would not be allowed:

```
aB-1 Initialize Project
```

```
ab-1 Initialize Project
```

```
Ab 1 Initialize Project
```

Valid Pull Request titles must also include a short description after the Issue Key. Therefore the following is not valid. 

```
AB-1
```

By default, this action will allow any valid Issue Key so long as it *could* be valid; however, you may specify an Issue Key to exclude checking with `ciExclusion`. For example, the default exclusion value, "CI", will make the following valid (with or without colon): 

```
AB-CI: CI Automation
```

And finally, you may opt out of project key and issue key checks all together by starting a pull request title with the `exclusionMarker` (which is "!" by default):

```
! Any Title will be valid.
```

## Inputs

### `projectKey`

A specific Project Key to always check for. 

### `ciExclusion`

A specific string suffix that may be affixed to the projectKey instead of an Issue Key. `CI` by default.

### `exclusionMarker`

A specific string prefix that will automatically pass the title, regardless of projectKey and Issue Key. `!` by default.

## Example Usage

```
- name: Enforce Jira Issue Key in Pull Request Title
  uses: nemesisprime/enforce-pr-title-style-action@v1.1
```

## Example Usage with a specific Project Key

```
- name: Enforce Jira Issue Key in Pull Request Title
  uses: nemesisprime/enforce-pr-title-style-action@v1.1
  with:
    projectKey: AB
```

## Example Usage with a specific Project Key and custom exclusions

```
- name: Enforce Jira Issue Key in Pull Request Title
  uses: nemesisprime/enforce-pr-title-style-action@v1.1
  with:
    projectKey: AB
    exclusionMarker: "~"
    ciExclusion: "NaN"
```