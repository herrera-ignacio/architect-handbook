# Accessibility testing

- [Accessibility testing](#accessibility-testing)
  - [WCAG and good practices](#wcag-and-good-practices)
  - [Automated tools](#automated-tools)
    - [Browser/HTML](#browserhtml)
    - [JavaScript](#javascript)
    - [Code style - ESlint](#code-style---eslint)
      - [Code style - Example 1](#code-style---example-1)
      - [Code style - Example 2](#code-style---example-2)
    - [Storybook - Accessibility plugin](#storybook---accessibility-plugin)
    - [Unit testing - jest-axe](#unit-testing---jest-axe)
  - [Manual testing](#manual-testing)
    - [Testing with assistive technologies](#testing-with-assistive-technologies)
      - [Screen readers](#screen-readers)
      - [Screen magnifiers](#screen-magnifiers)
      - [Speech recognition](#speech-recognition)

## WCAG and good practices

The __Web Content Accessibility Guidelines (WCAG)__ are part of a series of web accessibility guidelines published by the [Web Accessibility Initiative (WAI)](https://en.wikipedia.org/wiki/Web_Accessibility_Initiative) of the [World Wide Web Consortium (W3C)](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium). WCAG 2.1 became a W3C Recommendation in 2018.

- [Industry standards - good practices](https://github.com/dequelabs/axe-core/blob/develop/doc/rule-descriptions.md#best-practices-rules).
- [WCAG 2.0 A & AA checks](https://github.com/dequelabs/axe-core/blob/develop/doc/rule-descriptions.md#wcag-20-level-a--aa-rules).
- [WCAG 2.1 A & AA checks](https://github.com/dequelabs/axe-core/blob/develop/doc/rule-descriptions.md#wcag-21-level-a--aa-rules).

## Automated tools

While GDS Accessibility team found that [a large proportion of issues are not found by automated testing](https://accessibility.blog.gov.uk/2017/02/24/what-we-found-when-we-tested-tools-on-the-worlds-least-accessible-webpage/), it can help to __establish a baseline__ with virtually no effort no include and run.

> It’s a well-known statement that __automated testing does not make your app fully accessible__. You still do need to __test the interface with assistive technologies__ such as VoiceOver or NVDA.

### Browser/HTML

- [Tenon](https://tenon.io/).
- [HTML_CodeSniffer](http://squizlabs.github.io/HTML_CodeSniffer/).
- [Google accessibility developer tools (deprectaed)](https://github.com/GoogleChrome/accessibility-developer-tools)
- [Web AIM color contrast checker](https://webaim.org/resources/contrastchecker/)
- [Google Lighthouse accessibility audit](https://developer.chrome.com/docs/lighthouse/accessibility/).

It's important that teams don't rely on them heaviliy. No tool will be able to pick up every accessibility barrier and even if they do, sometimes the results they give will be inconclusive or require further investigation.

### JavaScript

There are many tools that can help React developers to test accessibility in their code.

- [axe-core](https://github.com/dequelabs/axe-core): Test the accessibility of the rendered DOM and highlight accessibility issues.
- [jest-axe](https://www.npmjs.com/package/jest-axe): Custom Jest matcher for axe testing accessibility.
- [eslint-plugin-jsx-a11y](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y): Runs a static analysis of the JSX.
- [cypress-axe](https://github.com/component-driven/cypress-axe): axe support for Cypress E2E.
- [axe-testcafe](https://www.npmjs.com/package/axe-testcafe) and [@testcafe-community/axe](https://www.npmjs.com/package/@testcafe-community/axe): axe support for TestCafe E2E.

### Code style - ESlint

Code style will give us useful insights such as the following examples found in live code.

#### Code style - Example 1

Consider the following code:

```html
<a role="link" aria-label="custom-link">
  {children}
</a>
```

Default rules will warn us about:

```txt
1:3 error  The href attribute is required for an anchor to be keyboard accessible. Provide a valid, navigable address as the href value. If you cannot provide an href, but still need the element to resemble a link, use a button and change it with appropriate styles. Learn more:    jsx-a11y/anchor-is-valid
```

This can be fixed with the following refactor:

```html
<a role="button" aria-label="custom-link">
  {children}
</a>
```

#### Code style - Example 2

Consider the following code:

```tsx
export const LinkHandler: React.FC<LinkHandlerProps> = ({
  children,
  link,
  ...props
}) => {
  const onClick = (e: React.MouseEvent<HTMLDivElement>): void => {
    if (link) {
      if (e.metaKey) {
        window.open(link);
        return;
      }
      window.location.href = link;
    }
  };
  return (
    <div onClick={onClick} {...props}>
      {children}
    </div>
  );
};
```

Default rules will warn us about:

```txt
16:5 error  Visible, non-interactive elements with click handlers must have at least one keyboard listener jsx-a11y/click-events-have-key-events

16:5 error  Avoid non-native interactive elements. If using native HTML is not possible, add an appropriate role and support for tabbing, mouse, keyboard, and touch inputs to an interactive content element  jsx-a11y/no-static-element-interactions
```

This can be fixed with the following refactor:

```tsx
export const LinkHandler: React.FC<LinkHandlerProps> = ({
  children,
  link,
  ...props
}) => {
  const onClick = (e: React.MouseEvent<HTMLDivElement>): void => {
    if (link) {
      if (e.metaKey) {
        window.open(link);
        return;
      }
      window.location.href = link;
    }
  };

  const onKeyDown = (): void => {
    if (link) {
      window.location.href = link;
    }
  };

  return (
    <div
      onClick={onClick}
      {...props}
      onKeyPress={onKeyDown}
      role="link"
      tabIndex={0}
    >
      {children}
    </div>
  );
};
```

### Storybook - Accessibility plugin

You can test your components in storybook by using [addon-a11y](https://storybook.js.org/addons/@storybook/addon-a11y).

A new tab “Accessibility” will be added to your components' stories. You can see “Violations”, “Passes” and “Incomplete” checks.

### Unit testing - jest-axe

[jest-axe](https://www.npmjs.com/package/jest-axe) provides a custom Jest matcher for axe. It should provide support for unit testing a good amount of accessibility rules.

Using the assertions provided with jest-axe in combination with the storybook accessibility plugin provides a robust mechanisms for defining and validating a baseline of accessibility good practices.

For example, it might warn us about violations such as:

```txt
"Form elements should have a visible label (label-title-only)"

Fix all of the following:
  Only title used to generate label for form element
```

## Manual testing

> More information here: [gov.uk case study](https://accessibility.blog.gov.uk/2017/02/24/what-we-found-when-we-tested-tools-on-the-worlds-least-accessible-webpage/).

There's a large number of accessibility barriers that won't be detected by automated testing. Therefore, it is advised to combine automated tool testing with __manual checking, an accessibility audit, and user testing__.

### Testing with assistive technologies

> More information here: [Gov.uk, testing with asssistive technologies](https://www.gov.uk/service-manual/technology/testing-with-assistive-technologies#when-to-test).

Your service should work with a combination of assistive technologies and browsers. You can base your testing on some public available surveys like [WebAIM screen reader survey](https://webaim.org/projects/screenreadersurvey9/) or make your own accessibility audit.

Recommended combinations are:

- JAWS (desktop screen reader) + Chrome or Edge (latest).
- NVDA (desktop screen reader) + Chrome or Edge (latest).
- VoiceOver on iOS (mobile screen reader) + Safari (12 or later).
- TalkBaclk (mobile screen reader) + Chrome (latest).
- Windows Magnifier or Apple Zoom (screen magnifiers) + Any browser (latest).
- Dragon (speech recognition) - Chrome (latest).
- Windows high contrast mode - Any browser (latest).

#### Screen readers

You should be able to:

- Read every element and header.
- Tab through every link.
- Checke very landmark, for example footer and any navigation.
- Check use of Accessible Rich Internet Applicatios (ARIA).
- Fill in any editable fields.

#### Screen magnifiers

Test up to at least 4 times magnification:

- Spacing between elements.
- Page elements display consistently on different page layouts.
- Users know when something happens outside the viewport.

#### Speech recognition

You should be able to:

- Navigate to each feature.
- Activate every link, button, or interactive element.
- Fill in any editable fields.
