---
layout: page
title: Customising with a Cobrand module
---

# Cobrand module

If you need customistation beyond what templates, configuration variables, and
translations can offer, then you will have to have a Cobrand module. These are
automatically loaded according to the current Cobrand and can be found in
`perllib/FixMyStreet/Cobrand/`. There is a default Cobrand (`Default.pm`)
which all Cobrands should inherit from. A Cobrand module can then override any
of the methods from the default Cobrand.

Many of the functions in the Cobrand module are used by FixMyStreet in the UK
to allow the site to offer versions localised to a single authority and should
not be needed for most installs. Listed below are the most useful options that
can be changed:

* geocode_postcode

    This function is used to convert postcodes (zip codes, etc.) entered into a
latitude and longitude, if there's a different way from your geocoder of doing so
(e.g. a MapIt install). If the text passed is not a valid postcode then an
error should be returned. If you do not want to use postcodes, just do not define
this function.

    If the postcode is valid and can be converted then the return value should
look like this:

        return { latitude => $latitude, longitude => $longitude };

    If there is an error it should look like this:

        return { error => $error_message };

* find_closest and find_closest_address_for_rss

    These are used to provide information on the closest street to the point of
the address in reports and RSS feeds or alerts.

* allow_photo_upload

    Return 0 to disable the photo upload field.

* allow_photo_display

    Return 0 to disable the display of uploaded photos.

* remove_redundant_areas

    This is used to filter out any overlapping jurisdictions from MapIt results
where only one of the authorities actually has responsibility for the events
reported by the site. An example would be a report in a city where MapIt
has an ID for the city council and the state council (and they are both the
same MapIt area type) but problems are only reported to the state. In this case
you could remove the ID for the city council from the results.

    With the new bodies handling, a better way to handle this would be to simply
have a body that only covered the state council administrative area.

* short_name

    This is used to turn the full authority name returned by MapIt into a short
name.

