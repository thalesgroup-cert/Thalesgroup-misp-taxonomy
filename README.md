This taxonomy was designed with the aim of enabling desired sharing and preventing unwanted sharing between Thales Group security communities.
---
# Install the Thales Group Taxonomy

The Thales Group Official taxonomy is now **installed by default** in **MISP v2.4.146**.
For versions prior to v2.4.146, please install the taxonomy as described in the [here](#required-for-versions-prior-to-v24146-install-from-scratch).

## [MANDATORY] Activate the taxonomy
- Doucle click on the **thales_group taxonomy**
- Click on **(enable)**
- Go back to `taxonomies/index`
- Click on **(enable all)**
- Check **Required** checkbox (required for Event publication):
  - When publishing an Event, you will be required to use at least one TAG from the Thales Group taxonomy.

We also recommend to activate the **TLP Taxonomy**.

## [MANDATORY] Filter Event publication using the taxonomy 
Go to MISP Web GUI `/servers/index` and click on `Edit icon` on the **MISP Thales Group Internal Server**.

Then, modify the **Push rules**:
  - Add to **Blocked Tags (AND NOT)**:
    - `thales_group:tlp:black`
    - `tlp:red`
    - `thales_group:distribution="team_eyes_only"`
  - Add to **Allowed tags (OR)**:
    -  `thales_group:distribution="limited_distribution"`
    -  `thales_group:distribution="external_alliances"`
    -  `thales_group:distribution="customers"`
    -  `thales_group:minarm`
    -  `thales_group:acn`
    -  `thales_group:sigpart`
    -  `thales_group:to_block`

## [Required for versions prior to v2.4.146] Install from scratch

    cd /var/www/MISP/app/files/taxonomies/
    mkdir thales-group
    cd thales-group
    
Copy the [`thales-group/machinetag.json`](https://github.com/MISP/misp-taxonomies/blob/main/thales_group/machinetag.json) file:

    curl https://raw.githubusercontent.com/MISP/misp-taxonomies/main/thales_group/machinetag.json -o machinetag.json

Go to MISP Web GUI `taxonomies/index` and click on **Update Taxonomies**. The newly created taxonomy should be visible. 

# Usage
When using this Taxonomy, first, you need to be the more restrictive possible. Then, allow the sharing to the Thales Group Community or to specific entities.

Example:

When creating an Event: 
- Put the `Event Distribution` to `Your organisation only` 
- Select the TAG `thales_group:distribution="team_eyes_only"` from the Thales Group Taxonomy.

When you want to **share** the Event to the **Thales Group Community ONLY**:
  - Put the `Event Distribution` to `All communities` 
  - Remove the TAG `thales_group:distribution="team_eyes_only"`
  - Select the TAG `thales_group:distribution="limited_distribution"`
  - Publish the Event
