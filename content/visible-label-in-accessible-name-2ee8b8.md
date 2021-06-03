---
title: "Visible label is part of accessible name"
permalink: /standards-guidelines/act/rules/visible-label-in-accessible-name-2ee8b8/
ref: /standards-guidelines/act/rules/visible-label-in-accessible-name-2ee8b8/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/visible-label-in-accessible-name-2ee8b8.md
# footer: > # Text in footer in HTML
#   <p> This is the text in the footer </p>
---

{% include_relative _proposed-banner.html %}

Rule Type:
:   atomic

Rule ID:
:   2ee8b8

Last Modified:
:   June 3, 2021

Accessibility Requirements Mapping:
:   [2.5.3 Label in Name (Level A)](https://www.w3.org/TR/WCAG21/#label-in-name)
    - **Required for conformance** to WCAG 2.1 on level A and higher
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion needs further testing
        - An `inapplicable` outcome: success criterion needs further testing
:   [G208: Including the text of the visible label as part of the accessible name](https://www.w3.org/WAI/WCAG21/Techniques/general/G208)
    - Not required to conformance to any W3C accessibility recommendation.
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: technique is not satisfied
        - All `passed` outcomes: technique needs further testing
        - An `inapplicable` outcome: technique needs further testing

Input Aspects:
:   [Accessibility Tree](https://www.w3.org/TR/act-rules-aspects/#input-aspects-accessibility)
:   [DOM Tree](https://www.w3.org/TR/act-rules-aspects/#input-aspects-dom)
:   [CSS Styling](https://www.w3.org/TR/act-rules-aspects/#input-aspects-css)

## Description

This rule checks that interactive elements labeled through content have their visible label as part of their accessible name.

## Applicability

This rule applies to any element for which all the following is true:

- The element has a [semantic role][] that is a [widget][widget role] that [supports name from content][]; and
- The element has [visible text content][]; and
- The element has an `aria-label` or `aria-labelledby` attribute.

## Expectation

For each target element, all [text nodes][] in the [visible text content][] either match or are contained within the [accessible name][] of this target element, except for characters in the [text nodes][] used to express [non-text content][]. Leading and trailing [whitespace][] and difference in case sensitivity should be ignored.

## Assumptions

_There are currently no assumptions_

## Accessibility Support

Implementation of [Presentational Roles Conflict Resolution][] varies from one browser or assistive technology to another. Depending on this, some elements can have one of the applicable [semantic roles][semantic role] and fail this rule with some technology but users of other technologies would not experience any accessibility issue.

## Background

This rule applies to elements with a [widget role][] that [support name from content][supports name from content]. This includes the following: `button`, `checkbox`, `gridcell`, `link`, `menuitem`, `menuitemcheckbox`, `menuitemradio`, `option`, `radio`, `searchbox`, `switch`, `tab`, `treeitem`.

The understanding document of [2.5.3 Label in Name][understand253] use the term "symbolic text characters" to refer to a type of [non-text content][] that uses text characters as symbols, such as using "x" to mean "close". This rule considers them as "characters expressing non-text content". Unicode emojis are another example of characters expressing non-text content, although these are not "symbolic text characters".

- [Understanding Success Criterion 2.5.3: Label in Name][understand253]
- [G208: Including the text of the visible label as part of the accessible name](https://www.w3.org/WAI/WCAG21/Techniques/general/G208)

## Test Cases

### Passed

#### Passed Example 1

This link has [visible][] text that matches the [accessible name][].

```html
<a href="https://act-rules.github.io/" aria-label="ACT rules">ACT rules</a>
```

#### Passed Example 2

This link has [visible][] text that, ignoring trailing whitespace, matches the [accessible name][].

```html
<a href="https://act-rules.github.io/" aria-label="  ACT rules  ">ACT rules</a>
```

#### Passed Example 3

This link has [visible][] text that, ignoring case, matches the [accessible name][].

```html
<a href="https://act-rules.github.io/" aria-label="act rules">ACT rules</a>
```

#### Passed Example 4

This button has [visible][] text that is contained within the [accessible name][].

```html
<button aria-label="Next Page in the list">Next Page</button>
```

#### Passed Example 5

This button has [visible][] text that does not need to be contained within the [accessible name][], because the "x" text node is [non-text content][].

```html
<button aria-label="close">X</button>
```

#### Passed Example 6

This `button` element has the text "search" rendered as an magnifying glass icon by the font. Because the text is rendered as [non-text content][], the text does not need to be contained within the [accessible name][].

```html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
<style>
	button {
		font-family: 'Material Icons';
	}
</style>
<button aria-label="Find">search</button>
```

### Failed

#### Failed Example 1

This link has [visible][] text that is different from the [accessible name][].

```html
<a href="https://act-rules.github.io/" aria-label="WCAG">ACT rules</a>
```

#### Failed Example 2

This button has [visible][] text that is only partially contained within the [accessible name][].

```html
<button aria-label="the full">The full label</button>
```

#### Failed Example 3

This link has [visible][] text with mathematical symbols, that does not match the [accessible name][] because the mathematical symbols were written out in the accessible name. This is [explicitly mentioned in WCAG](https://www.w3.org/WAI/WCAG21/Understanding/label-in-name#mathematical-expressions-and-formulae).

```html
<a href="/" aria-label="Proof of two multiplied by two is four">Proof of 2&times;2=4</a>
```

### Inapplicable

#### Inapplicable Example 1

This `nav` is not a widget, so the [visible][] text does not need to match the [accessible name][].

```html
<nav aria-label="main nav">W3C navigation</nav>
```

#### Inapplicable Example 2

This email text field does not need to have its [visible][] text match the [accessible name][]. The content of a textfield shows its value instead of its label; it does not [support name from content][supports name from content]. The label is usually adjacent to the textfield instead.

```html
<div>E-mail</div>
<input type="email" aria-label="E-mail" value="Contact" />
```

#### Inapplicable Example 3

This `div` element does not have a widget role, so the [visible][] text does not need to match the [accessible name][].

```html
<div role="tooltip" aria-label="OK">Next</div>
```

#### Inapplicable Example 4

This link has no [visible text content][].

```html
<a href="https://w3.org" aria-label="W3C homepage">
	<img src="/test-assets/shared/w3c-logo.png" alt="w3c logo" />
</a>
```

## Glossary

{% include_relative glossary/accessible-name.md %}
{% include_relative glossary/explicit-role.md %}
{% include_relative glossary/focusable.md %}
{% include_relative glossary/hidden-state.md %}
{% include_relative glossary/implicit-role.md %}
{% include_relative glossary/included-in-the-accessibility-tree.md %}
{% include_relative glossary/marked-as-decorative.md %}
{% include_relative glossary/outcome.md %}
{% include_relative glossary/semantic-role.md %}
{% include_relative glossary/visible.md %}
{% include_relative glossary/visible-text-content.md %}
{% include_relative glossary/wai-aria-specifications.md %}
{% include_relative glossary/whitespace.md %}

## Acknowledgements

This rule was written in the [ACT Rules community group](https://w3.org/community/act-r/), 
with the support of the EU-funded [WAI-Tools Project](https://www.w3.org/WAI/about/projects/wai-tools/).

### Authors

- [Anne Thyme Nørregaard](https://github.com/annethyme)
- [Bryn Anderson](https://github.com/brynanders)
- [Jey Nandakumar](https://github.com/jkodu)

## Changelog

This is the first version of this ACT rule.

[accessible name]: #accessible-name 'Definition of accessible name'
[non-text content]: https://www.w3.org/TR/WCAG21/#dfn-non-text-content 'WCAG Definition of Non-text content'
[presentational roles conflict resolution]: https://www.w3.org/TR/wai-aria-1.1/#conflict_resolution_presentation_none 'Presentational Roles Conflict Resolution'
[semantic role]: #semantic-role 'Definition of Semantic role'
[supports name from content]: https://www.w3.org/TR/wai-aria-1.1/#namefromcontent 'Definition of Supports name from contents'
[visible]: #visible 'Definition of visible'
[visible text content]: #visible-text-content 'Definition of Visible text content'
[whitespace]: #whitespace 'Definition of Whitespace'
[widget role]: https://www.w3.org/TR/wai-aria-1.1/#widget_roles 'Definition of Widget role'
[text nodes]: https://dom.spec.whatwg.org/#text 'DOM text, 2020/08/18'
[understand253]: https://www.w3.org/WAI/WCAG21/Understanding/label-in-name.html
