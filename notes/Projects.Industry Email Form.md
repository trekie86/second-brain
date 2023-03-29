---
id: 8jrob1dsv6kafiswbtlqapy
title: Industry Email Form
desc: ''
updated: 1676591252674
created: 1675880537728
---

See [[Word Press.custom form]] for details on how to do it.

Content in the template to render the form to the user
```php
<?php /* Template Name: IndustryForm */ ?>
	
	<?php get_header(); ?>
	
	<div id="primary" class="content-area">
		<main id="main" class="site-main" role="main">
			<?php
			// Start the loop.
			while ( have_posts() ) : the_post();
				// Include the page content template.
				get_template_part( 'content', 'page' );
				// End of the loop.
			endwhile;
			?>	
		</main><!-- .site-main -->
    <form action="#" method="POST">
    <?php wp_nonce_field('provide-industry-email', 'industry-email-validation'); ?>
    <div>
        <label for="email">Enter your email address:</label>
        <input id="email" type="email" name="email" />

        <input id="submit" type="submit" name="industry-email-form" value="Submit" />
    </div>
	</form>
    <?php if ( isset( $_GET['error'] ) ) {
		print('<div class="error"><p>"Something went wrong, please try again."</p></div>');
	} ?>
	</div><!-- .content-area -->
	<?php get_sidebar(); ?>
	<?php get_footer(); ?>

```

Now lets process the form request

```php
function process_industry_email() {
	if ( ! isset( $_POST['industry-email-form'] ) || ! isset( $_POST['industry-email-validation'] ) )  {
		return;
	}
    if ( ! wp_verify_nonce( $_POST['industry-email-validation'], 'provide-industry-email' ) ) {
		return;
	}
	if ( ! isset( $_POST['email'] ) ) {
		return;	
	}
	$url = wp_get_referer();
	$email = $_POST['email'];
    #echo("Received email address " . $email);
	$current_restricted_email = pmpro_getOption("level_13_restrict_emails");
	$cleaned_restricted_email = str_replace("\"", "&quot;", stripslashes($current_restricted_email));
	$cleaned_restricted_email = $current_restricted_email . "\r\n" . $email;
	if(pmpro_setOption("level_13_restrict_emails", $cleaned_restricted_email)) {
		$url = "/membership-account/membership-checkout?level=13";
	} else {
		$url = add_query_arg( 'error', "failure", wp_get_referer() );
	}
	
	// Redirect user back to the form, with an error or success marker in $_GET.
	wp_safe_redirect( $url );
	exit();
}
add_action( 'template_redirect', 'process_industry_email' );
```