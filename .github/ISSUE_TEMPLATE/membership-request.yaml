---
name: membership-request.yml
about: Describe this issue template's purpose here.
title: ''
labels: ''
assignees: vinceskahan
body:
  - type: markdown
    attributes:
      value: |
        Thanks for taking the time to fill out this bug report!
 - type: input
    id: contact
    attributes:
      label: Contact Details
      description: How can we get in touch with you if we need more info?
      placeholder: ex. email@example.com
    validations:
      required: false
---

---
########################################################################
# How to create a YAML issue template form in your repository          #
########################################################################
# To use a YAML issue form in your repository, you must create a new
# file and add it to the .github/ISSUE_TEMPLATE folder in your
# repository by typing the full path to the new file in when prompted
# for a new file's name.
#
# If, for example, you wanted to create the bug.yaml form to add to your
# repository, click on the <> Code tab, then click on the "Add file"
# button, click on "Create new file", and then type this into the window
# that pops up: .github/ISSUE_TEMPLATE/bug.yaml
#
# Note that you won't need to get rid of your Markdown issue template.
########################################################################
# Required top-level fields                                            #
########################################################################
# The name is a string that's unique across all templates:
name: Foo
# The description is a string that is no more than 200 characters long
# that describes the intended use for this template:
description: Bar
########################################################################
# Optional top-level fields                                            #
########################################################################
# The title is an optional string that will pre-populate the title field
# in the issue submission form. If you leave it blank, the title field
# will be empty and will need to be filled in by the user. If you
# populate it with a string value, it will contain that value with a
# blinking cursor indicating to the user that he or she can change it.
title: Baz
# The labels are an array or comma-delimited string of labels that will
# automatically be assigned to this issue:
labels: new
# The assignees are an array or comma-delimited string of users the
# issue will be automatically assigned to:
assignees:
- Dave
- Jane
# The body is an array that defines user inputs:
body:
  # YOUR YAML HERE, INDENTED BY 2 SPACES SO THAT IT'S PART OF THE BODY.
  ######################################################################
  # NATIVE DATA STRUCTURES                                             #
  ######################################################################
  # YAML represents any native data structure using three node kinds:  #
  # sequence (an ordered series of entries)                            #
  # mapping (an unordered association of unique keys to values)        #
  # scalar (any datum with opaque structure presentable as a series of #
  #         Unicode characters)                                        #
  ######################################################################
  # SOME EXAMPLES:

  # CHECKBOX:
  - type: checkboxes
    id: checkboxes
    attributes:
      label: What kinds of M&Ms do you like?
      description: You may select more than one.
      options:
        - label: Green
        - label: Orange
        - label: Red
        - label: Yellow
    validations:
      required: false

  # CHECKBOX WITH REQUIRED ITEM:
  - type: checkboxes
    id: checkboxes_multiple_with_required_item
    attributes:
      label: What kinds of M&Ms do you like?
      description: You may select more than one.
      options:
        - label: Green
          required: true
        - label: Orange
        - label: Red
        - label: Yellow
    validations:
      required: false

  # DROPDOWN:
  - type: dropdown
    id: download
    attributes:
      label: How did you download the software?
      options:
        - apt-get
        - Built from source
        - Homebrew
        - MacPorts
    validations:
      required: true

  # INPUT:
  - type: input
    id: prevalence
    attributes:
      label: Bug prevalence
      description: "How often do you or others encounter this bug?"
      placeholder: "Whenever I visit the user account page."
    validations:
      required: false

  # MARKDOWN:
  - type: markdown
    id: markdown
    value: "## Welcome!"
    validations:
      required: false

  # MARKDOWN WITH MULTI-LINE CONTENT:
  - type: markdown
    id: markdown_with_multiline_content
    value: |
      ## Welcome!
      This type of entry can be used to communicate with the user
      without asking for any input.
    validations:
      required: false

  # MARKDOWN WITH EMOJIS:
  - type: markdown
    id: markdown_with_emojis
    attributes:
      value: >
        Type an emoji name from the emoji cheat sheet (see below)
        between two colons to insert an emoji in your Markdown. For
        example, this is a heart: :heart:
    validations:
      required: false

  # MARKDOWN WITH FOOTNOTES:
  - type: markdown
    id: markdown_with_footnotes
    attributes:
      value: |
        This is the first footnote link[^1].
        This is the second footnote link[^2].
        This is the third footnote link[^note].
        [^1]: This is the first footnote.
        [^2]: This is the second footnote. It's a multi-line footnote.
          Newlines should be indented with 2 spaces.
        [^note]: This is the third footnote. It's a named footnote that
          renders with numbers just like simple footnotes do, but the
          name allows for easier identification and linking.
    validations:
      required: false

  # MARKDOWN WITH LINK TO ISSUE:
  - type: markdown
    id: markdown_with_link_to_issue
    attributes:
      value: |
        You can mention a bug with an explicit link. For example:
        [test](https://github.com/Elliria/hello-world/issues/2)
        This short version might also work, but I haven't tested it:
        [test](Elliria/hello-world#2)
    validations:
      required: false

  # MARKDOWN WITH MENTION:
  - type: markdown
    id: markdown_with_mention
    attributes:
      value: |
        You can mention a GitHub member with an at symbol followed by
        their name. For instance, to mention myself, I would use
        @Elliria.
    validations:
      required: false

  # MARKDOWN WITH TABLES:
  - type: markdown
    id: markdown_with_tables
    attributes:
      value: |
        | Column 1 Heading  | Column 2 Heading |
        | ------------- | ------------- |
        | Column 1 cell  | Column 2 cell  |
        | Column 1 cell  | Column 2 cell  |
        | Column 1 cell  | Column 2 cell  |

        | Left-aligned | Center-aligned | Right-aligned |
        | :---         |     :---:      |          ---: |
        | one | two | three |
        | one | two | three |
        | one | two | three |
    validations:
      required: false

  # TEXTAREA:
  - type: textarea
    id: textarea
    attributes:
      label: My text
      description: "Which version of the software did you use?"
    validations:
      required: false

  # TEXTAREA PREPOPULATED WITH CONTENTS:
  - type: textarea
    id: textarea_prepopulated_with_contents
    attributes:
      label: Textarea prepopulated with contents
      description: "How do you trigger this bug?"
      value: |
        1. Do this.
        2. Then do that.
        3. Then do the other.
    validations:
      required: false

  # TEXTAREA WITH A PLACEHOLDER:
  - type: textarea
    id: textarea_with_a_placeholder
    attributes:
      label: Textarea with a placeholder
      description: "How do you trigger this bug?"
      placeholder: |
        1. Do this.
        2. Then do that.
        3. Then do the other.
    validations:
      required: false

  # TEXTAREA RENDERED WITH LANGUAGES:
  # If a render value is provided, submitted text will be formatted in a
  # code block and the textarea will not expand for file attachments or
  # Markdown editing. The available languages known to GitHub:
  # https://github.com/github/linguist/blob/master/lib/linguist/languages.yml
  
  # TEXTAREA RENDERED WITH BASH:
  - type: textarea
    id: textarea_rendered_with_bash
    attributes:
      label: Textarea rendered with Bash
      description: |
        Please provide some example command output:
      render: bash
    validations:
      required: false

  # TEXTAREA RENDERED WITH CSS:
  - type: textarea
    id: textarea_rendered_with_CSS
    attributes:
      label: Textarea rendered with CSS
      description: |
        Please provide some example CSS:
      render: CSS
    validations:
      required: false

  # TEXTAREA RENDERED WITH INI:
  - type: textarea
    id: textarea_rendered_with_ini
    attributes:
      label: Textarea rendered with ini
      description: |
        Please provide some example ini:
      render: ini
    validations:
      required: false

  # TEXTAREA RENDERED WITH MARKDOWN:
  - type: textarea
    id: textarea_rendered_with_markdown
    attributes:
      label: Textarea rendered with Markdown
      description: "Please provide some example Markdown:"
      render: markdown
    validations:
      required: false

  # TEXTAREA RENDERED WITH MARKDOWN AND PREPOPULATED WITH CONTENTS:
  - type: textarea
    id: textarea_rendered_with_markdown_and_prepopulated_with_contents
    attributes:
      label: Textarea rendered with Markdown and prepopulated contents
      description: "How do you trigger this bug?"
      value: |
        ## Steps:
        1. Do this.
        2. Then do that.
        3. Then do the other.
      render: markdown
    validations:
      required: false

  # TEXTAREA RENDERED WITH MARKDOWN WITH A PLACEHOLDER:
  - type: textarea
    id: textarea_rendered_with_markdown_with_a_placeholder
    attributes:
      label: Textarea rendered with Markdown with a placeholder
      description: "How do you trigger this bug?"
      placeholder: |
        ## Steps:
        1. Do this.
        2. Then do that.
        3. Then do the other.
      render: markdown
    validations:
      required: false

  # TEXTAREA RENDERED WITH SHELL:
  - type: textarea
    id: textarea_rendered_with_shell
    attributes:
      label: Textarea rendered with shell
      description: >
        Please provide some example command output:
      render: shell # shouldn't this be sh instead?
    validations:
      required: false

  # TEXTAREA RENDERED WITH TXT:
  - type: textarea
    id: textarea_rendered_with_txt
    attributes:
      label: Example text snippet
      description: |
        Please provide some example text:
      render: txt
    validations:
      required: false

  # TEXTAREA RENDERED WITH XML:
  - type: textarea
    id: textarea_rendered_with_xml
    attributes:
      label: Example XML
      description: |
        Please provide some example XML:
      render: xml
    validations:
      required: false

  # TEXTAREA RENDERED WITH YAML:
  - type: textarea
    id: textarea_rendered_with_yaml
    attributes:
      label: Example YAML snippet
      description: |
        Please provide some example YAML:
      render: yaml
    validations:
      required: false

  ######################################################################
  # MULTI-LINE KEYS OR VALUES USING BLOCK-CHOMPING INDICATORS          #
  ######################################################################
  # To create multi-line keys or values, you can use block-chomping
  # indicators:
  #
  # The > indicator automatically wraps the text.
  #
  # > "clip": keep the final linebreak, remove trailing blank lines.
  # >+ "keep": keep the final linebreak, keep trailing blank lines.
  # >- "strip": remove the final linebreak, remove trailing blank lines.

  foo: >
    Clip example.
    Keep the final linebreak.
    Remove trailing blank lines.
  bar: >+
    Keep example.
    Keep the final linebreak.
    Keep trailing blank lines.
  baz: >-
    Strip example.
    Remove the final linebreak.
    Remove trailing blank lines.

  # The | indicator respects the placement of the text as is.
  #
  # | "clip": keep the final linebreak, remove trailing blank lines.
  # |+ "keep": keep the final linebreak, keep trailing blank lines.
  # |- "strip": remove the final linebreak, remove trailing blank lines.
  #
  # You can also manually insert a linebreak anywhere in the middle of
  # a word or between words or simply at a specific point by putting ...
  # and YAML will replace those three dots with a newline.

  foo: |
    Clip example.
    Keep the final linebreak.
    Remove trailing blank lines.
  bar: |+
    Keep example.
    Keep the final linebreak.
    Keep trailing blank lines.
  baz: |-
    Strip example.
    Remove the final linebreak.
    Remove trailing blank lines.


  # TEXTAREA WITH A MULTI-LINE VALUE THAT CONTAINS A LINEBREAK:
  - type: textarea
    id: textarea_with_multi-line_value_with_linebreak
    attributes:
      label: Textarea with a multi-line value that contains a linebreak
      description: |
        This will be on the first line...and this will be on the second
        line.
    validations:
      required: false

  ######################################################################
  # NOTES                                                              #
  ######################################################################
  # Boolean values can be on/off, true/false, or yes/no.
  #
  # Lists can be aligned with their parent or indented one level,
  # whichever you prefer.
  ######################################################################
  # URLS FOR MORE INFORMATION                                          #
  ######################################################################
  # Documenting your project with wikis: https://docs.github.com/en/communities/documenting-your-project-with-wikis
  # Emoji cheat sheet: https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md
  # Example GitHub YAML bug report: https://www.youtube.com/watch?v=40r3WhCQL08
  # GitHub-flavored Markdown is accepted: https://github.github.com/gfm/
  # Languages known to GitHub (all instances of ace_mode on this page): https://github.com/github/linguist/blob/master/lib/linguist/languages.yml
  # Maintaining your safety on GitHub: https://docs.github.com/en/communities/maintaining-your-safety-on-github
  # Managing disruptive comments: https://docs.github.com/en/communities/moderating-comments-and-conversations/managing-disruptive-comments
  # Setting up your project for healthy contributions: https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions
  # Syntax for GitHub's form schema: https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-githubs-form-schema
  # Syntax for issue forms: https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms
  # Using templates to encourage useful issues and pull requests: https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests
  # Welcome to issue forms: https://gh-community.github.io/issue-template-feedback/welcome/
  # Writing on GitHub: https://docs.github.com/en/github/writing-on-github
  # YAML home page: https://yaml.org/
  # YAML validator: http://www.yamllint.com/
...
