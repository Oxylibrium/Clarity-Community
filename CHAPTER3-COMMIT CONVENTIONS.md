# Chapter 3 - Commit Message Conventions

These rules are adopted from [the AngularJS commit conventions](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits).

* [Subject line](#subject-line)
    * [Allowed `<type>`](#allowed-type)
    * [Allowed `<scope>`](#allowed-scope)
    * [`<subject>` text](#subject-text)
* [Message body](#message-body)
* [Message footer](#message-footer)
    * [Breaking changes](#breaking-changes)
    * [Referencing issues](#referencing-issues)
* [Examples](#examples)


The format of a commit message should be as follows:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer> (optional)
```

Any line of the commit message should not exceed 100 characters. This allows for the message to be easier to read.

## Subject line        
The subject line should contain a succinct description of the change with context and should not exceed 50 characters.

### Allowed `<type>`
- build: changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
- ci: changes to CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
- docs: documentation only changes
- feat: a new feature
- fix: a bug fix
- perf: a code change that improves performance
- refactor: a code change that affects the underlying logic, but neither fixes a bug nor adds a feature
- style: a code change that affects conformance to a style guide, but does not affect functionality
- test: adding missing tests or correcting existing tests

### Allowed `<scope>`
Scope specifies the module of the code changed by the commit, if applicable.

### `<subject>` text
* Use imperative, present tense: “change” not “changed” nor “changes”
* Do not capitalize the first letter
* No period (.) at the end

## Message body
* Use imperative, present tense: “change” not “changed” nor “changes”
* Include the motivation for the change and the contrasts with previous behavior

## Message footer

A message footer should include mentions of any breaking changes and issues closed by the commit, if any.
If none, it should be left blank.

### Breaking changes

All breaking changes should be mentioned in the footer starting with the words `BREAKING CHANGE:`, with a description of the change, justification and migration notes.

### Referencing issues

Closed issues should be listed on a separate line in the footer prefixed with the "Closes" keyword. For instance:

```
Closes #24, #12, #24, #92
```

## Examples

```
feat($browser): onUrlChange event

Add new event to $browser:
- forward popstate event if available
- forward hashchange event if popstate not available
- poll when neither popstate nor hashchange available

BREAKING CHANGE: Breaks $browser.onHashChange, which was removed.
To migrate code, replace onHashChange with onUrlChange.

Closes #143
```

```
feat(modules): Add kitsu.io API implementation

Add the `kitsu` command to look up anime and manga on kitsu.io.

Closes #43
```

```
style(libs): fix indentation
```

```
docs(guide): update fixed docs from Google Docs

Fix a few typos:
- indentation
- batchLogbatchLog -> batchLog
- start periodic checking
- missing brace
```

```
feat($compile): simplify isolate scope bindings

Change the isolate scope binding options to:
  - @attr - attribute binding (including interpolation)
  - =model - by-directional model binding
  - &expr - expression execution binding

BREAKING CHANGE: isolate scope bindings definition has changed and
the inject option for the directive controller injection was removed.

To migrate code, follow the example below:

Before:

scope: {
  myAttr: 'attribute',
  myBind: 'bind',
  myExpression: 'expression',
  myEval: 'evaluate',
  myAccessor: 'accessor'
}

After:

scope: {
  myAttr: '@',
  myBind: '@',
  myExpression: '&',
  // myEval - usually not useful, but in cases where the expression is assignable, you can use '='
  myAccessor: '=' // in directive's template change myAccessor() to myAccessor
}

The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```
