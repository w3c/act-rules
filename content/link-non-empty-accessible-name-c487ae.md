---
title: "Link has non-empty accessible name"
permalink: /standards-guidelines/act/rules/link-non-empty-accessible-name-c487ae/
ref: /standards-guidelines/act/rules/link-non-empty-accessible-name-c487ae/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/link-non-empty-accessible-name-c487ae.md
# footer: > # Text in footer in HTML
#   <p> This is the text in the footer </p>
---

Rule Type:
:   atomic

Rule ID:
:   c487ae

Last Modified:
:   Oct 12, 2020

Accessibility Requirements Mapping:
:   [4.1.2 Name, Role, Value (Level A)](https://www.w3.org/TR/WCAG21/#name-role-value)
    - **Required for conformance** to WCAG 2.0 and later on level A and higher
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion needs further testing
        - An `inapplicable` outcome: success criterion needs further testing
:   [2.4.4 Link Purpose (In Context) (Level A)](https://www.w3.org/TR/WCAG21/#link-purpose-in-context)
    - **Required for conformance** to WCAG 2.0 and later on level A and higher
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion needs further testing
        - An `inapplicable` outcome: success criterion needs further testing
:   [2.4.9 Link Purpose (Link Only) (Level AAA)](https://www.w3.org/TR/WCAG21/#link-purpose-link-only)
    - **Required for conformance** to WCAG 2.0 and later on level AAA
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion needs further testing
        - An `inapplicable` outcome: success criterion needs further testing
:   [G91: Providing link text that describes the purpose of a link](https://www.w3.org/WAI/WCAG21/Techniques/general/G91)
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

This rule checks that each link has a non-empty accessible name.

## Applicability

The rule applies to any HTML element with the [semantic role][] of `link` that is [included in the accessibility tree][].

## Expectation

Each target element has an [accessible name][] that is not empty (`""`).

## Assumptions

The rule assumes that all links are [user interface components](https://www.w3.org/TR/WCAG21/#dfn-user-interface-components) as defined by WCAG 2. When the link role is used on elements that do not behave as links, failing this rule might not mean that the success criteria are failed.

## Accessibility Support

- There are assistive technologies that do not support using the `title` attribute for an [accessible name][], or in which this feature can be disabled.
- For `area` elements that have an `href` attribute, but are not nested inside a `map` element, there are differences between browsers and assistive technology on if the `area` is [included in the accessibility tree][].
- Implementation of [Presentational Roles Conflict Resolution][] varies from one browser or assistive technology to another. Depending on this, some elements can have a [semantic role][] of `link` and fail this rule with some technology but users of other technologies would not experience any accessibility issue.

## Background

- [Understanding Success Criterion 2.4.4: Link Purpose (In Context)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context)
- [ARIA7: Using aria-labelledby for link purpose](https://www.w3.org/WAI/WCAG21/Techniques/aria/ARIA7)
- [ARIA8: Using aria-label for link purpose](https://www.w3.org/WAI/WCAG21/Techniques/aria/ARIA8)
- [Understanding Success Criterion 4.1.2: Name, Role, Value](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value)
- [F89: Failure of Success Criteria 2.4.4, 2.4.9 and 4.1.2 due to not providing an accessible name for an image which is the only content in a link](https://www.w3.org/WAI/WCAG21/Techniques/failures/F89)

## Test Cases

### Passed

#### Passed Example 1

This `a` element has an [accessible name][] from its content.

```html
<a href="https://www.w3.org/WAI"> Web Accessibility Initiative (WAI) </a>
```

#### Passed Example 2

This `div` element has an [explicit semantic role](#explicit-role) of `link` and an [accessible name][] from its content.

```html
<div role="link" onclick="window.location.href='https://www.w3.org/WAI/'">Web Accessibility Initiative (WAI)</div>
```

#### Passed Example 3

This `button` element has an [explicit semantic role](#explicit-role) of `link` and an [accessible name][] from its content.

```html
<button role="link" onclick="window.location.href='https://www.w3.org/WAI/'">Click me for WAI!</button>
```

#### Passed Example 4

This `a` element has an [accessible name][] via `aria-label`

```html
<a href="https://www.w3.org/WAI"
	><img src="/test-assets/shared/w3c-logo.png" aria-label="Web Accessibility Initiative"
/></a>
```

#### Passed Example 5

This `a` element has an [accessible name][] via `title`.

```html
<a href="https://www.w3.org/WAI" title="Web Accessibility Initiative"
	><img src="/test-assets/shared/w3c-logo.png" alt=""
/></a>
```

#### Passed Example 6

This `a` element has an [accessible name][] from its content via the `title` on the `img` element.

```html
<a href="https://www.w3.org/WAI"><img src="/test-assets/shared/w3c-logo.png" title="Web Accessibility Initiative"/></a>
```

#### Passed Example 7

This `a` element has an [accessible name][] from its content.

```html
<a href="https://www.w3.org/WAI"
	><img src="/test-assets/shared/w3c-logo.png" alt="" />Web Accessibility Initiative (WAI)</a
>
```

#### Passed Example 8

This `a` element has an [accessible name][] from its content via `aria-labelledby` on the `img` element.

```html
<a href="https://www.w3.org/WAI"><img src="/test-assets/shared/w3c-logo.png" aria-labelledby="id1"/></a>
<div id="id1">Web Accessibility Initiative (WAI)</div>
```

#### Passed Example 9

This `a` element placed off screen has an [accessible name][] from its content.

```html
<html>
	<style>
		.offScreenLink {
			position: absolute;
			left: -9999px;
			top: -9999px;
		}
	</style>
	<body>
		<a class="offScreenLink" href="https://www.w3.org/WAI">Web Accessibility Initiative (WAI)</a>
	</body>
</html>
```

#### Passed Example 10

This `area` element has a [semantic role][] of `link` and an [accessible name][] via `alt`.

```html
<img src="/test-assets/c487ae/planets.jpg" width="145" height="126" alt="Planets" usemap="#planetmap" />

<map name="planetmap">
	<area shape="rect" coords="0,0,30,100" href="sun.htm" alt="Sun" />
</map>
```

### Failed

#### Failed Example 1

This `a` element has an empty [accessible name][].

```html
<a href="http://www.w3.org/WAI"></a>
```

#### Failed Example 2

This `a` element with an image has an empty [accessible name][]. The image is decorative and is marked as such with an empty `alt` [attribute value][].

```html
<a href="https://www.w3.org/WAI"><img src="/test-assets/shared/w3c-logo.png" alt=""/></a>
```

#### Failed Example 3

This `a` element with an image has an empty [accessible name][]. The image is decorative because it has a `role` [attribute value][] of `presentation`.

```html
<a href="http://www.w3.org/WAI"><img src="/test-assets/shared/w3c-logo.png" role="presentation"/></a>
```

#### Failed Example 4

This `a` element with an image has an empty [accessible name][]. The image is decorative because it has a `role` [attribute value][] of `none`.

```html
<a href="http://www.w3.org/WAI"><img src="/test-assets/shared/w3c-logo.png" role="none"/></a>
```

#### Failed Example 5

This `a` element with an `img` with an empty `title` has an empty [accessible name][].

```html
<a href="https://www.w3.org/WAI"><img src="/test-assets/shared/w3c-logo.png" title=""/></a>
```

#### Failed Example 6

This `a` element with an `img` with an `aria-labelledby` has an empty [accessible name][].

```html
<a href="https://www.w3.org/WAI"><img src="/test-assets/shared/w3c-logo.png" aria-labelledby="id1"/></a>
<div id="id1"></div>
```

#### Failed Example 7

This `a` element with an `img` with an `aria-labelledby` referencing a non-existing id has an empty [accessible name][].

```html
<a href="https://www.w3.org/WAI"><img src="/test-assets/shared/w3c-logo.png" aria-labelledby="id1"/></a>
```

#### Failed Example 8

This `a` element placed off screen has an empty [accessible name][].

```html
<a href="https://www.w3.org/WAI" style="left: -9999px; position: absolute;">
	<img src="/test-assets/shared/w3c-logo.png" />
</a>
```

#### Failed Example 9

This `area` element has a [semantic role][] of `link` and an empty [accessible name][].

```html
<img src="/test-assets/c487ae/planets.jpg" width="145" height="126" alt="Planets" usemap="#planetmap" />

<map name="planetmap">
	<area shape="rect" coords="0,0,82,126" href="sun.htm" />
</map>
```

#### Failed Example 10

This `a` element has an [explicit role][] of `none`. However, it is [focusable][] (by default). Thus it has a [semantic role][] of `link` due to [Presentational Roles Conflict Resolution][]. It has an empty [accessible name][].

```html
<a href="https://www.w3.org/WAI" role="none"> </a>
```

### Inapplicable

#### Inapplicable Example 1

This `a` element does not have a [semantic role][] of `link` because it has been changed to `button`.

```html
<a href="https://www.w3.org/WAI" role="button">
	Web Accessibility Initiative (WAI)
</a>
```

#### Inapplicable Example 2

This `a` element is not [included in the accessibility tree][] due to `display: none`.

```html
<a href="https://www.w3.org/WAI" style="display: none;"><img src="/test-assets/shared/w3c-logo.png"/></a>
```

#### Inapplicable Example 3

This `a` element is not [included in the accessibility tree][] due to `visibility: hidden`.

```html
<a href="https://www.w3.org/WAI" style="visibility: hidden;">Some text</a>
```

#### Inapplicable Example 4

This `a` element is not [included in the accessibility tree][] due to `aria-hidden="true"`.

```html
<a aria-hidden="true" href="https://www.w3.org/WAI">
	Web Accessibility Initiative (WAI)
</a>
```

#### Inapplicable Example 5

This `area` element does not have the role of link because it does not have an `href` attribute.

```html
<area shape="rect" coords="0,0,82,126" />
```

#### Inapplicable Example 6

This `a` element does not have the role of link because it does not have an `href` attribute.

```html
<a />
```

## Glossary

{% include_relative glossary/accessible-name.md %}
{% include_relative glossary/attribute-value.md %}
{% include_relative glossary/explicit-role.md %}
{% include_relative glossary/focusable.md %}
{% include_relative glossary/hidden-state.md %}
{% include_relative glossary/implicit-role.md %}
{% include_relative glossary/included-in-the-accessibility-tree.md %}
{% include_relative glossary/marked-as-decorative.md %}
{% include_relative glossary/outcome.md %}
{% include_relative glossary/semantic-role.md %}
{% include_relative glossary/wai-aria-specifications.md %}

## Acknowledgements

This rule was written in the [ACT Rules community group](https://w3.org/community/act-r/), 
with the support of the EU-funded [WAI-Tools Project](https://www.w3.org/WAI/about/projects/wai-tools/).

### Authors

- [Anne Thyme Nørregaard](https://github.com/annethyme)
- [Wilco Fiers](https://github.com/wilcofiers)

### Image

- Image used in passed example 10 and failed example 9 is courtesy of NASA/JPL-Caltech.

## Changelog

This is the first version of this ACT rule.

[accessible name]: #accessible-name 'Definition of accessible name'
[explicit role]: #explicit-role 'Definition of Explicit Role'
[focusable]: #focusable 'Definition of focusable'
[included in the accessibility tree]: #included-in-the-accessibility-tree 'Definition of included in the accessibility tree'
[presentational roles conflict resolution]: https://www.w3.org/TR/wai-aria-1.1/#conflict_resolution_presentation_none 'Presentational Roles Conflict Resolution'
[semantic role]: #semantic-role 'Definition of Semantic Role'
[attribute value]: #attribute-value 'Definition of Attribute value'
