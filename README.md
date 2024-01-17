# GDS - Twigged

GDS - Twigged is a collection of [Gov UK Design System](https://design-system.service.gov.uk/components/) components, converted into Twig templates. These templates are intended to be easily dropped into any project that uses Twig, making it simple to integrate Gov UK Design System components into your web applications.

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

## Getting Started

There's not much to this repo as it's intended to compliment an existing Twig project such as [DockPress](https://github.com/ufmedia/DockPress) (shameless plug), as such it's easier to download the [latest release](https://github.com/ufmedia/GDS-Twigged/releases/latest) and extract the twig files to where they're needed. Of course you can clone the repo if you prefer, just rember to remove the remote or scrub the .git dir.

