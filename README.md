# GDS - Twigged

GDS - Twigged is a collection of [Gov UK Design System](https://design-system.service.gov.uk/) components, converted into Twig templates. These templates are intended to be easily dropped into any project that uses Twig, making it simple to integrate Gov UK Design System components into your web applications.

## Components

Each component is available as a separate Twig template and can be customized by passing parameters. Here's an example of the Notification Banner component:

```
{% include 'partial/gds/notification-banner.twig' with {
    'title': 'Important',
    'content': 'You have 7 days left to send your application. <a href="#">View application</a>.',
    'role': 'region',
    'aria_labelledby': 'govuk-notification-banner-title'
} %}
```



