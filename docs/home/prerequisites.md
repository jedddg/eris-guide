## Installing Node.js

If you haven't already, make sure to install Node.js.

Eris requires a minimun of Node.js version 10.4.0 and higher, but its recommended you install the Long Term Support (LTS) version for the best stability.

## Installing a code editor

A code editor is an advanced text editor that can bring more tools to your work environment.

It is highly suggested you install a proper code editor, rather then using NotePad or Notepad++!

Some good examples are:

-   [Visual Studio Code](https://code.visualstudio.com/)
-   [Sublime Text](https://www.sublimetext.com/)
-   [Atom](https://atom.io/)

## Initializing your project

We want to setup our `package.json` file. This will store important information in here, like the dependencies you use, the name of your project and many other things.

Open a terminal in the folder of your choice and initialize the project by running:

```bash
npm init
```

_(You can add the `-y` flag at the end of the command, to automatically skip all options and provide the default options.)_

## Installing Eris

Installing Eris is simple, by typing:

```bash
npm i --no-optional eris
```

In some use cases, you may need to remove the `--no-optional` flag if you need voice support.

As Eris' [Getting Started](https://abal.moe/Eris/docs/0.16.1/getting-started) page says:

`If you want voice support, remove the --no-optional flag from the command before running it`

Make sure to check out the [Getting Started documentation page](https://abal.moe/Eris/docs/0.16.1/getting-started), as there are extra requirements in order to use voice.
