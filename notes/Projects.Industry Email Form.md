---
id: 8jrob1dsv6kafiswbtlqapy
title: Industry Email Form
desc: ''
updated: 1675880572862
created: 1675880537728
---

See [[Word Press.custom form]] for details on how to do it.

Content in the template to render the form to the user
```php
<?php
<form action="#" method="POST">
    <?php wp_nonce_field('provide-industry-email', 'industry-email-validation'); ?>
    <div>
        <label for="email">Enter your email address:</label>
        <input id="email" type="email" name="email" />

        <input id="submit" type="submit" name="industry-email-form" value="Submit" />
    </div>
</form>

```

Now lets process the form request

```php
<?php 
function process_industry_email() {
    if ( ! isset( $_POST['industry-email-form'] ) || ! isset( $_POST['industry-email-validation'] ) )  {
		return;
	}

    if ( ! wp_verify_nonce( $_POST['industry-email-validation'], 'provide-industry-email' ) ) {
		return;
	}

    # do the stuff to submit the content
}
add_action( 'template_redirect', 'process_industry_email' );
```