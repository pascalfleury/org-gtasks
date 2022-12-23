# Org-Gtasks

Export/import all Google Tasks to org files.

This module has been inspired by [org-gcal](https://github.com/kidd/org-gcal.el).

`org-gtasks` will

-   sync all the task lists you have into org files, one per list
-   map `TODO` and `DONE` status to the same on Google Tasks

## Config

You can define an account, identified by its *name* and with
org files stored in a particular directory like so:
``` elisp
(require 'org-gtasks)
(org-gtasks-register-account :name "Perso"
                             :directory "~/.emacs.d/gtasks/"
                             :login "massonju.eseo@gmail.com"
                             :client-id "XXXX"
                             :client-secret "XXXX")
```

## Obtaining Google credentials

1.  Go to [Google Developers Console](https://console.developers.google.com/project)
2.  Create a project (with any name)
3.  Click on the project
4.  Click on **APIs & Services** then **Credentials**
5.  Click on **Create credentials** and select **OAuth Client ID**
6.  Select Application type *Desktop* and give a name (e.g. *emacs*)
7.  Click on **Create**
8.  Copy the *Client ID* and *Client secret* into the relevant fields in the config (see below)
9.  Under the same **APIs & Services** menu section, select **Library**
10. Search for **Tasks API**, click on it and click **Enable**
11. Add yourself as *Test users* in **OAuth consent screen**.

You have now a project that accepts OAuth credentials and enables
the *Tasks API* for them.

## Setup

The first time you use `org-gtasks`, you need to authenticate.
These are the steps you will go through:

1.  Make sure Emacs has read your config. Then, `M-x org-gtasks`
    will show a prompt asking for the account. Enter its name,
    e.g. *Perso* as in the example config above.
2.  It will ask for the action, enter *Pull*.
3.  It will open your browser, and ask you to login. Then it will show
    a code, that you need to ...
4.  ... paste into the minibuffer where it asks about it.

You're done! You should now find one file per task list in the
directory you have configured.

**Note**: the OAuth token file is stored in the directory where the org
files are written, named `.refresh-token`

## Usage

Type `M-x org-gtasks`, enter the account name, an action,
and the operation takes a few seconds and you are done.

Possible actions are: (defined in `org-gtasks-actions`)

| Actions    | Descriptions                                       |
|------------|----------------------------------------------------|
| **Push**   | push one or all taskslists                         |
| **Fetch**  | fetch one or all taskslists (org file not updated) |
| **Pull**   | pull one or all taskslists                         |
| **Add**    | add taskslists on the gtasks account               |
| **Remove** | remove taskslists present on the gtasks account    |

## Limitations

Currently, `org-gtasks` does not understand or map the hierachical structure of tasks.
