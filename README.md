# pigs
Private Instagram Scraper

An admittedly creeperesque proof-of-concept that private Instagram pages weren't truly private as of a couple of months ago. The loophole has since been patched.

Prior to the patch, if one knew the shortcode (http://instagram.com/p/[SHORTCODE]), one could query Instagram's API (without an API key, even) for the direct link to the image, which still allows access to private images to this day. The query to the API with a shortcode of a private image no longer works.

Technically, knowing which shortcodes belong to images is a hard problem, since as the length of shortcodes increases, so does the sparsity of images embedded in that shortcode space. For example, even a mere 6-digit shortcode comprised of upper- and lowercase letters and digits has 62^6 = 56,800,235,584 possibilities. Since pictures on instagram now contain 10 characters, brute forcing the entire space of shortcodes would be laughably intractable. 

Fortunately, the way Instagram generates shortcodes for images is publicly known (details here: http://instagram-engineering.tumblr.com/post/10853187575/sharding-ids-at-instagram), which gives one a decent lower bound on the probability of finding an image at any given shortcode. 






