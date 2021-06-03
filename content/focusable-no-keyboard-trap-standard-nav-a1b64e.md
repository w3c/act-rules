---
title: "Focusable element has no keyboard trap via standard navigation"
permalink: /standards-guidelines/act/rules/focusable-no-keyboard-trap-standard-nav-a1b64e/
ref: /standards-guidelines/act/rules/focusable-no-keyboard-trap-standard-nav-a1b64e/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/focusable-no-keyboard-trap-standard-nav-a1b64e.md
# footer: > # Text in footer in HTML
#   <p> This is the text in the footer </p>
---

{% include_relative _proposed-banner.html %}

Rule Type:
:   atomic

Rule ID:
:   a1b64e

Last Modified:
:   June 3, 2021

Input Aspects:
:   [DOM Tree](https://www.w3.org/TR/act-rules-aspects/#input-aspects-dom)
:   [CSS Styling](https://www.w3.org/TR/act-rules-aspects/#input-aspects-css)

## Description

This rule checks if it is possible to use standard keyboard navigation to navigate through all content on a web page without becoming trapped in any element.

## Applicability

This rule applies to any HTML or SVG element that is [focusable][].

**Note:** This rule only applies to HTML and SVG. Thus, it is a partial check for WCAG 2.0 success criterion 2.1.2, which applies to all content.

## Expectation

For each target element focus can cycle to the browser UI by using [standard keyboard navigation](#standard-keyboard-navigation).

**Note:** Cycling back to the browser UI can be done both by moving forward through the tab order and by moving backwards. It is not possible to fulfill this expectation by using browser specific shortcuts to return to the browser UI.

## Assumptions

- The focus order in keyboard navigation is cyclical, not linear, meaning that the focus order will cycle to the first/last element when it moves away from the last/first element.
- The Browser UI is part of the focus navigation cycle of the page.

## Accessibility Support

There are no major accessibility support issues known for this rule.

## Background

- [Understanding Success Criterion 2.1.2: No Keyboard Trap](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
- [G21: Ensuring that users are not trapped in content](https://www.w3.org/WAI/WCAG21/Techniques/general/G21)
- [F10: Failure of Success Criterion 2.1.2 and Conformance Requirement 5 due to combining multiple content formats in a way that traps users inside one format type](https://www.w3.org/WAI/WCAG21/Techniques/failures/F10)

## Test Cases

### Passed

#### Passed Example 1

No trap for keyboard navigation.

```html
<a href="#">Link 1</a> <button>Button1</button>
```

#### Passed Example 2

Using `tabindex="1"`.

```html
<div tabindex="1">Text</div>
```

#### Passed Example 3

Using `tabindex="-1"`.

```html
<div tabindex="-1">Text</div>
```

### Failed

#### Failed Example 1

Keyboard trap one element.

```html
<a href="#">Link 1</a>
<button onblur="setTimeout(() => this.focus(), 10)">
	Button1
</button>
```

#### Failed Example 2

Keyboard trap group.

```html
<button onblur="setTimeout(() => this.nextElementSibling.focus(), 10)">
	Button1
</button>
<button onblur="setTimeout(() => this.previousElementSibling.focus(), 10)">
	Button2
</button>
<button>
	Button3
</button>
```

#### Failed Example 3

A [focusable][] element between keyboard traps.

```html
<button onblur="setTimeout(() => this.focus(), 10)">Button 1</button>
<button>Button 2</button>
<button onblur="setTimeout(() => this.focus(), 10)">Button 3</button>
```

### Inapplicable

#### Inapplicable Example 1

No [focusable][] element.

```html
<h1>Page 1</h1>
```

#### Inapplicable Example 2

Disabled element.

```html
<button type="button" disabled>Click Me!</button>
```

#### Inapplicable Example 3

Hidden element using `display:none`.

```html
<button type="button" style="display:none;">Click Me!</button>
```

#### Inapplicable Example 4

Hidden element using `visibility:hidden`.

```html
<a href="#" style="visibility:hidden;">Link 1</a> <button style="visibility:hidden;">Button1</button>
```

## Glossary

{% include_relative glossary/focusable.md %}
{% include_relative glossary/outcome.md %}
{% include_relative glossary/standard-keyboard-navigation.md %}

## Acknowledgements

This rule was written in the [ACT Rules community group](https://w3.org/community/act-r/), 
with the support of the EU-funded [WAI-Tools Project](https://www.w3.org/WAI/about/projects/wai-tools/).

### Authors

- [Anne Thyme Nørregaard](https://github.com/annethyme)
- [Carlos Duarte](https://github.com/carlosapaduarte)
- [Dagfinn Rømen](https://github.com/DagfinnRomen)
- [Geir Sindre Fossøy](https://github.com/geirsf)
- [Malin Øvrebø](https: //github.com/MaliinO)
- [Shadi Abou-Zahra](https://github.com/nitedog)
- [Stein Erik Skotkjerra](https://github.com/skotkjerra)

## Changelog

This is the first version of this ACT rule.

[focusable]: #focusable 'Definition of focusable'
