---
title: Metadata Guidelines
summary: Descriptions of different metadata schemas used to describe various resources and pages in RSQKit.
---

This page explains the metadata that can be used to describe various resources and pages in RSQKit. 
These guidelines have been adapted from the ELIXIR Toolkit theme's [page metadata guide](https://elixir-belgium.github.io/elixir-toolkit-theme/page_mechanics)
and [tools and resources guide](https://elixir-belgium.github.io/elixir-toolkit-theme/resource_table).

## Contributor metadata

Contributors are listed in the [contributors file (`_data/CONTRIBUTORS.yml`)](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/CONTRIBUTORS.yml)
starting with the contributor's full name, followed by the following optional metadata/attributes:

* `git`: contributor's GitHub id (serving as an identifier together with contributor's full name).
* `orcid`: contributor's ORCID id.
* `role`: role of the contributor in the RSQKit (at the moment, we only support the role `editor`, but more may be added in the future; leave blank if the role is not `editor`).
* `affiliation`: contributor's affiliation(s) as a single string (if multiple affiliations need to be listed, use a separator - e.g. "/". 
Also note that while affiliations should match those listed in the [affiliations file (`_data/affiliations.yml`)](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/affiliations.yml) (see below) this is not enforced.
* `image_url`: absolute path to contributor's image or avatar (defaults to contributor's GitHub profile image if GitHub id is provided).

