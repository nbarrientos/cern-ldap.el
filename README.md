The aim of this package is to provide a set of functions to interact
with CERN&rsquo;s LDAP servers, allowing to lookup users by login and full
name and the membership of user groups. The output is normally
displayed in read-only buffers. Below you can find a list of variables
that can be customised and also the commands that this package
provides. It&rsquo;s recommended though to read the documentation of each
variable and function as this document typically contains only
summaries and brief explanations.

Even though it&rsquo;s obviously tailored to the CERN context and hence with
a rather small audience, this package might also serve as inspiration
for others learning how to talk to LDAP servers using Emacs.


# Licence

See `COPYING`.


# Disclaimer

This Emacs package has no affiliation whatsoever with [CERN](https://home.cern) or the [CERN
IT department](https://information-technology.web.cern.ch/) and it&rsquo;s hence not maintained as part of any CERN
project.

However, the [current maintainer](https://cern.ch/nacho) (who turns out to be working for CERN
at the moment) will be happy to discuss changes and give a helping
hand but please note that developing `cern-ldap.el` is not part of his
paid job.


# Download and installation

The source code is available in Sourcehut and automatically mirrored
to Github for convenience:

-   **Sourcehut:** <https://git.sr.ht/~nbarrientos/cern-ldap.el>
-   **Github (mirror):** <https://github.com/nbarrientos/cern-ldap.el>

It&rsquo;d be cool to make the package available through MELPA but, given
the very scoped audience it has, I imagine it&rsquo;d be unlikely to be
accepted for distribution. I&rsquo;ll try at some point, though.


## Using `use-package`

Example installation with `use-package` using a local copy:

    (use-package cern-ldap
    :ensure nil
    :load-path "~/.emacs.d/local-packages/cern-ldap.el"
    :custom
    (cern-ldap-server-url "ldap://localhost:1389"))

Don&rsquo;t forget to clone the source code into the load path specified
above (or any other of your choice).


# Contributing

Send patches and/or comments to the [mailing list](https://lists.sr.ht/~nbarrientos/cern-ldap.el).


# Customisation options

The package allows the user to customise the behaviour of the code in
several ways. Here&rsquo;s just a list of the customisation variables for
quick reference:

-   `cern-ldap-server-url`
-   `cern-ldap-buffer-name-format`
-   `cern-ldap-user-lookup-login-key`
-   `cern-ldap-user-lookup-full-name-key`
-   `cern-ldap-user-full-name-matching-type`
-   `cern-ldap-user-displayed-attributes`
-   `cern-ldap-user-group-membership-filter`
-   `cern-ldap-user-sort-key`

For more information just run `M-x customize-group cern-ldap` or read
the documentation of each of the variables listed above, for example
by running `M-x describe-variable cern-ldap-server-url`.


# User interface


## With explicit input

These commands will always prompt for user input using the minibuffer.

-   **`cern-ldap-user-by-login`:** Lookup a user by login. With prefix
    argument, return more information.
-   **`cern-ldap-user-by-full-name`:** Lookup a user (or several) by full
    name. The search query is enclosed in `*` by default, making the
    search query more greedy (see
    `cern-ldap-user-full-name-matching-type`).
-   **`cern-ldap-group`:** Lookup the members of a group by name. With
    prefix argument, do it non-recursive.

Please refer to the built-in help of each function for further
information.


## With implicit input

The following commands fish the required input from the current
buffer, either from the active region or from the word at point. The
word is collected with `superword-mode` enabled so for instance groups
with dashes are picked up.

-   `cern-ldap-user-by-login-dwim`
-   `cern-ldap-user-by-full-name-dwim`
-   `cern-ldap-group-dwim`

Please refer to the built-in help of each function for further
information.


# Keybindings

No keybindings, keymaps or global minor modes are provided. It&rsquo;s up to
the user to configure them to their liking.


## Combining with transient

It might be a good idea to pack these commands in a [transient](https://github.com/magit/transient) menu,
for example:

    (transient-define-prefix my/cern-ldap-dispatch ()
      "Dispatch CERN LDAP related commands."
      [["LDAP user (by login)"
        ("U" "Dwim" cern-ldap-user-by-login-dwim)
        ("u" "Ask" cern-ldap-user-by-login)]
       ["LDAP user (by full name)"
        ("F" "Dwim" cern-ldap-user-by-full-name-dwim)
        ("f" "Ask" cern-ldap-user-by-full-name)]
       ["LDAP group"
        ("G" "Dwim" cern-ldap-group-dwim)
        ("g" "Ask" cern-ldap-group)]])

