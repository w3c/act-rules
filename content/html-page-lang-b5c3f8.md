---
title: "HTML page has lang attribute"
permalink: /standards-guidelines/act/rules/html-page-lang-b5c3f8/
ref: /standards-guidelines/act/rules/html-page-lang-b5c3f8/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/html-page-lang-b5c3f8.md
# footer: > # Text in footer in HTML
#   <p> This is the text in the footer </p>
---

Rule Type:
:   atomic

Rule ID:
:   b5c3f8

Last Modified:
:   March 5, 2020

Accessibility Requirements Mapping:
:   [3.1.1 Language of Page (Level A)](https://www.w3.org/TR/WCAG21/#language-of-page)
    - **Required for conformance** to WCAG 2.0 and later on level A and higher
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion needs further testing
        - An `inapplicable` outcome: success criterion needs further testing
:   [H57: Using language attributes on the html element](https://www.w3.org/WAI/WCAG21/Techniques/html/H57)
    - Not required to conformance to any W3C accessibility recommendation.
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: technique is not satisfied
        - All `passed` outcomes: technique needs further testing
        - An `inapplicable` outcome: technique needs further testing

Input Aspects:
:   [DOM Tree](https://www.w3.org/TR/act-rules-aspects/#input-aspects-dom)

## Description

This rule checks that an HTML page has a non-empty `lang` attribute.

## Applicability

This rule applies to any [document element](https://dom.spec.whatwg.org/#document-element) if it is an `html` element that:

- is in a [top-level browsing context](https://html.spec.whatwg.org/#top-level-browsing-context); and
- has a [node document](https://dom.spec.whatwg.org/#concept-node-document) with a [content type](https://dom.spec.whatwg.org/#concept-document-content-type) of `text/html`.

**Note:** `html` elements within `iframe` and `object` elements are not applicable as `iframe` and `object` elements create [nested browsing contexts](https://html.spec.whatwg.org/#nested-browsing-context). However, as these elements are meant to provide a layer of isolation, the declared language of their [parent browsing context](https://html.spec.whatwg.org/#parent-browsing-context) will likely not be inherited, making it possible for empty `lang` attributes in [nested browsing contexts](https://html.spec.whatwg.org/#nested-browsing-context) to also cause accessibility issues.

## Expectation

Each test target has a `lang` attribute that is neither empty (`""`) nor only [ASCII whitespace](https://infra.spec.whatwg.org/#ascii-whitespace).

## Assumptions

The language of the page can be set by other methods than the `lang` attribute, for example using HTTP headers or the `meta` element. These methods are not supported by all assistive technologies. This rule assumes that these other methods are insufficient to satisfying [Success Criterion 3.1.1: Language of Page](https://www.w3.org/TR/WCAG21/#language-of-page).

## Accessibility Support

_There are no major accessibility support issues known for this rule._

## Background

- [Understanding Success Criterion 3.1.1: Language of Page](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
- [H57: Using language attributes on the html element](https://www.w3.org/WAI/WCAG21/Techniques/html/H57)
- [BCP 47: Tags for Identifying Languages](https://www.ietf.org/rfc/bcp/bcp47.txt)
- [The `lang` and `xml:lang` attributes](https://html.spec.whatwg.org/multipage/dom.html#the-lang-and-xml:lang-attributes)

## Test Cases

### Passed

#### Passed Example 1

This `html` element has a `lang` attribute with a non-empty (`""`) value.

```html
<html lang="en"></html>
```

### Failed

#### Failed Example 1

This `html` element does not have a `lang` attribute.

```html
<html></html>
```

#### Failed Example 2

This `html` element has a `lang` attribute with an empty (`""`) value.

```html
<html lang=""></html>
```

#### Failed Example 3

This `html` element has a `lang` attribute whose value is only [ASCII whitespace](https://infra.spec.whatwg.org/#ascii-whitespace).

```html
<html lang=" "></html>
```

#### Failed Example 4

This `html` element has no `lang` attribute, only a `xml:lang` attribute.

```html
<html xml:lang="en"></html>
```

### Inapplicable

#### Inapplicable Example 1

This rule does not apply to `svg` element.

```svg
<svg xmlns="http://www.w3.org/2000/svg"></svg>
```

#### Inapplicable Example 2

This rule does not apply to `math` element.

```xml
<math></math>
```

## Glossary

{% include_relative glossary/outcome.md %}

## Acknowledgements

This rule was written in the [ACT Rules community group](https://w3.org/community/act-r/), 
with the support of the EU-funded [WAI-Tools Project](https://www.w3.org/WAI/about/projects/wai-tools/).

### Authors

- [Jey Nandakumar](https://github.com/jkodu)

### Previous Authors

- [Annika Nietzio](https://github.com/annika-FTB)

## Changelog

This is the first version of this ACT rule.

