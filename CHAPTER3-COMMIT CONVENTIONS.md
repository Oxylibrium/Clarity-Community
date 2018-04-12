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
<footer>
```

Any line of the commit message should not exceed 100 characters. This allows the message to be easier to read.

## Subject line        
The subject line should contain a succinct description of the change with context and should not exceed 50 characters.

### Allowed `<type>`
- build: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
- ci: Changes to CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
- docs: Documentation only changes
- feat: A new feature
- fix: A bug fix
- perf: A code change that improves performance
- refactor: A code change that neither fixes a bug nor adds a feature
- style: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- test: Adding missing tests or correcting existing tests

### Allowed `<scope>`
Scope specifies the module of the code changed by the commit, if applicable.

### `<subject>` text
* use imperative, present tense: “change” not “changed” nor “changes”
* don't capitalize first letter
* no single dot (.) at the end

## Message body
* use imperative, present tense: “change” not “changed” nor “changes”
* include motivation for the change and contrasts with previous behavior

## Message footer

### Breaking changes

All breaking changes should be mentioned in footer with a description of the change, justification and migration notes.

### Referencing issues

Closed bugs should be listed on a separate line in the footer prefixed with the "Closes" keyword. For instance:

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

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
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

To migrate the code, follow the example below:

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
