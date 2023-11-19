## Step 1
Download [Obsidian](https://obsidian.md/download)

---
## Step 2
Download and enable [Better BibTeX for Zotero](https://retorque.re/zotero-better-bibtex/) in Zotero

---
## Step 3
Set up Obsidian folders and a file
- Make folders named "Templates/Inputs", "Inbox", and "Images"
- Create a file "paper" in "Inputs"
- Copy and paste this into "paper"
```
---
category: literaturenote
tags: 
citekey: "{{citekey}}"
status: unread
dateread:
---
> [!Cite] 
> {{bibliography}}
  
>[!md] 
{% for type, creators in creators | groupby("creatorType") -%}  
{%- for creator in creators -%}  
>**{{"First" if loop.first}}{{type | capitalize}}**::
{%- if creator.name %} {{creator.name}}
{%- else %} {{creator.lastName}}, {{creator.firstName}}  
{%- endif %}  
{% endfor %}~  
{%- endfor %}  
> **Title**:: {{title}}
> **Year**:: {{date | format("YYYY")}} 
> **Citekey**:: {{citekey}} {%- if itemType %}
> **itemType**:: {{itemType}}{%- endif %}{%- if itemType == "journalArticle" %}  
> **Journal**:: *{{publicationTitle}}* {%- endif %}{%- if volume %}  
> **Volume**:: {{volume}} {%- endif %}{%- if issue %}
> **Issue**:: {{issue}} {%- endif %}{%- if itemType == "bookSection" %}  
> **Book**:: {{publicationTitle}} {%- endif %}{%- if publisher %}  
> **Publisher**:: {{publisher}} {%- endif %}{%- if place %}
> **Location**:: {{place}} {%- endif %}{%- if pages %}
> **Pages**:: {{pages}} {%- endif %}{%- if DOI %}
> **DOI**:: {{DOI}} {%- endif %}{%- if ISBN %}  
> **ISBN**:: {{ISBN}} {%- endif %}  

> [!LINK]
{%- for attachment in attachments | filterby("pdfURI") %}  
[{{attachment.title}}]({{attachment.pdfURI}}) {%- endfor %}.
  
> [!Abstract]
 >{%- if abstractNote %}
 >{{abstractNote}}
 >{%- endif %}

🔖 Tags
{% if hashTags %}{{hashTags}}{% endif %}

{% macro heading(color) -%}
{%- if color == "#ffd400" -%}
⭐ Important
{%- endif -%}
{%- if color == "#ff6666" -%}
⛔ Weaknesses and caveats
{%- endif -%}
{%- if color == "#5fb236" -%}
🧩 Definitions and concepts
{%- endif -%}
{%- if color == "#2ea8e5" -%}
❔ Questions
{%- endif -%}
{%- endmacro -%}

{% persist "annotations" %}
{% set annotations = annotations | filterby("date", "dateafter", lastImportDate) -%}
{% if annotations.length > 0 %}

*Imported on {{importDate | format("YYYY-MM-DD HH:mm")}}*

{% for color, annotations in annotations | groupby("color") -%}

### {{heading(color)}} <br>

{%- for annotation in annotations -%}
{%- if annotation.imageRelativePath %}
![[{{annotation.imageRelativePath}}]]
{%- endif %}
{%- if annotation.comment %}
- {{annotation.comment}}
	- {{annotation.annotatedText | nl2br}} [(p. {{annotation.pageLabel}})](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.pageLabel}}&annotation={{annotation.id}}) {% if annotation.allTags %}{{annotation.allTags}}{% endif %}
{%- elif annotation.annotatedText %}
- {{annotation.annotatedText | nl2br}} [(p. {{annotation.pageLabel}})](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.pageLabel}}&annotation={{annotation.id}}) {% if annotation.allTags %}{{annotation.allTags}}{% endif %}

{%- endif -%}
{%- endfor %}

{% endfor -%}
{% endif %}
{% endpersist %}

```
---
## Step 4
Set up Obsidian plugin
- Download Zotero Integration from community plugins (just search it in Obsidian!)
- Set up the plugin from a setting ⚙️ as below
![[Screenshot 2023-11-19 at 12.34.54.png]]![[Screenshot 2023-11-19 at 12.35.04.png]]![[Screenshot 2023-11-19 at 12.35.30.png]]![[Screenshot 2023-11-19 at 12.35.43.png]]
---
## Step 5
- Press cmd-p (for Mac guys) and type in the paper's name in the pop-up Zotero search bar
- You get a markdown file named with a unique citekey like this
- The "🔖 Tags" are the tags you add to the document with attachments (tags for annotations are displayed with invdiviual annotation)
![[Screenshot 2023-11-19 at 13.09.45.png]]
![[Screenshot 2023-11-19 at 13.09.53.png]]
![[Screenshot 2023-11-19 at 13.10.03.png]]

## Step 6
You can refer to the file key in Obsidian like this
```
[[@citekey]]
```


