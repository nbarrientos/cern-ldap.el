

# License

See `COPYING`.


# Disclaimer

This Emacs package has no affiliation whatsoever with CERN or the CERN
IT department and it&rsquo;s not maintained by CERN.

Even though it&rsquo;s obviously tailored to the CERN context, it could
serve as inspiration for others learning how to talk to LDAP servers
using Emacs.


# Download and installation

The source code is available in Sourcehut:

-   <https://git.sr.ht/~nbarrientos/cern-ldap.el>


## `use-package`

Example installation with `use-package`:

    (use-package cern-ldap
    :ensure nil
    :load-path "~/.emacs.d/local-packages/cern-ldap.el"
    :custom
    (cern-ldap-server-url "ldap://localhost:1389"))

Don&rsquo;t forget to clone the source code into the load path specified
above.


# Customisation options

The package allows the user to customize the behaviour of code. For
more information just run `M-x customize-group cern-ldap`.


# User interface


## With explicit input

These commands will always prompt for user input.

-   **`cern-ldap-user-by-login`:** Lookup a user by login.
-   **`cern-ldap-user-by-full-name`:** Lookup a user (or several) by full
    name. The search query is enclosed in `*` by default, making the
    search query more greedy.
-   **`cern-ldap-group`:** Lookup a group by name. With prefix argument,
    do it non-recursive.

Please refer to the built-in help of each function for further
information.


## With implicit input

The following commands fish required input from the current buffer,
either from the active region or from the word at point. The word is
collected with `superword-mode` enabled so for instance groups with
dashes are picked up.

-   `cern-ldap-user-by-login-dwim`
-   `cern-ldap-user-by-full-name-dwim`
-   `cern-ldap-group-dwim`

Please refer to the built-in help of each function for further
information.

