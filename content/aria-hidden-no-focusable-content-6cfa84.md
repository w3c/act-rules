---
title: "Element with aria-hidden has no focusable content"
permalink: /standards-guidelines/act/rules/aria-hidden-no-focusable-content-6cfa84/
ref: /standards-guidelines/act/rules/aria-hidden-no-focusable-content-6cfa84/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/aria-hidden-no-focusable-content-6cfa84.md
# footer: > # Text in footer in HTML
#   <p> This is the text in the footer </p>
---

{% include_relative _proposed-banner.html %}

Rule Type:
:   atomic

Rule ID:
:   6cfa84

Last Modified:
:   June 3, 2021

Accessibility Requirements Mapping:
:   [1.3.1 Info and Relationships (Level A)](https://www.w3.org/TR/WCAG21/#info-and-relationships)
    - **Required for conformance** to WCAG 2.0 and later on level A and higher
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion needs further testing
        - An `inapplicable` outcome: success criterion needs further testing
:   [4.1.2 Name, Role, Value (Level A)](https://www.w3.org/TR/WCAG21/#name-role-value)
    - **Required for conformance** to WCAG 2.0 and later on level A and higher
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion needs further testing
        - An `inapplicable` outcome: success criterion needs further testing
:   [Fourth rule of ARIA use](https://www.w3.org/TR/using-aria/#fourth)
    - Not required to conformance to any W3C accessibility recommendation.
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: WAI-ARIA rule is not satisfied
        - All `passed` outcomes: WAI-ARIA rule needs further testing
        - An `inapplicable` outcome: WAI-ARIA rule needs further testing

Input Aspects:
:   [DOM Tree](https://www.w3.org/TR/act-rules-aspects/#input-aspects-dom)
:   [CSS Styling](https://www.w3.org/TR/act-rules-aspects/#input-aspects-css)

## Description

This rule checks that elements with an `aria-hidden` attribute do not contain focusable elements.

## Applicability

This rule applies to any element with an `aria-hidden` [attribute value][] of `true`.

**Note:** Using `aria-hidden="false"` on a descendant of an element with `aria-hidden="true"` **does not** expose that element. `aria-hidden="true"` hides itself and all its content from assistive technologies.

## Expectation

None of the target elements are part of [sequential focus navigation](https://html.spec.whatwg.org/multipage/interaction.html#sequential-focus-navigation), nor do they have [descendants](https://dom.spec.whatwg.org/#concept-tree-descendant) in the [flat tree](https://drafts.csswg.org/css-scoping/#flat-tree) that are part of [sequential focus navigation](https://html.spec.whatwg.org/#sequential-focus-navigation).

## Assumptions

_There are currently no assumptions_

## Accessibility Support

Some user agents treat the value of `aria-hidden` attribute as case-sensitive.

## Background

By adding `aria-hidden="true"` to an element, content authors ensure that assistive technologies will ignore the element. This can be used to hide parts of a web page that are [pure decoration](https://www.w3.org/TR/WCAG21/#dfn-pure-decoration), such as icon fonts - that are not meant to be read by assistive technologies.

A [focusable][] element with `aria-hidden="true"` is ignored as part of the reading order, but still part of the focus order, making its state of [visible](#visible) or hidden unclear.

- [CSS Scoping Module Level 1 (editor's draft)](https://drafts.csswg.org/css-scoping/)
- [Understanding Success Criterion 1.3.1: Info and Relationships](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships)
- [Understanding Success Criterion 4.1.2: Name, Role, Value](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value)
- [`aria-hidden` (state)](https://www.w3.org/TR/wai-aria-1.1/#aria-hidden)
- [Fourth rule of ARIA use (work in progress)](https://www.w3.org/TR/using-aria/#fourth)

## Test Cases

### Passed

#### Passed Example 1

Content not [focusable][] by default.

```html
<p aria-hidden="true">Some text</p>
```

#### Passed Example 2

Content hidden through CSS.

```html
<div aria-hidden="true">
	<a href="/" style="display:none">Link</a>
</div>
```

#### Passed Example 3

Content taken out of sequential focus order using `tabindex`.

```html
<div aria-hidden="true">
	<button tabindex="-1">Some button</button>
</div>
```

#### Passed Example 4

Content made [unfocusable][focusable] through `disabled` attribute.

```html
<input disabled aria-hidden="true" />
```

#### Passed Example 5

`aria-hidden` can't be reset once set to true on an ancestor.

```html
<div aria-hidden="true">
	<div aria-hidden="false">
		<button tabindex="-1">Some button</button>
	</div>
</div>
```

#### Passed Example 6

Content taken out of sequential focus order using `tabindex`.

```html
<div aria-hidden="true">
	<button tabindex="-2">Some button</button>
</div>
```

### Failed

#### Failed Example 1

[Focusable][] off screen link.

```html
<div aria-hidden="true">
	<a href="/" style="position:absolute; top:-999em">Link</a>
</div>
```

#### Failed Example 2

[Focusable][] form field, incorrectly disabled.

```html
<div aria-hidden="true">
	<input aria-disabled="true" />
</div>
```

#### Failed Example 3

`aria-hidden` can't be reset once set to true on an ancestor.

```html
<div aria-hidden="true">
	<div aria-hidden="false">
		<button>Some button</button>
	</div>
</div>
```

#### Failed Example 4

[Focusable][] content through `tabindex`.

```html
<p tabindex="0" aria-hidden="true">Some text</p>
```

#### Failed Example 5

[Focusable][] `summary` element.

```html
<details aria-hidden="true">
	<summary>Some button</summary>
	<p>Some details</p>
</details>
```

### Inapplicable

#### Inapplicable Example 1

Ignore `aria-hidden` with null value.

```html
<button tabindex="-1" aria-hidden>Some button</button>
```

#### Inapplicable Example 2

Ignore `aria-hidden` false.

```html
<p aria-hidden="false">Some text</p>
```

#### Inapplicable Example 3

Incorrect value of `aria-hidden`.

```html
<div aria-hidden="yes">
	<p>Some text</p>
</div>
```

## Glossary

{% include_relative glossary/attribute-value.md %}
{% include_relative glossary/focusable.md %}
{% include_relative glossary/outcome.md %}
{% include_relative glossary/visible.md %}

## Acknowledgements

This rule was written in the [ACT Rules community group](https://w3.org/community/act-r/), 
with the support of the EU-funded [WAI-Tools Project](https://www.w3.org/WAI/about/projects/wai-tools/).

### Authors

- [Wilco Fiers](https://github.com/wilcofiers)

## Changelog

This is the first version of this ACT rule.

[attribute value]: #attribute-value 'Definition of Attribute Value'
[focusable]: #focusable 'Definition of focusable'
