### Editing and Copying the Handbook

This page is for future users who want to edit this handbook or who want to make a handbook of their own. 

**Fork a Copy:** The easiest way to adapt this handbook is to clone the Group Handbook repo from the Kulkarni Group [Github](https://github.com/kul-group) and edit it yourself. See below for editing details.

**Starting your own copy:** To make your own handbook, start a Github repository and begin adding pages written in markdown formatting. Make sure the page titles have no spaces and end with `.md`. This will help with converting your handbook to a website.

#### Basic Editing

See [here](https://www.markdownguide.org/basic-syntax) for a Markdown guide. Though knowing basic Markdown will serve most of your needs, it is useful to know that Github uses slightly different Markdown called ["Github Flavored Markdown"](https://guides.github.com/features/mastering-markdown/) which differs in some places.

Make **bold text** using `**example text**`, __italics__ using `__example text__`

##### Headings

Put several hashes in front of your heading, more hashes means a smaller heading. For example `### Heading` will be smaller than `## Heading` when the document is rendered.

##### Links

**Internal Links:** The syntax is simple for linking to another page within your repository. Simply write `[link_title](file_name.md)` where "link_title" can be any label you want and will show up as blue text, while "file_name.md" is the precise title of the page you want to link to (case sensitive). For example, `[example](Introduction.md)` would link the the introduction of this handbook.

**External Links:** The syntax follows the same rules as an internal link except instead of the file name, you place a URL in the parenthesis. For example, to link to the Kulkarni group website, write `[example](https://kulkarni.sf.ucdavis.edu/)`

#### Publishing as a website

[Github Pages](https://pages.github.com/) makes it easy to convert a repo directly into a website, however, it can be pretty expensive if you have several contributors to a repo. Additionally, the repository has to be public to produce a website. You can host the website for free and incorporate new contributions by making a public repository in someone's __individual__ account, cloning the original handbook repository to it, and, in your new repository settings, selecting a source and theme for your webpage in the "GitHub Pages" section. You can incorporate new changes by adding them to the individual repository which supports the website. 
