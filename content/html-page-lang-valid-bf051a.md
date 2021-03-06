---
title: "HTML page language is valid"
permalink: /standards-guidelines/act/rules/html-page-lang-valid-bf051a/
ref: /standards-guidelines/act/rules/html-page-lang-valid-bf051a/
lang: en
github:
  repository: w3c/wcag-act-rules
  path: content/html-page-lang-valid-bf051a.md
---

Rule Type:
:   atomic

Rule ID:
:   bf051a

Last modified:
:   March 5, 2020

Accessibility Requirements Mapping
:   [3.1.1 Language of Page (Level A)](https://www.w3.org/TR/WCAG21/#language-of-page)
    - **Required for conformance** to WCAG 2.0 and above on level A and above
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: success criterion is not satisfied
        - All `passed` outcomes: success criterion needs further testing
        - An `inapplicable` outcome: success criterion needs further testing
:   [H57: Using the language attribute on the HTML element](https://www.w3.org/WAI/WCAG21/Techniques/html/H57)
    - **Required for conformance** to WCAG 2.0 and above on level A and above
    - [Outcome](#outcome) mapping:
        - Any `failed` outcomes: technique is not satisfied
        - All `passed` outcomes: technique needs further testing
        - An `inapplicable` outcome: technique needs further testing

Input Aspects
: [DOM Tree](https://www.w3.org/TR/act-rules-aspects/#input-aspects-dom)

## Description

This rule checks that the `lang` attribute of the root element of an HTML page has a valid primary language subtag.

## Applicability

This rule applies to any [document element](https://dom.spec.whatwg.org/#document-element) if it is an `html` element that:

- has a `lang` attribute that is neither empty ("") nor only [ASCII whitespace](https://infra.spec.whatwg.org/#ascii-whitespace); and
- is in a [top-level browsing context](https://html.spec.whatwg.org/#top-level-browsing-context); and
- has a [node document](https://dom.spec.whatwg.org/#concept-node-document) with a [content type](https://dom.spec.whatwg.org/#concept-document-content-type) of `text/html`.

**Note:** `html` elements within `iframe` and `object` elements are not applicable as `iframe` and `object` elements create [nested browsing contexts](https://html.spec.whatwg.org/#nested-browsing-context). These elements can embed any third party content, making testing difficult. As these elements are meant to provide a layer of isolation, the language of the [parent browsing context](https://html.spec.whatwg.org/#parent-browsing-context) may not be inherited. Thus, embedded documents with an invalid `lang` attribute can cause accessibility issues. This should be tested separately.

## Expectation

For each test target, the `lang` attribute has a [valid language subtag][].

## Assumptions

- The language of the page can be set by other methods than the `lang` attribute, for example using HTTP headers or the `meta` element. These methods are not supported by all assistive technologies. This rule assumes that these other methods are insufficient to satisfying [Success Criterion 3.1.1: Language of Page](https://www.w3.org/TR/WCAG21/#language-of-page).

- This rule assumes that user agents and assistive technologies can programmatically determine [valid language subtags](#valid-language-subtag) even if these do not conform to the [BCP 47][] syntax.

- This rule assumes that [grandfathered tags][] are not used as these will not be recognized as [valid language subtags](#valid-language-subtag).

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

This `html` element has a `lang` attribute whose value is a [valid][valid language subtag] [primary language subtag][].

```html
<html lang="fr"></html>
```

#### Passed Example 2

This `html` element has a `lang` attribute value that is a [valid language subtag][] even though the [region subtag][] is not.

```html
<html lang="en-US-GB"></html>
```

### Failed

#### Failed Example 1

This `html` element has a `lang` attribute whose value is not a [valid language subtag][].

```html
<html lang="em-US"></html>
```

#### Failed Example 2

This `html` element has a `lang` attribute whose value is not a [valid language subtag][].

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

### Outcome

A conclusion that comes from evaluating an ACT Rule on a [test subject](https://www.w3.org/TR/act-rules-format/#test-subject) or one of its constituent [test target](https://www.w3.org/TR/act-rules-format/#test-target). An outcome can be one of the three following types:

- **Inapplicable:** No part of the test subject matches the applicability
- **Passed:** A [test target](https://www.w3.org/TR/act-rules-format/#test-target) meets all expectations
- **Failed:** A [test target](https://www.w3.org/TR/act-rules-format/#test-target) does not meet all expectations

**Note:** A rule has one `passed` or `failed` outcome for every [test target](https://www.w3.org/TR/act-rules-format/#test-target). When there are no test targets the rule has one inapplicable outcome. This means that each [test subject](https://www.w3.org/TR/act-rules-format/#test-subject) will have one or more outcomes.

**Note:** Implementers using the [EARL10-Schema](https://www.w3.org/TR/EARL10-Schema/) can express the outcome with the [outcome property](https://www.w3.org/TR/EARL10-Schema/#outcome). In addition to `passed`, `failed` and `inapplicable`, EARL 1.0 also defined an `incomplete` outcome. While this cannot be the outcome of an ACT Rule when applied in its entirety, it often happens that rules are only partially evaluated. For example, when applicability was automated, but the expectations have to be evaluated manually. Such "interim" results can be expressed with the incomplete outcome.

### Valid Language Subtag

A language tag consists of a [primary language subtag][] from the [language subtag registry][], optionally followed by a hyphen (`-`) and any sequence of characters.

_Note:_ This definition intentionally differs from the [BCP 47][] syntax as user agents and assistive technologies are more lenient in what they accept. The definition is however consistent with the behavior of the `:lang()` pseudo-selector as defined by [Selectors Level 3][]. For example, `de-hello` would be an accepted way to indicate German in current user agents and assistive technologies, despite not being valid according to [BCP 47][]. As a consequence of this definition, however, [grandfathered tags][] are not correctly recognized as valid language subtags.

## Acknowledgements

### Authors

- [Jey Nandakumar](https://github.com/jkodu)

### Previous Authors

- [Annika Nietzio](https://github.com/annika-FTB)

[primary language subtag]: https://tools.ietf.org/html/bcp47#section-2.2.1 'Definition of primary language subtag'
[region subtag]: https://tools.ietf.org/html/bcp47#section-2.2.4 'Definition of region subtag'
[valid language subtag]: #valid-language-subtag 'Definition of valid language subtag'
[grandfathered tags]: https://tools.ietf.org/html/bcp47#section-2.2.8
[bcp 47]: https://tools.ietf.org/html/bcp47#section-2.1
[language subtag registry]: http://www.iana.org/assignments/language-subtag-registry/language-subtag-registry
[selectors level 3]: https://drafts.csswg.org/selectors-3/#lang-pseudo
