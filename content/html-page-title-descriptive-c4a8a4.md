---
title: "HTML page title is descriptive"
permalink: /standards-guidelines/act/rules/html-page-title-descriptive-c4a8a4/
ref: /standards-guidelines/act/rules/html-page-title-descriptive-c4a8a4/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/html-page-title-descriptive-c4a8a4.md
# footer: > # Text in footer in HTML
#   <p> This is the text in the footer </p>
---

{% include_relative _proposed-banner.html %}

Rule Type:
:   atomic

Rule ID:
:   c4a8a4

Last Modified:
:   June 3, 2021

Accessibility Requirements Mapping:
:   [2.4.2 Page Titled (Level A)](https://www.w3.org/TR/WCAG21/#page-titled)
    - **Required for conformance** to WCAG 2.0 and later on level A and higher
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion is satisfied
        - An `inapplicable` outcome: success criterion needs further testing
:   [G88: Providing descriptive titles for Web pages](https://www.w3.org/WAI/WCAG21/Techniques/general/G88)
    - Not required to conformance to any W3C accessibility recommendation.
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: technique is not satisfied
        - All `passed` outcomes: technique needs further testing
        - An `inapplicable` outcome: technique needs further testing
:   [H25: Providing a title using the title element](https://www.w3.org/WAI/WCAG21/Techniques/html/H25)
    - Not required to conformance to any W3C accessibility recommendation.
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: technique is not satisfied
        - All `passed` outcomes: technique needs further testing
        - An `inapplicable` outcome: technique needs further testing

Input Aspects:
:   [DOM Tree](https://www.w3.org/TR/act-rules-aspects/#input-aspects-dom)
:   [Language](https://www.w3.org/TR/act-rules-aspects/#input-aspects-text)

## Description

This rule checks that the first title in an HTML page describes the topic or purpose of that page.

## Applicability

This rule applies to the first HTML `title` element that

- is a [descendant](https://dom.spec.whatwg.org/#concept-tree-descendant) of the `html` element of a [web page](https://www.w3.org/TR/WCAG21/#dfn-web-page-s), and
- contains [children](https://dom.spec.whatwg.org/#concept-tree-child) that are [text nodes](https://dom.spec.whatwg.org/#text) that are not only [whitespace](#whitespace).

## Expectation

The target element describes the topic or purpose of the overall content of the [document](https://dom.spec.whatwg.org/#concept-document).

## Assumptions

This rule assumes that the language of each test target can be correctly determined (either programmatically or by analyzing the content), and sufficiently understood.

## Accessibility Support

- This rule assumes that browsers only recognize the first `title` element if multiple `title` elements are present in the [document](https://dom.spec.whatwg.org/#concept-document). Testing shows that this in general is the case. Therefore the scope of this rule is limited to only checking the first `title` element in a document.

## Background

The `title` elements of embedded documents, such as those in `iframe`, `object`, or `svg` elements, are not applicable because those are not web pages according to the definition in WCAG.

The [HTML specification - The `title` element](https://html.spec.whatwg.org/#the-title-element) requires that a document only has one `title` element, and that it is a child of the `head` element of a document. However, current HTML specification also describes what should happen in case of multiple titles, and titles outside the `head` element. Because of this, neither of these validation issues causes a conformance problem for WCAG.

- [HTML page has non-empty title](https://act-rules.github.io/rules/2779a5)
- [Understanding Success Criterion 2.4.2: Page titled](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
- This rule is testing [Technique G88: Providing descriptive titles for Web pages](https://www.w3.org/WAI/WCAG21/Techniques/general/G88)
- A prerequisite for this rule is that [Technique H25: Providing a title using the title element](https://www.w3.org/WAI/WCAG21/Techniques/html/H25) is used for living up to 2.4.2 Page Titled

## Test Cases

### Passed

#### Passed Example 1

This `<title>` element describes the content of the document.

```html
<html lang="en">
	<head>
		<title>Clementine harvesting season</title>
	</head>
	<body>
		<p>
			Clementines will be ready to harvest from late October through February.
		</p>
	</body>
</html>
```

#### Passed Example 2

This `<title>` element, the first of two, describes the content of the document.

```html
<html lang="en">
	<head>
		<title>Clementine harvesting season</title>
		<title>Second title is ignored</title>
	</head>
	<body>
		<p>
			Clementines will be ready to harvest from late October through February.
		</p>
	</body>
</html>
```

#### Passed Example 3

This `<title>` element, which is within the `body`, describes the content of the document. Even though it is not placed within the `<head>` element, as expected [according to the HTML specification](https://html.spec.whatwg.org/#the-title-element), the rule still passes because the browser fixes it and it doesn't cause any known accessibility issues.

```html
<html lang="en">
	<head> </head>
	<body>
		<title>Clementine harvesting season</title>
		<p>
			Clementines will be ready to harvest from late October through February.
		</p>
	</body>
</html>
```

### Failed

#### Failed Example 1

This `<title>` element does not describe the content of the document.

```html
<html lang="en">
	<head>
		<title>Apple harvesting season</title>
	</head>
	<body>
		<p>
			Clementines will be ready to harvest from late October through February.
		</p>
	</body>
</html>
```

#### Failed Example 2

This `<title>` element, the first of two, does not describe the content of the document. Most browsers, and this rule, only look at the first `<title>` element.

```html
<html lang="en">
	<head>
		<title>First title is incorrect</title>
		<title>Clementine harvesting season</title>
	</head>
	<body>
		<p>
			Clementines will be ready to harvest from late October through February.
		</p>
	</body>
</html>
```

### Inapplicable

#### Inapplicable Example 1

This `title` element is a child of an `svg` element.

```svg
<svg xmlns="http://www.w3.org/2000/svg">
  <title>This is a circle</title>
  <circle cx="150" cy="75" r="50" fill="green"></circle>
</svg>
```

## Glossary

{% include_relative glossary/outcome.md %}
{% include_relative glossary/whitespace.md %}

## Acknowledgements

This rule was written in the [ACT Rules community group](https://w3.org/community/act-r/), 
with the support of the EU-funded [WAI-Tools Project](https://www.w3.org/WAI/about/projects/wai-tools/).

### Authors

- [Anne Thyme Nørregaard](https://github.com/annethyme)
- [Corbb O'Connor](https://github.com/corbb)

## Changelog

This is the first version of this ACT rule.

