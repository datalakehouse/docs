Contributing to this repository
===============================

|:smile:| |:heart_eyes:| First off, thanks for taking the time to contribute! With your help, we’re making developers' lives easier. |:heart_eyes:| |:smile:|

The following is a set of tips and guidelines that will help you improve the DLH developer portal.


What should I know before I contribute?
---------------------------------------

**What is docs?**

docs is DLH’s developer portal. Its goal is to provide a comprehensive set of help articles aimed at developers using DLH’s products. 


**How does docs work?**

It is Python-based, with content in ReStructuredText (rst) and rendered by Sphinx.


**What is the content model?**

docs contains the following content types:
- *Concept* - Conceptual content helps people understand a feature or topic by providing a clear, high-level overview, explanation of how the feature or topic can help them on their journey, and context like use cases or examples. 
- *Task* - Task content helps people complete a task from start to finish while they're using DLH’s products.
- *Reference* - Referential content provides detailed information that people need while they're actively using DLH's products.
- *Tutorial* - Tutorials help people learn about products, and solve real world problems by guiding them through the entire workflow to complete a task.

.. tip::
    Use the templates included below for further guidance. 

To learn more about documentation content types, see the `Diátaxis Framework <https://diataxis.fr/>`_.


**What is the structure of docs?**

You can see the structure in the left-hand navigation menu. 
It is driven by a plugin called `Sphinx external TOC <https://sphinx-external-toc.readthedocs.io/en/latest/intro.html>`_. 

You can find the current structure in ``_toc.yml``.

If you have an article about any of the DLH tools (API, CLI, console, Terraform provider, Kubernetes operator), place it in the **DLH tools** section.
If you have an article about any specific DLH product (M3, Kafka, Grafana, etc.), nest it in the product-specific section. 
If you have an article with general reference information, place it in the **Resources** section. 


How can I contribute?
---------------------

Reporting bugs, and suggesting enhancements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you notice something is off (anything - from typos to completely incorrect instructions) or missing, consider opening an issue. 

.. tip::
    Before you open an issue, check all the existing issues for the docs to make sure you're not duplicating it. 


Contributing via pull requests (PRs)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you have your own article to add or you want to modify an existing article yourself, here's what you do:

1. Fork the repo.
2. Make your update.
3. Open a pull request (make sure you use a helpful PR and commit message). 
4. Submit your PR, and get it reviewed (one reviewer is required). 

We'll merge it!

.. note::
    Our build runs several checks on your updates - from linting to spell check to broken links to help you commit good content. Look at the **Checks** section in your pull request to make sure everything passes. If anything fails, check the error details, or reach out to us, and we'll help you. 


Style tips
==========

If you're writing content, here are some high-level tips that can be useful:

- Decide what type of content you want to contribute (check the content model above), and use our content type templates - for concept, task, reference and tutorial.

- Write a good title (start with a verb for tasks, and noun for concepts, or use one of the templates below to guide you). 

- Note down your main ideas, and decide what formatting will best support these (use the content templates):
    - Ordered lists - for tasks
    - Paragraphs - for definitions and explanations
    - Lists and tables - for reference/options

- Highlight information by using the following elements:
    - Tip - for interesting facts about parts of your content/alternative ways of doing something, and shortcuts
    - Important - for important facts readers need to know before proceeding
    - Info - for any extra information (this may be skipped)

- Add good links (internal and external) - properly formatted, to reputable sources of information.

- Choose your visuals (images, diagrams, screenshots) and include them in a specified size (no bigger than 800px). 



Style guides and other resources
================================

Templates for docs content (by type)
-----------------------------------------

**Concept**::

    ---
    title: *About [subject]* (if this is a background information for a task, e.g. *About migrating to DLH*) / *Subject* (use noun or noun phrase, e.g. *Authentication*, *High availability*)
    short description: Answer the question "What is this?" and "Why do I care about this?" If the concept is unfamiliar, start with a brief definition.
    ---

    A section here
    --------------

    .. Write one or two paragraphs about the main idea of your topic, as a summary. 
        Make sure you don't have any content that isn't preceded by a header, or it won't be linkable in our TOC. 

    Another section here
    --------------------

    .. Write one or two paragraphs about another element of your topic. 
        Keep adding headers and sections until you've completed your article.  


**Task**::

    ---
    title: Start with a verb (e.g. *Connect with Go*, *Install or upgrade an extension*).
    intro: Explain what the task helps users accomplish, the benefits of the task, or the purpose of the task. Try to include information that will help users understand when the task is appropriate or why the task is necessary. 
    ---

    Procedural section header here
    -------------------------------

    .. Include prerequisite information or specific permissions information here.
        Then write procedural steps using ordered lists. 
        Include only one way of doing something. If there's a shortcut, make sure to add it as a **Tip**. 

    Optionally, another procedural section here 
    -------------------------------------------

    Keep adding procedures until you've finished writing your article.


**Reference**::

    ---
    title: Nouns describing your subject
    intro: Briefly describe what the reference item does, what it is, or what it is used for (e.g. *List of configuration elements*)
    ---
    
    A section here
    --------------

    .. Write one or two paragraphs about the main idea of your topic, as a summary.
        Reference content is often in a form of table or list. Decide which works better for you.
        Make sure you don't have any content that isn't preceded by a header, or it won't be linkable in our TOC.

    Another section here
    ------------------------

    .. Write one or two paragraphs about another element of your topic.
        Keep adding headers and sections until you've completed your article. 


Styleguides and more info
-------------------------

- `ReStructuredText primer <https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html>`_
- `Diátaxis Framework <https://diataxis.fr/>`_.


|:pray:|  Thanks again for contributing! |:pray:|

DLH Team
