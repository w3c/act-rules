---
title: "Scrollable element is keyboard accessible"
permalink: /standards-guidelines/act/rules/scrollable-element-keyboard-accessible-0ssw9k/
ref: /standards-guidelines/act/rules/scrollable-element-keyboard-accessible-0ssw9k/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/scrollable-element-keyboard-accessible-0ssw9k.md
# footer: > # Text in footer in HTML
#   <p> This is the text in the footer </p>
---

{% include_relative _proposed-banner.html %}

Rule Type:
:   atomic

Rule ID:
:   0ssw9k

Last Modified:
:   June 3, 2021

Accessibility Requirements Mapping:
:   [2.1.1 Keyboard (Level A)](https://www.w3.org/TR/WCAG21/#keyboard)
    - **Required for conformance** to WCAG 2.0 and later on level A and higher
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion needs further testing
        - An `inapplicable` outcome: success criterion needs further testing
:   [2.1.3 Keyboard (No Exception) (Level AAA)](https://www.w3.org/TR/WCAG21/#keyboard-no-exception)
    - **Required for conformance** to WCAG 2.0 and later on level AAA
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion needs further testing
        - An `inapplicable` outcome: success criterion needs further testing
:   [G202: Ensuring keyboard control for all functionality](https://www.w3.org/WAI/WCAG21/Techniques/general/G202)
    - Not required to conformance to any W3C accessibility recommendation.
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: technique is not satisfied
        - All `passed` outcomes: technique needs further testing
        - An `inapplicable` outcome: technique needs further testing

Input Aspects:
:   [DOM Tree](https://www.w3.org/TR/act-rules-aspects/#input-aspects-dom)
:   [CSS Styling](https://www.w3.org/TR/act-rules-aspects/#input-aspects-css)

## Description

This rule checks that scrollable elements can be scrolled by keyboard

## Applicability

This rule applies to any HTML element that has [visible][] [children][] in the [flat tree][] for which one of the following is true:

- It has a [horizontal scroll distance][scrollable] greater than the [computed][] [left][padding-left] or [right padding][padding-right] of the element; or
- It has a [vertical scroll distance][scrollable] greater than the [computed][] [top][padding-top] or [bottom padding][padding-bottom] of the element

## Expectation

Each test target is either included in [sequential focus navigation][] or has a [descendant][] in the [flat tree][] that is included in [sequential focus navigation][].

## Assumptions

This rule assumes that all [scrollable elements][scrollable] with visible content need to be keyboard accessible. [Scrollable elements][scrollable] that do not need to be keyboard accessible, perhaps because their content is [purely decorative][] or because scroll can be controlled in some other keyboard accessible way such as through a button or custom scrollbar, may fail this rule but still satisfy [success criterion 2.1.1 Keyboard][].

## Accessibility Support

Some browsers will automatically make any [scrollable element][scrollable] focusable to ensure keyboard accessibility. However, the browser does not include these elements in [sequential focus navigation][] when it has a negative number as a tabindex [attribute value][].

## Background

To ensure there is some element from which arrow keys can be used to control the scroll position, focus must be on or in a scrollable region. If scripts are used to prevent the keyboard events from reaching the scrollable region, this could still cause a keyboard accessibility issue. This must be tested separately.

- [Understanding Success Criterion 2.1.1: Keyboard](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html)
- [G202: Ensuring keyboard control for all functionality](https://www.w3.org/WAI/WCAG21/Techniques/general/G202)

## Test Cases

### Passed

#### Passed Example 1

This [scrollable][] `section` element is included in [sequential focus navigation][] because it has a `tabindex` attribute set to `0`.

```html
<section style="height: 100px; width: 500px; overflow: scroll;" tabindex="0">
	<h1>WCAG 2.1 Abstract</h1>
	<p>
		Web Content Accessibility Guidelines (WCAG) 2.1 covers a wide range of recommendations for making Web content more
		accessible. Following these guidelines will make content more accessible to a wider range of people with
		disabilities, including accommodations for blindness and low vision, deafness and hearing loss, limited movement,
		speech disabilities, photosensitivity, and combinations of these, and some accommodation for learning disabilities
		and cognitive limitations; but will not address every user need for people with these disabilities. These guidelines
		address accessibility of web content on desktops, laptops, tablets, and mobile devices. Following these guidelines
		will also often make Web content more usable to users in general.
	</p>
</section>
```

#### Passed Example 2

This [scrollable][] `section` element contains a link that is included in [sequential focus navigation][].

```html
<section style="height: 100px; width: 500px; overflow: scroll;">
	<h1>
		<a href="https://www.w3.org/TR/WCAG21/#abstract">
			WCAG 2.1 Abstract
		</a>
	</h1>
	<p>
		Web Content Accessibility Guidelines (WCAG) 2.1 covers a wide range of recommendations for making Web content more
		accessible. Following these guidelines will make content more accessible to a wider range of people with
		disabilities, including accommodations for blindness and low vision, deafness and hearing loss, limited movement,
		speech disabilities, photosensitivity, and combinations of these, and some accommodation for learning disabilities
		and cognitive limitations; but will not address every user need for people with these disabilities. These guidelines
		address accessibility of web content on desktops, laptops, tablets, and mobile devices. Following these guidelines
		will also often make Web content more usable to users in general.
	</p>
</section>
```

### Failed

#### Failed Example 1

This [vertically scrollable][scrollable] `section` element is not included in [sequential focus navigation][], nor does it have any [descendants][descendant] that are.

```html
<section style="height: 100px; width: 500px; overflow-y: scroll">
	<h1>WCAG 2.1 Abstract</h1>
	<p>
		Web Content Accessibility Guidelines (WCAG) 2.1 covers a wide range of recommendations for making Web content more
		accessible. Following these guidelines will make content more accessible to a wider range of people with
		disabilities, including accommodations for blindness and low vision, deafness and hearing loss, limited movement,
		speech disabilities, photosensitivity, and combinations of these, and some accommodation for learning disabilities
		and cognitive limitations; but will not address every user need for people with these disabilities. These guidelines
		address accessibility of web content on desktops, laptops, tablets, and mobile devices. Following these guidelines
		will also often make Web content more usable to users in general.
	</p>
</section>
```

#### Failed Example 2

This [horizontally scrollable][scrollable] `section` element is not included in [sequential focus navigation][], nor does it have any [descendants][descendant] that are.

```html
<style>
	section {
		height: 100px;
		width: 400px;
		overflow-y: auto;
		white-space: nowrap;
	}
	section > img {
		display: inline-block;
		width: 80px;
	}
</style>
<h1>Our sponsors:</h1>
<section>
	<img src="/test-assets/shared/w3c-logo.png" alt="W3C" />
	<img src="/test-assets/shared/eu-logo.svg" alt="EU" />
	<img src="/test-assets/shared/w3c-logo.png" alt="W3C" />
	<img src="/test-assets/shared/eu-logo.svg" alt="EU" />
	<img src="/test-assets/shared/w3c-logo.png" alt="W3C" />
	<img src="/test-assets/shared/eu-logo.svg" alt="EU" />
	<img src="/test-assets/shared/w3c-logo.png" alt="W3C" />
</section>
```

### Inapplicable

#### Inapplicable Example 1

This `section` element has a [computed][] [overflow][] of `visible`.

```html
<section style="height: 95px; width: 500px;">
	<h1>WCAG 2.1 Abstract</h1>
	<p>
		Web Content Accessibility Guidelines (WCAG) 2.1 covers a wide range of recommendations for making Web content more
		accessible. Following these guidelines will make content more accessible to a wider range of people with
		disabilities, including accommodations for blindness and low vision, deafness and hearing loss, limited movement,
		speech disabilities, photosensitivity, and combinations of these, and some accommodation for learning disabilities
		and cognitive limitations; but will not address every user need for people with these disabilities. These guidelines
		address accessibility of web content on desktops, laptops, tablets, and mobile devices. Following these guidelines
		will also often make Web content more usable to users in general.
	</p>
</section>
```

#### Inapplicable Example 2

This `section` element has a [scroll distance][scrollable] of 0 in both directions.

```html
<section style="height: 95px; width: 500px; overflow: auto;">
	<p>
		<a href="https://www.w3.org/TR/WCAG21/#abstract">
			WCAG 2.1 Abstract
		</a>
	</p>
</section>
```

#### Inapplicable Example 3

This `section` element is not [scrollable][] because it has a [computed][] [overflow][] of `hidden`.

```html
<h1>
	<a href="https://www.w3.org/TR/WCAG21/#abstract">
		WCAG 2.1 Abstract
	</a>
</h1>
<section style="height: 95px; width: 500px; overflow: hidden;">
	<p>
		Web Content Accessibility Guidelines (WCAG) 2.1 covers a wide range of recommendations for making Web content more
		accessible. Following these guidelines will make content more accessible to a wider range of people with
		disabilities, including accommodations for blindness and low vision, deafness and hearing loss, limited movement,
		speech disabilities, photosensitivity, and combinations of these, and some accommodation for learning disabilities
		and cognitive limitations; but will not address every user need for people with these disabilities. These guidelines
		address accessibility of web content on desktops, laptops, tablets, and mobile devices. Following these guidelines
		will also often make Web content more usable to users in general.
	</p>
</section>
```

#### Inapplicable Example 4

This [scrollable][] `section` element has no [visible][] content.

```html
<p>This is what a scrollbar looks like:</p>
<section style="height: 20px; width: 500px; overflow-x:scroll;">
	<div style="width: 1000px; height: 1px;"></div>
</section>
```

#### Inapplicable Example 5

This `section` element has a [horizontal scroll distance][scrollable] that is less than its horizontal [padding][], and [vertical scroll distance][scrollable] that is less than its vertical [padding][].

```html
<section style="height: 210px; width: 500px; overflow: scroll; padding: 30px;">
	<div role="heading" aria-level="1">WCAG 2.1 Abstract</div>
	<div style="width: 520px">
		Web Content Accessibility Guidelines (WCAG) 2.1 covers a wide range of recommendations for making Web content more
		accessible. Following these guidelines will make content more accessible to a wider range of people with
		disabilities, including accommodations for blindness and low vision, deafness and hearing loss, limited movement,
		speech disabilities, photosensitivity, and combinations of these, and some accommodation for learning disabilities
		and cognitive limitations; but will not address every user need for people with these disabilities. These guidelines
		address accessibility of web content on desktops, laptops, tablets, and mobile devices. Following these guidelines
		will also often make Web content more usable to users in general.
	</div>
</section>
```

#### Inapplicable Example 6

This `iframe` element is not a [scrollable element][scrollable].

```html
<iframe src="https://www.w3.org/TR/WCAG21/#abstract" width="500" height="200"></iframe>
```

## Glossary

{% include_relative glossary/attribute-value.md %}
{% include_relative glossary/outcome.md %}
{% include_relative glossary/scrollable-element.md %}
{% include_relative glossary/visible.md %}

## Acknowledgements

This rule was written in the [ACT Rules community group](https://w3.org/community/act-r/), 
with the support of the EU-funded [WAI-Tools Project](https://www.w3.org/WAI/about/projects/wai-tools/).

### Authors

- [Wilco Fiers](https://github.com/wilcofiers)

## Changelog

This is the first version of this ACT rule.

[visible]: #visible
[scrollable]: #scrollable-element
[attribute value]: #attribute-value
[children]: https://dom.spec.whatwg.org/#concept-tree-child 'DOM child, 2020/04/03'
[descendant]: https://dom.spec.whatwg.org/#concept-tree-descendant 'DOM descendant, 2020/04/03'
[sequential focus navigation]: https://html.spec.whatwg.org/multipage/interaction.html#sequential-focus-navigation 'HTML sequential focus navigation, 2020/04/03'
[flat tree]: https://drafts.csswg.org/css-scoping/#flat-tree 'CSS draft, flat tree, 2020/04/03'
[computed]: https://www.w3.org/TR/css-cascade-3/#computed-value
[overflow]: https://www.w3.org/TR/CSS22/visufx.html#overflow
[padding]: https://www.w3.org/TR/CSS22/box.html#propdef-padding
[padding-left]: https://www.w3.org/TR/CSS22/box.html#propdef-padding-left
[padding-right]: https://www.w3.org/TR/CSS22/box.html#propdef-padding-right
[padding-top]: https://www.w3.org/TR/CSS22/box.html#propdef-padding-top
[padding-bottom]: https://www.w3.org/TR/CSS22/box.html#propdef-padding-bottom
[purely decorative]: https://www.w3.org/TR/WCAG21/#dfn-pure-decoration
[success criterion 2.1.1 keyboard]: https://www.w3.org/TR/WCAG21/#keyboard
