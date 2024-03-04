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

There's not much to this repo as it's intended to compliment an existing Twig project such as [DokPress](https://github.com/ufmedia/DokPress) (shameless plug), as such it's easier to download the [latest release](https://github.com/ufmedia/GDS-Twigged/releases/latest) and extract the twig files to where they're needed. Of course you can clone the repo if you prefer, just rember to remove the remote or scrub the .git dir.

<strong>Don't forget to [include the GDS javascript and css](https://frontend.design-system.service.gov.uk/installing-with-npm/#requirements) in your project.</strong>

## Example Configuration

There are a few hoops to jump through to get the GDS front end working on WordPress. We'll go through the process assuming you're using the DokPress theme included within this project, however this should work for most themes.

Firstly, from within the theme folder, install the GDS front end.

```
npm install govuk-frontend --save
```

Next, include the sass within your SASS index file **(public/src/scss/style.scss)**.
```
@import "~govuk-frontend/dist/govuk/all";
```

Now import and initialise the JS within your javascript index file **(public/src/js/index.js)**.
```
import { initAll } from 'govuk-frontend';
initAll()
```

Now copy the **assets** folder from your node_modules folder into your theme root.

Assuming you're within the root of your theme, you'd run something like:
```
cp -r node_modules/govuk-frontend/dist/govuk/assets ./
```
<sup>This is something that would ideally be automated during deployment to ensure the latest assets are used.</sup>

Finally, we need to add the **govuk-frontend-supported** to our body class and ensure that our JS is loaded with the type="module" attribute. To do this we can add two new methods to the Init class **(includes/class-init.php)**.

Firstly add these two links to the existing constructor:

```
add_filter( 'script_loader_tag', array( $this, 'add_type_to_script' ), 10, 3 );
add_filter( 'body_class', array( $this, 'add_gds_body_class' ), 10, 1 );
```

Then we add the two additional methods to the class:

```
/**
* Add type module to main JS
*
* @param string $tag
* @param string $handle
* @param string $source
* @return string
*/
public function add_type_to_script( $tag, $handle, $source ) {
  if ( 'timberpress-scripts' === $handle ) {
    $tag = '<script type="module" src="' . esc_url( $source ) . '" id="timberpress-scripts-js" ></script>';
  }
  return $tag;
}

/**
* Add the GovUK body class.
*
* @param array $classes
* @return array
*/
public function add_gds_body_class( $classes ) {
  $classes[] = 'govuk-frontend-supported';
  return $classes;
}
```
