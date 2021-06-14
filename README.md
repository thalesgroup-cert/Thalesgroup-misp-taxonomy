This taxonomy was designed with the aim of enabling desired sharing and preventing unwanted sharing between Thales Group security communities.
---
# Install the Thales Group Taxonomy

    cd /var/www/MISP/app/files/taxonomies/
    mkdir thales-group-taxonomy
    cd thales-group-taxonomy
    
Copy the [`thales-group-taxonomy/machinetag.json`](https://github.com/thalesgroup-cert/Thalesgroup-misp-taxonomy/blob/main/thales-group-taxonomy/machinetag.json) file.

Go to MISP Web GUI `taxonomies/index` and click on **Update Taxonomies**. The newly created taxonomy should be visible. 

Now, you need to activate the tags within the taxonomy:
- Doucle click on the **thales_group taxonomy**
- Click on **(enable)**
- Go back to `taxonomies/index`
- Click on **(enable all)**
- Check **Required** checkbox (required for Event publication):
  - When publishing an Event, you will be required to use at least one TAG from the Thales Group taxonomy.

### [MANDATORY] Filter Event publication using the taxonomy 
Go to MISP Web GUI `/servers/index` and click on `Edit icon` on the **MISP Thales Group Internal Server**.

Then, modify the **Push rules**:
  - Add to **Blocked Tags (AND NOT)**:
    - `thales_group:tlp:black`
    - `tlp:red`
    - `thales_group:distribution="team_eyes_only"`

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
