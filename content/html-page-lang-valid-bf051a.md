---
title: "HTML page lang attribute has valid language tag"
permalink: /standards-guidelines/act/rules/html-page-lang-valid-bf051a/
ref: /standards-guidelines/act/rules/html-page-lang-valid-bf051a/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/html-page-lang-valid-bf051a.md
# footer: > # Text in footer in HTML
#   <p> This is the text in the footer </p>
---

Rule Type:
:   atomic

Rule ID:
:   bf051a

Last Modified:
:   Oct 6, 2020

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

This rule checks that the `lang` attribute of the root element of a non-embedded HTML page has a language tag with a known primary language subtag.

## Applicability

This rule applies to any [document element](https://dom.spec.whatwg.org/#document-element) if it is an `html` element that:

- has a `lang` attribute that is neither empty ("") nor only [ASCII whitespace](https://infra.spec.whatwg.org/#ascii-whitespace); and
- is in a [top-level browsing context](https://html.spec.whatwg.org/#top-level-browsing-context); and
- has a [node document](https://dom.spec.whatwg.org/#concept-node-document) with a [content type](https://dom.spec.whatwg.org/#concept-document-content-type) of `text/html`.

## Expectation

For each test target, the `lang` attribute has a [valid language tag][].

## Assumptions

- The language of the page can be set by other methods than the `lang` attribute, for example using HTTP headers or the `meta` element. These methods are not supported by all assistive technologies. This rule assumes that these other methods are insufficient to satisfying [Success Criterion 3.1.1: Language of Page](https://www.w3.org/TR/WCAG21/#language-of-page).

- This rule assumes that user agents and assistive technologies can programmatically determine [valid language tags](#valid-language-tag) even if these do not conform to the [BCP 47][] syntax.

- This rule assumes that [grandfathered tags][] are not used as these will not be recognized as [valid language tags](#valid-language-tag).

## Accessibility Support

_There are no major accessibility support issues known for this rule._

## Background

This rule is only applicable to non-embedded HTML pages. HTML pages embedded into other documents, such as through `iframe` or `object` elements are not applicable because they are not [web pages](https://www.w3.org/TR/WCAG21/#dfn-web-page-s) according to the definition in WCAG.

- [Understanding Success Criterion 3.1.1: Language of Page](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
- [H57: Using language attributes on the html element](https://www.w3.org/WAI/WCAG21/Techniques/html/H57)
- [BCP 47: Tags for Identifying Languages](https://www.ietf.org/rfc/bcp/bcp47.txt)
- [The `lang` and `xml:lang` attributes](https://html.spec.whatwg.org/multipage/dom.html#the-lang-and-xml:lang-attributes)

## Test Cases

### Passed

#### Passed Example 1

This `html` element has a `lang` attribute whose value is a [valid][valid language tag] [primary language subtag][].

```html
<html lang="fr"></html>
```

#### Passed Example 2

This `html` element has a `lang` attribute value that is a [valid language tag][] even though the [region subtag][] is not.

```html
<html lang="en-US-GB"></html>
```

### Failed

#### Failed Example 1

This `html` element has a `lang` attribute whose value is not a [valid language tag][].

```html
<html lang="em-US"></html>
```

#### Failed Example 2

This `html` element has a `lang` attribute whose value is not a [valid language tag][].

```html
<html lang="#1"></html>
```

### Inapplicable

#### Inapplicable Example 1

This rule does not apply to `svg` elements.

```svg
<svg xmlns="http://www.w3.org/2000/svg" lang="fr"></svg>
```

## Glossary

{% include_relative glossary/outcome.md %}
{% include_relative glossary/valid-language-tag.md %}

## Acknowledgements

This rule was written in the [ACT Rules community group](https://w3.org/community/act-r/), 
with the support of the EU-funded [WAI-Tools Project](https://www.w3.org/WAI/about/projects/wai-tools/).

### Authors

- [Jey Nandakumar](https://github.com/jkodu)

### Previous Authors

- [Annika Nietzio](https://github.com/annika-FTB)

## Changelog

- **October 6st**
  - Rename definition "valid language subtag" to "valid language tag"
  - Clarify the title

[primary language subtag]: https://tools.ietf.org/html/bcp47#section-2.2.1 'Definition of primary language subtag'
[region subtag]: https://tools.ietf.org/html/bcp47#section-2.2.4 'Definition of region subtag'
[valid language tag]: #valid-language-tag 'Definition of valid language tag'
[grandfathered tags]: https://tools.ietf.org/html/bcp47#section-2.2.8
[bcp 47]: https://tools.ietf.org/html/bcp47#section-2.1
