# API quality

Add a quality rate on apis according to criteria:

- markdown documentation exists and is published
- swagger documentation exists and is published
- a health-check is set
- the description contains has a minimum length
- the default logo is not used
- views and labels are set on the API

The idea is to invite API publisher to configure all non mandatory fields according to the admin rules.
A percentage rate will be calculated according to these rules and their weights.


## Manual quality rules

This will allow for a reviewer to validate the quality of the APIs according to some rules defined manually.
These rules are attached to a weight to process the final quality rate.
