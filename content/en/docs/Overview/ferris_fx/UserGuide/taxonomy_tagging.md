---
title: "Taxonomy/Tagging"
linkTitle: "Taxonomy/Tagging"
weight: -09
description: >
    How to add Tags and the importance of Taxonomy.
---

Taxonomies or Tags describe the ability to organize and structure types and classes of objects and their correlations
within executions/services and events (event types) across any given application, use case or project. Tags are
searchable and makes it easy to group and relate objects across different components and lifecycle stages.

As a generic base module "taggability" can easily be included in any model, use case or application by the
developers/users.

**Note: As of the current release the Taxonomy is universal across all projects, use cases and cannot be segregated
along different functional domains. It is thus essential to create a unified naming convention to be shared among the
different projects & user groups.**

# Taxonomies / Tags

1. Click on Taxonomies in the left menu to open dropdown and then on Tags
2. Click Add to create a tag

{{< blocks/screenshot color="white" image="/images/taxonomies_tags_add_roboto.png">}}

1. Name Tag
2. Save

{{< blocks/screenshot color="white" image="/images/create_tag_save_roboto.png">}}

- Check created Tag(s)

1. Click on the magnifying glass to open details (show tag) page
2. This will automatically transfer you to the tag details page
3. Click on *List services* to see in which services the same tag is used
5. Click on *Event Types* to see in which event type the same tag uses (in this example no event type is associated with
   the tag just created)
6. Click on the Edit icon (List tags page) to edit/rename a tag

{{< blocks/screenshot color="white" image="/images/tag_list_click_loupe_details_roboto.png">}}

{{< blocks/screenshot color="white" image="/images/show_tag_details_roboto.png">}}

{{< blocks/screenshot color="white" image="/images/list_tag_services_roboto.png">}}

{{< blocks/screenshot color="white" image="/images/list_event_types_tag_roboto.png">}}

{{< blocks/screenshot color="white" image="/images/list_tags_edit_roboto.png">}}

## Search Tag

1. Click *Search* on top of the *List Tags* / *Details Page*
2. Click *Add Filter* to choose a filter (currently only the "Name" filter is supported)
3. From the dropdown list choose the tag to be searched for

- Starts with
- Ends with
- Contains
- Equal to
- Not Starts with
- Not ends with
- Not Contains

4. Insert tag "Name"
5. Hit the Search button

{{< blocks/screenshot color="white" image="/images/search_tag_filter_roboto.png">}}

- Check search results

{{< blocks/screenshot color="white" image="/images/search_results_new.png">}}

