---
title: "Image button has non-empty accessible name"
permalink: /standards-guidelines/act/rules/image-button-non-empty-accessible-name-59796f/
ref: /standards-guidelines/act/rules/image-button-non-empty-accessible-name-59796f/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/image-button-non-empty-accessible-name-59796f.md
# footer: > # Text in footer in HTML
#   <p> This is the text in the footer </p>
---

Rule Type:
:   atomic

Rule ID:
:   59796f

Last Modified:
:   Oct 13, 2020

Accessibility Requirements Mapping:
:   [1.1.1 Non-text Content (Level A)](https://www.w3.org/TR/WCAG21/#non-text-content)
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
:   [G94: Providing short text alternative for non-text content that serves the same purpose and presents the same information as the non-text content](https://www.w3.org/WAI/WCAG21/Techniques/general/G94)
    - Not required to conformance to any W3C accessibility recommendation.
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: technique is not satisfied
        - All `passed` outcomes: technique needs further testing
        - An `inapplicable` outcome: technique needs further testing
:   [G95: Providing short text alternatives that provide a brief description of the non-text content](https://www.w3.org/WAI/WCAG21/Techniques/general/G95)
    - Not required to conformance to any W3C accessibility recommendation.
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: technique is not satisfied
        - All `passed` outcomes: technique needs further testing
        - An `inapplicable` outcome: technique needs further testing

Input Aspects:
:   [DOM Tree](https://www.w3.org/TR/act-rules-aspects/#input-aspects-dom)
:   [CSS Styling](https://www.w3.org/TR/act-rules-aspects/#input-aspects-css)

## Description

This rule checks that each image button element has a non-empty accessible name.

## Applicability

The rule applies to any `input` element where the [state of the `type` attribute](https://html.spec.whatwg.org/multipage/input.html#states-of-the-type-attribute) is `image`, and that is [included in the accessibility tree][].

## Expectation

Each target element has an [accessible name][] that is not empty (`""`).

## Assumptions

- This rule assumes that all image buttons are [user interface components as defined by WCAG 2](https://www.w3.org/TR/WCAG21/#dfn-user-interface-components).

## Accessibility Support

There is a known combination of a popular browser and assistive technology that does not by default support `title` as an [accessible name][].

## Background

- [Understanding Success Criterion 1.1.1: Non-text Content](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
- [Understanding Success Criterion 4.1.2: Name, Role, Value](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
- [WCAG Technique H36: Using alt attributes on images used as submit buttons](https://www.w3.org/WAI/WCAG21/Techniques/html/H36)

## Test Cases

### Passed

#### Passed Example 1

The image button has an [accessible name][] through the `alt` attribute.

```html
<input type="image" src="/test-assets/shared/search-icon.svg" alt="Search" />
```

#### Passed Example 2

The image button has an [accessible name][] through the `aria-label` attribute.

```html
<input type="image" src="/test-assets/shared/search-icon.svg" aria-label="Search" />
```

#### Passed Example 3

The image button has an [accessible name][] through the `title` attribute.

**note**: The `title` attribute may not always be [accessibility supported](#accessibility-support).

```html
<input type="image" src="/test-assets/shared/search-icon.svg" title="Search" />
```

#### Passed Example 4

The image button has an [accessible name][] through the `aria-labelledby` attribute.

```html
<input type="image" src="/test-assets/shared/search-icon.svg" aria-labelledby="id1" />
<div id="id1">Search</div>
```

### Failed

#### Failed Example 1

The image button element has an empty [accessible name][]. The `name` attribute can not be used to provide an [accessible name][].

```html
<input type="image" name="search" src="/test-assets/shared/search-icon.svg" />
```

#### Failed Example 2

The image button has an empty `alt` attribute, and no other attributes that can give it an [accessible name][].

```html
<input type="image" src="/test-assets/shared/search-icon.svg" alt="" />
```

#### Failed Example 3

The image button has an `aria-labelledby` attribute, but the referenced element does not exist. This gives the button an empty [accessible name][].

```html
<input type="image" src="/test-assets/shared/search-icon.svg" aria-labelledby="non-existing" />
```

### Inapplicable

#### Inapplicable Example 1

The `button` element is not an image button. [Success Criterion 1.1.1 Non-text Content](https://www.w3.org/TR/WCAG21/#non-text-content) can not fail text buttons. Only non-text content is applicable.

```html
<button>My button</button>
```

#### Inapplicable Example 2

The `input` element with type with a `type` attribute in the `Button` state is not an image button. [Success Criterion 1.1.1 Non-text Content](https://www.w3.org/TR/WCAG21/#non-text-content) can not fail text buttons. Only non-text content is applicable.

```html
<input type="button" value="My button" />
```

#### Inapplicable Example 3

The `button` element is tested separately from the `img` element. [Success Criterion 4.1.2 Name, Role, Value](https://www.w3.org/TR/WCAG21/#name-role-value) is applied to the button, whereas the image is tested under [Success Criterion 1.1.1 Non-text Content](https://www.w3.org/TR/WCAG21/#non-text-content)

```html
<button><img src="/test-assets/shared/search-icon.svg" alt="Search" /></button>
```

#### Inapplicable Example 4

The `img` element is not a user interface component, and so is not tested for [Success Criterion 4.1.2 Name, Role, Value](https://www.w3.org/TR/WCAG21/#name-role-value).

```html
<img src="/test-assets/shared/w3c-logo.png" alt="W3C logo" />
```

#### Inapplicable Example 5

The image button is ignored by assistive technologies because it is not [included in the accessibility tree][]. These are not required to have an accessible name. If at some future state of the page the element gets [included in the accessibility tree][], an [accessible name][] will be necessary.

```html
<input type="image" src="/test-assets/shared/search-icon.svg" style="display: none;" />
```

## Glossary

{% include_relative glossary/accessible-name.md %}
{% include_relative glossary/focusable.md %}
{% include_relative glossary/included-in-the-accessibility-tree.md %}
{% include_relative glossary/outcome.md %}

## Acknowledgements

This rule was written in the [ACT Rules community group](https://w3.org/community/act-r/), 
with the support of the EU-funded [WAI-Tools Project](https://www.w3.org/WAI/about/projects/wai-tools/).

### Authors

- [Anne Thyme Nørregaard](https://github.com/annethyme)

## Changelog

- **Oct 13, 2020**:
    - Added "non-empty" to the rule title
    - Added mapping to technique G94 and G95

[included in the accessibility tree]: #included-in-the-accessibility-tree 'Definition of included in the accessibility tree'
[accessible name]: #accessible-name 'Definition of accessible name'
