---
title: "Element with presentational children has no focusable content"
permalink: /standards-guidelines/act/rules/presentational-children-no-focusable-content-307n5z/
ref: /standards-guidelines/act/rules/presentational-children-no-focusable-content-307n5z/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/presentational-children-no-focusable-content-307n5z.md
# footer: > # Text in footer in HTML
#   <p> This is the text in the footer </p>
---

{% include_relative _proposed-banner.html %}

Rule Type:
:   atomic

Rule ID:
:   307n5z

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

Input Aspects:
:   [DOM Tree](https://www.w3.org/TR/act-rules-aspects/#input-aspects-dom)
:   [CSS Styling](https://www.w3.org/TR/act-rules-aspects/#input-aspects-css)

## Description

This rule checks that elements with a role that makes its children presentational do not contain focusable elements.

## Applicability

This rule applies to any HTML or SVG element with a [semantic role][] that defines its [children][child] to be [presentational children][].

## Expectation

None of the target elements have [descendants][] in the [flat tree][] that are part of [sequential focus navigation][].

## Assumptions

This rule assumes that elements that are part of [sequential focus navigation][] do not immediately blur, or move focus to another element. Such elements will fail this rule, but may still satisfy success criteria 1.3.1 and 4.1.2.

## Accessibility Support

Several major browsers ignore the WAI-ARIA requirements on [presentational children][] for most or sometimes all roles. Because some browsers do, and others do not implement presentational children, there can be significant differences between browsers.

## Background

This rule applies to elements with a [semantic role][] that defines its [children][child] to be [presentational children][]. This includes the following: `button`, `checkbox`, `img`, `math`, `menuitemcheckbox`, `menuitemradio`, `option`, `progressbar`, `radio`, `scrollbar`, `separator`, `slider`, `switch`, and `tab`.

Elements with a [semantic role][] that has [presentational children][] will not have any descendants in the accessibility tree. If any of those descendants are included in [sequential focus navigation][], this causes the focus to land on an element that has no corresponding node in the [accessibility tree][]. The result is that there is no programmatic name or role available for assistive technologies. There are other problems that can come from [presentational children][] too. These must be tested separately.

- [Understanding Success Criterion 1.3.1: Info and Relationships](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships)
- [Understanding Success Criterion 4.1.2: Name, Role, Value](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value)
- [WAI-ARIA 1.1 Presentational Children][presentational children]

## Test Cases

### Passed

#### Passed Example 1

None of these `button` elements has [descendants][] that are included in [sequential focus navigation][].

```html
<button>Save</button> <button aria-label="save options" aria-expanded="false">▼</button>
```

#### Passed Example 2

This element with `checkbox` role has no [descendants][] that are included in [sequential focus navigation][]. Instead the link to the terms of service is adjacent, and `aria-labelledby` is used to provide its [accessible name][].

```html
<p id="terms">
	<span role="checkbox" aria-checked="false" tabindex="0" aria-labelledby="terms">
		I agree to the
	</span>
	<a href="/terms">terms of service</a>
</p>
```

#### Passed Example 3

This element with `menuitemcheckbox` role has an `input` element as a descendant. Because the `input` is disabled it is not included in [sequential focus navigation][].

**Note**: The `input` checkbox has a `role` [attribute value][] of `none` to ensure it is ignored by browsers that do not support [presentational children][].

```html
<ul role="menu">
	<li role="menuitemcheckbox" aria-checked="true">
		<input type="checkbox" role="none" disabled checked />
		Sort by Last Modified
	</li>
</ul>
```

### Failed

#### Failed Example 1

This `button` element has a [child][] `span` element. Because the `span` element has a `tabindex` attribute with value of `0`, it is included in [sequential focus navigation][].

```html
<button>
	Save
	<span aria-label="save options" aria-expanded="false" tabindex="0">▼</span>
</button>
```

#### Failed Example 2

This element with `checkbox` role has an `a` element as a [child][]. Because the `a` element has an `href` attribute, it is included in [sequential focus navigation][].

```html
<p role="checkbox" aria-checked="false" tabindex="0">I agree to the <a href="/terms">terms of service</a></p>
```

#### Failed Example 3

This element with `menuitemcheckbox` role has a checkbox as a child. Because the checkbox is not disabled, it is included in [sequential focus navigation][].

```html
<ul role="menu">
	<li role="menuitemcheckbox" aria-checked="true">
		<input type="checkbox" checked />
		Sort by Last Modified
	</li>
</ul>
```

### Inapplicable

#### Inapplicable Example 1

This element has a `link` role which does not have [presentational children][].

```html
<a href="https://w3.org">W3C Website</a>
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

- [Wilco Fiers](https://github.com/wilcofiers)

## Changelog

This is the first version of this ACT rule.

[accessible name]: #accessible-name 'Definition of Accessible name'
[attribute value]: #attribute-value 'Definition of Attribute value'
[semantic role]: #semantic-role 'Definition of Semantic role'
[accessibility tree]: https://www.w3.org/TR/accname-1.1/#dfn-accessibility-tree 'Definition of Accessibility tree'
[presentational children]: https://www.w3.org/TR/wai-aria-1.1/#childrenArePresentational 'WAI-ARIA 1.1 Presentational Children'
[child]: https://dom.spec.whatwg.org/#concept-tree-child 'Definition child, as on 2020-10-21'
[descendants]: https://dom.spec.whatwg.org/#concept-tree-descendant 'Definition Descendant, as on 2020-10-21'
[sequential focus navigation]: https://html.spec.whatwg.org/#sequential-focus-navigation 'HTML sequential focus navigation, 2020/10/21'
[flat tree]: https://drafts.csswg.org/css-scoping/#flat-tree 'CSS Scoping definition of Flat tree, working draft'
