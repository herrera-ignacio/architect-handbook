# Backbone OKRs

## Motivation

Lay the foundations for building front-end applications so developers can focus on shipping things faster without compromising on quality.

## Goal

Create a swiss knife of tools, utilities, and configurations governed by clear standards. They can be either used separately or composed together through a common CLI.

## Principles

- Small and autonomous team with an ownership mindset.
- Opinionated toolchain flexible enough to mold it as per product needs.
- Platform as a product & developers as customers.
- Collect feedback often and iterate.
- Educate and empower teams. Write documentation with examples, FAQs, and guidelines.
- Recognize and reward early adopters and external contributors.

## Frontend OKRs

We want to answer how to measure the success of a frontend-core team—finding impact metrics and quantifying dev productivity along with standardization and quality of code.

Frontend OKRs are usually distributed in one of three major areas:

- Performance.
- Delivery.
- Maintainability (i.e., code quality).

### Performance

The performance and health of our web application have a major impact on SEO and user experience.

- Loading time
- Browser support.
- Accessibility.

#### Performance - Example OKRs

- Lighthouse score for desktop.
- Amount of tests for Chrome, Firefox, and Edge.
- Google Page Speed benchmark.
- Static assets size.
- Production-bundle size.
- Amount of components that use lazy loading.
- Amount of components that use pagination.

### Delivery

The frontend backbone has a major impact on how quickly and efficiently we can ship new features.

- Time to market.
- Production outages.

#### Delivery - Example OKRs

- Ticket resolution time.
- PR approval time.
- Sprint velocity.
- Bug fixing time.

### Maintainability (code quality)

Code quality directly impacts both performance and delivery. Better code quality means shipping features faster and safer while delivering a higher quality product with better user experiences.

- Test coverage.
- Reusable code.
- Consistency.
- Development entry barrier.

#### Maintainability - Example OKRs

- Line coverage.
- E2E test cases.
- React components with 100% test coverage.
- React components in self-contained reusable form (e.g., UI library) – new or migrated.
- ESLint errors.
- Documented features.
- Guidelines and FAQs docs.
- Components with variations and inconsistencies.
- New components in PRs (not in UI library).

## Conclusion

Tracking our progress on maintainability and code quality will shift our focus to developers as customers and concentrate on early adopters, getting fast feedback, and iterating. Moreover, as stated above, improving our code quality will have a tangible impact on both the performance and time-to-market of our products.

Therefore, we should evaluate OKRs primarily for Maintainability in the early stages of the UI platform team.

That being said, we should still keep an eye on its impact in shipping new production-ready features.

It is a long way to the top if you want to rock n roll.

### Suggested OKRs

- Increase React components in UI Components Library (i.e., Carrot).
- Decrease React components with variations/inconsistencies in our web application.
- Decrease React components in PRs directly to our web application (i.e., should be in Carrot instead).
- Increase E2E test cases.
- Enforce linting.
- Decrease frontend setup time for new developers.
- Decrease frontend ticket delivery time.
