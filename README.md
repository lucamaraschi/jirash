A Jira shell. Show a ticket. Create an issue. List projects.
That sort of thing.

# Getting Started

Get jirash:

    $ cd ~/opt
    $ git clone https://github.com/trentm/jirash.git
    $ alias jirash='$HOME/opt/jirash/bin/jirash'      # or whatever

First you need a config file with Jira URL and auth info:

    $ cat ~/.jirash.json
    {
      "jira_url": "https://dev.example.com/jira",
      "https://dev.example.com/jira": {
        "username": "joe.blow",
        "password": "secret"
      }
    }

Then use it (this is an example and might be a little out of date):

    $ jirash help
    Usage:
        jirash COMMAND [ARGS...]
        jirash help [COMMAND]

    Options:
        -h, --help          show this help message and exit
        --version           show version and exit
        -d, --debug         debug logging
        -J JIRA_URL, --jira-url=JIRA_URL
                            Jira base URL. Otherwise defaults to 'jira_url' value
                            from config file.

    Commands:
        createissue    Create a new issue.
        help (?)       give detailed help on a specific sub-command
        issue          Get an issue.
        issuetypes     Get an issue types (e.g. bug, task, ...).
        projects       List projects (excluding "Archived" projects).
        versions       Get available versions for the given project.

    $ jirash projects
    KEY         NAME                              LEAD
    DOC         DOC: Documentation                philip
    TOOLS       TOOLS: Tools and Extras           trent.mick
    ...

    $ jirash issues TOOLS-90
    TOOLS-90: Add a distclean target (mark.cavage -> trent.mick, Improvem...)

    $ jirash TOOLS-90     # shortcut
    TOOLS-90: Add a distclean target (mark.cavage -> trent.mick, Improvem...)

    $ ./jirash.py createissue TOOLS
    Summary: Foo is broken
    Description (use '.' on a line by itself to finish):
    blah
    blah
    blah
    .
    created: TOOLS-157: Foo is broken (trent.mick -> <unassigned>, Bug, Normal, Open)
