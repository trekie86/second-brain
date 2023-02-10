---
id: hinbl6z1uphtxivuxr5w6nl
title: options
desc: ''
updated: 1675878523351
created: 1675877999966
---

For retrieving values in the wp_options table
https://developer.wordpress.org/reference/functions/get_option/

For creating a new option, this does not overwrite if one already exists
https://developer.wordpress.org/reference/functions/add_option/

Updating option values, this squashes what is there
https://developer.wordpress.org/reference/functions/update_option/


Overall, if we are interfacing with the PaidMembership Pro plugin, use pmpro_getOption & pmpro_setOption functions.