You can reference contributors by their name in the metadata section of content pages using parameter `contributors` - see [page metadata section](#page-metadata) for more details. 

An example contributor definition is given below:

<<<<<<< HEAD
* `search_exclude`: by setting this field true, the page will not end up in the search results of the searchbar. By default this is false.

* `sitemap`: let the page appear in the sitemap.xml. Default: true

* `no_robots`: by setting this field to true, the page will not end up in the search results of google or any other search engine.

* `hide_sidebar`: When true, the sidebar will be hidden. Default: false.

* `custom_editme`: This attribute can be used to specify an alternative file/link when clicked on the edit-me button.

* `keywords`: List here all the keywords that can be used to find the page using the searchbox in the right upper corner of the page, lowercase.

* `sidebar`: Specify here an alternative sidebar. Default: main.

* `toc`: When set to false, the table of contents in the beginning of the page will not be generated.

* `page_id`: Unique identifier of a page. It is usually a shortened version of the page name or title, with small letters and spaces, or an acronym, with capital and small letters. Used to list `Related` pages. If you forget to add this then autogenerated tables highlighting the mentioned tools and resources and related pages will not render.

* `datatable`: use this attribute to activate the pagination + sorting + searching in tables

### Related pages

* `related_pages`: List here the `page_id` of {{site.title}} pages that you want to display as Related pages, grouped by section.

  If you want pages from the specific section (Your tasks, Your domain, Tool assembly) to be shown here as Related pages, list their `page_id`. If you want to list multiple related pages, make sure to put them in a list like this: [page_id1, page_id2]. The specific sections allowed in each page are specified in each page template. Please, do not add extra sections in the metadata of the page.

  ```yml
  related_pages: 
    - your_tasks: [page_id1, page_id2]
    - your_domain: [page_id1, page_id2]
  ``` 


### Tools and resources

Pages will often include references to existing tools, which are further described in the RSQKit. To refer to a tool, first make sure they exist  in the [tool and resource list file](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/tool_and_resource_list.yml). Then, link to the tool from your page by using the following syntax:

{% raw %}
```
{% tool "Tool id" %}
```
{% endraw %}


Tools that are mentioned this way will be described in the mains tools and resources table. If you are confused about using the syntax, please [use a sample task page](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/pages/your_tasks/writing_readable_code.md) as reference, or ask for help to the reviewers when contributing your content. The metadata attributes of a tool may be browsed below.

## Metadata attributes of a tool
Tools are maintained in the [tool and resource list file](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/tool_and_resource_list.yml). A tool may have the following attributes: 

* `description`: A short description of the purpose of the tool or resource
* `id`: Identifier by which the tool will be references on other pages.
* `name`: Name of the tool or resource
* `registry`: This is followed by a list of registry-tag:search-string combinations indented below which search for further information about this tool  
       tess: <name>  <-- this will search the tess training registry using the term <name> - i.e. the tool name and return associated results - in this case around training on this tool
* `url`: Homepage of the tool/resource
* `qualityIndicator`: Research Software Quality indicator (see [quality_indicators.yml](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/quality_indicators.yml)) associated with this tool. More than one quality indicator may be declared per tool (in a list).

These attributes are a subset of the [EVERSE RS metadata schema](https://w3id.org/everse/rs#).

An example of a tool can be seen below:
```yml
- description: The System Package Data Exchange (SPDX) License List is a list of commonly found licenses and exceptions used in free and open or collaborative software, data, hardware, or documentation, and is an integral part of the SPDX Specification.
  id: spdx
  name: SPDX License List
  url: https://spdx.org/licenses/
```

## Metadata attributes of a research software quality indicator
Just like tools, indicators are described in the RSQKit. We currently support the following descriptions of indicators (following the [RS indicator metadata schema](https://w3id.org/everse/rsqi/)): 

* `identifier`: Identifier associated with the indicator.
* `contact`: Contact person or organization associated with the indicator in EVERSE.
* `name`: Name of the indicator (title).
* `description`: A brief description of the indicator, stating its purpose and how to measure it. 
* `keywords`: keywords to ease finding the indicator
* `qualityDimension`: Research Software quality dimension associated with the indicator (see https://w3id.org/everse/rsqi for a full list) 
* `version`: If the indicator has a version (e.g., some ISO standards specify indicators), it should be included here
* `source`: The standard or reference document where the indicator was first proposed
* `status`: States whether the indicator is still used or not (deprecated, obsolete, active, etc.)
* `created`: Date of creation of the indicator

Indicators are maintained in [https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/quality_indicators.yml](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/quality_indicators.yml). Example of an indicator:

```yml
- identifier: Do1 
  description: >
    Software includes clear contribution instructions, software purpose on project website, feedback channels, and version control practices.
  contact: Daniel Garijo # see CONTRIBUTORS.yml to declare contacts
  name: Contribution Process and Project Purpose
  keywords:
    - contribution guidelines
    - feedback channel
    - software purpose
  qualityDimension:
    - documentation 
  source: https://www.bestpractices.dev/en/criteria/0
  status: Active
```

## Metadata attributes of a research software quality dimension 
Indicators can be grouped according to common categories or quality dimensions (defined following the [RS quality dimension metadata schema](https://w3id.org/everse/rsqd/)): 

* `identifier`: Identifier associated with the dimension
* `description`: A brief text describing the dimension
* `name`: Name of the dimension (title)
* `source`: The standard(s) or reference document(s) where the dimension was proposed, or adapted from

Dimensions are maintained in [https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/quality_dimensions.yml](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/quality_dimensions.yml). En example dimension can be seen below:

```yml
- identifier: documentation 
  description: >
    Ability of the system to provide information helpful for identifying and resolving issues when it fails to work correctly. Existence of a helpdesk or issue tracking, bug reporting, enhancements and general support
  name: Documentation and Supportability
  source: 
    - https://www.iso.org/standard/35733.html
    - https://doi.org/10.5281/zenodo.10723608
```


## Metadata attributes of a contributor
Contributors are maintained in the [`CONTRIBUTORS.yml` file](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/CONTRIBUTORS.yml). Each contributor supports the metadata fields outlined below:

* `Full Name`: full name and surname of the contributor. It serves as an identifier.
* `git`: GitHub user id.
* `orcid`: ORCID user id.
* `role`: the role of the contributor in the RSQKit (editor or leave empty)
* `affiliation`: affiliation information. An identifier for the `affiliations.yml` file should be used.
* `image_url`: absolute path to image (defaults to image from GitHub)

You can reference contributors by their name in the page metadata section of content pages using parameter "contributors:". An example of a contributor can be seen below:

Example of a contributor: 
=======
>>>>>>> main
```yml
Fotis Psomopoulos:
    git: fpsom
    orcid: 0000-0002-0222-4273
    email: email.@org.edu
    role: editor
    affiliation: Institute of Applied Biosciences (INAB|CERTH) / ELIXIR-GR
```

## Affiliation metadata

Affiliations are listed in the [affiliations file (`_data/affiliations.yml`)](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/affiliations.yml)
and can be used as means of listing all institutions in the project or institutions/affiliations of all contributors. 

Affiliations can be described using the following metadata/attributes (all of which are optional apart from the `name`):

* `name`: name of the institution.
* `expose`: flag to indicate whether to show the affiliation in affiliation listings or not.
* `type`: type of affiliation, e.g. `institution`.
* `url`: URL of the affiliation.
* `pid`: persistent identifier of the affiliation (e.g. Research Organization Registry (ROR) id).
* `image_url`: absolute path to affiliation's image.

An example affiliation definition is given below:

```yml
- name: The University of Manchester
  image_url: /images/institutions/logo-university-of-manchester.svg
  expose: true
  type: institution
  url: https://www.manchester.ac.uk/
  pid: https://ror.org/027m9bs27
```

## Page metadata

Each page in RSQKit can be described with the following metadata/attributes (which can either be included 
in the "front matter" header of the page or applied to a group of pages via `_config.yml` repository file):

* `title`: page title (used as the H1 HTML header in the rendered version of the page).
* `summary`: a short page summary, displayed under the page title.
* `description`: a short page description, used when pages are listed as "tiles" (e.g. in search results, related pages sections or when all pages of certain type are listed).
* `type`: page type, used to classify pages into categories. Each page type is displayed differently in the website. Possible values: `research_community`, `task_page`.
* `contributors`: a list of contributors that authored or contributed significantly to the page in some way (e.g. via discussions). Each contributor must also be listed in the `_data/CONTRIBUTORS.yml` repository file.
* `search_exclude`: a boolean value indicating if the page should be excluded from search results. Default: `false`.
* `sitemap`: a boolean value indicating if the page should appear in the `sitemap.xml`. Default: `true`.
* `no_robots`: a boolean value indicating if the page should not end up in the search results of Google or any other search engines. Default: `false`.
* `hide_sidebar`: a boolean value indicating if the page should not appear in the sidebar. Default: `false`.
* `custom_editme`: specify an alternative file/link when clicking on the `edit-me` button.
* `keywords`: a list of lowercase keywords that can be used to find the page using the search facility of RSQKit.
* `sidebar`: name of the left-hand side navigation sidebar that should be displayed for the page. Default sidebar: `main`. The sidebar file `<SIDEBAR_NAME.md>` named after the sidebar must exist under `_data/sidebars/` in the repository.
* `toc`: a boolean value indicating if a table of contents should be included at the top right of the page. Default: `false`.
* `page_id`: unique identifier of the page, usually a shortened version of the page title (with words separated with underscores or dashes and spaces avoided). This identifier is used in `related_pages` parameter to list pages related to this page. 
* `datatable`: a boolean value indicating the activation of the pagination, sorting and searching in tabular representations of pages.
* `related_pages`: a list of `page_id`s that are related to this page and will appear under "Related pages" section on the page, grouped by page type.
* `page_citation`: When set to `true`, it will cause the citation section for the page to be generated in the format: "<author names>. <page title>. <site domain>. <page URL>. <date accessed>". Defaults to `true` for task pages; `false` for other page types.

## Tools and resources metadata

Tools and resources are described in the [tool and resource data file (`_data/tool_and_resource_list.yml`)](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/tool_and_resource_list.yml) using the 
following attributes (a subset of the [EVERSE Research Software metadata schema](https://w3id.org/everse/rs#)): 

* `name`: name of the tool or resource.
* `description`: a short description of the tool or resource.
* `id`: identifier used to refer to the tool or resource in pages.
* `url`: URL of the tool or resource
* `quality_indicator`:  research software quality indicators associated with this tool. We have not settled 100% on the format of attribute yet - this is still work in progress. 
Most likely it will be a list of research software quality indicators (defined in the [quality indicators data file (`_data/quality_indicators.yml`)](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/quality_indicators.yml)).

An example of a tool definition is given below:

```yml
- description: > 
    The System Package Data Exchange (SPDX) License List is a list of commonly found licenses 
    and exceptions used in free and open or collaborative software, data, hardware, or 
    documentation, and is an integral part of the SPDX Specification.
  id: spdx
  name: SPDX License List
  url: https://spdx.org/licenses/
```

Pages in RSQKit can include references to tools and resources. Such references will appear visually different on a page - 
with a little wrench icon and a pop-up window which shows up on hover over and includes the tool/resource description and a website link.

To refer to a tool or a resource in a page, use the following syntax:

{% raw %}
```
{% tool "tool-id" %}
```
{% endraw %}

All tools and resources mentioned on a page will be listed in a table at the bottom of the page as well as under "[All Tools and Resources](all_tools_and_resources)" page. 
Have a look at an [example task page](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/pages/your_tasks/zenodo_doi.md) for how this syntax is used in practice.

## Software quality indicator metadata

Research Software Quality (RS Quality) indicators are described in the [quality indicators data file (`_data/quality_indicators.yml`)](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/quality_indicators.yml) using the
following attributes (a subset of the [EVERSE Research Software indicator metadata schema](https://w3id.org/everse/rsqi/)):

* `identifier`: identifier associated with the indicator.
* `contact`: contact person or organisation associated with the indicator.
* `name`: name of the indicator (title).
* `description`: a brief description of the indicator, stating its purpose and how to measure it. 
* `keywords`: keywords to ease finding the indicator.
* `quality_dimension`: Research Software Quality (RS Quality) dimension associated with the indicator (see [https://w3id.org/everse/rsqd](https://w3id.org/everse/rsqd) for a full list).
* `version`: if the indicator has a version (e.g., some ISO standards specify indicators), it should be included here.
* `source`: the standard or reference document where the indicator was first proposed.
* `status`: status of the indicator (e.g. deprecated, obsolete, active, etc.).
* `created`: date of creation of the indicator.

An example of an RS Quality indicator definition is given below:

```yml
- identifier: Do1 
  description: >
    Software includes clear contribution instructions, software purpose on project website, 
    feedback channels, and version control practices.
  contact: Daniel Garijo
  name: Contribution Process and Project Purpose
  keywords:
    - contribution guidelines
    - feedback channel
    - software purpose
  qualityDimension:
    - documentation 
  source: https://www.bestpractices.dev/en/criteria/0
  status: active
```

## Software quality dimension metadata  

Research Software Quality indicators can be grouped according to common categories or quality dimensions.
Research Software Quality dimensions are described in the [quality dimensions data file (`_data/quality_dimensions.yml`)](https://github.com/EVERSE-ResearchSoftware/RSQKit/blob/main/_data/quality_dimensions.yml) using the
following attributes from the [EVERSE Research Software dimension metadata schema](https://w3id.org/everse/rsqd/): 

* `identifier`: identifier associated with the dimension.
* `description`: description of the dimension.
* `name`: name of the dimension (title).
* `source`: the standard(s) or reference document(s) where the dimension was proposed, or adapted from.

An example of an RS Quality dimension definition is given below:

```yml
- identifier: documentation 
  description: >
    Ability of the system to provide information helpful for identifying and resolving issues 
    when it fails to work correctly. Existence of a helpdesk or issue tracking, bug reporting, 
    enhancements and general support
  name: Documentation and Supportability
  source: 
    - https://www.iso.org/standard/35733.html
    - https://doi.org/10.5281/zenodo.10723608
```