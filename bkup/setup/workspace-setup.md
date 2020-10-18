# Workspace Setup

[<<](../)

## Table-of-Contents

- [git](#git)
- [sdkman! for java and mvn](#sdkman!-for-java-and-mvn)
- [nvm](#nvm)
- [other tools](#other-tools)
- [other config](#other-config)

## git

1. Download [git](https://git-scm.com/download/win) and install *Git-2.25.1-64-bit.exe*
1. Add ssh key to github.

   - Generate ssh key

        ```console
        $ ssh-keygen -t rsa -b 4096 -C "em@il.com"
        Generating public/private rsa key pair.
        Enter a file in which to save the key (/c/Users/you/.ssh/id_rsa):[Press enter]
        Enter passphrase (empty for no passphrase):
        Enter same passphrase again:
        ```

   - Go `https://github.com/settings/keys`
      - Click New SSH key
      - Enter key
1. Add git alias
     - Go to `~/.bash_profile` and add [git-alias-list](./settings/git-alias-list.txt)
     - References
       - [git-scm-docs](https://git-scm.com/docs/)
       - [git-cheatsheet-interactive](https://ndpsoftware.com/git-cheatsheet.html)

 [~](#Table-of-Contents)

## sdkman!-for-java-and-mvn

1. Reference [Guide](https://ngeor.com/2019/12/07/sdkman-windows.html) and [sdkman!](https://sdkman.io/)
2. Verify prerequisites

   ```console
    $ which zip
    /mingw64/bin/zip

    $ which unzip
    /usr/bin/unzip

    $ which curl
    /mingw64/bin/curl

    $ which tar
    /usr/bin/tar

    $ which gzip
    /usr/bin/gzip
   ````

    - If zip does not exist, add zip into git bash
       - Navigate to [gnuwin32/zip](https://sourceforge.net/projects/gnuwin32/files/zip/3.0/)
          - Download zip-3.0-bin.zip
          - In the zipped file, in the bin folder, find the file zip.exe.
          - Extract the file “zip.exe” to your "mingw64" bin folder `C:\Program Files\Git\mingw64\bin`
       - Navigate to [gnuwin32/bzip2](https://sourceforge.net/projects/gnuwin32/files/bzip2/1.0.5/)
          - Download bzip2-1.0.5-bin.zip
          - In the zipped file, in the bin folder, find the file bzip2.dll
          - Extract bzip2.dll to your "mingw64" bin folder `C:\Program Files\Git\mingw64\bin`

3. Install **sdkman**.

   ```console
    curl -s "https://get.sdkman.io" | bash
   ````

4. Install **java**.

    ```console
    sdk list java
    sdk install java 11.0.6-amzn
    ```

    - Java [SDK Vendors](https://dzone.com/articles/an-overview-on-jdk-vendors)
    - Update environment variables

        ```properties
        JAVA_HOME ~\.sdkman\candidates\java\current
        ```

    - move `JAVA_HOME` to top on environment variables
    - Verfiy java version

        ```console
        $ java --version

        openjdk 11.0.6 2020-01-14 LTS
        OpenJDK Runtime Environment Corretto-11.0.6.10.1 (build 11.0.6+10-LTS)
        OpenJDK 64-Bit Server VM Corretto-11.0.6.10.1 (build 11.0.6+10-LTS, mixed mode)
        ```

5. Install **maven**.

    ```console
    sdk list maven
    sdk install maven 3.6.3
    ```

    - Update environment variables

       ```properties
        MAVEN_HOME ~\.sdkman\candidates\maven\current
        ```

    - Add [settings.xml](./settings/settings.xml) to .m2

 [~](#Table-of-Contents)

## nvm

1. [nvm-windows](https://github.com/coreybutler/nvm-windows/releases) - A node.js version management utility for Windows.
2. Download and run `nvm-setup.exe`.
3. Move `NVM_HOME` `NVM_SYMLINK` to top on environment variables
4. Run the following command

    ```console
    nvm list available
    nvm install 13.11.0
    nvm use 13.11.0
    ```

5. Verify version

    ```console
    $ nvm list
      * 13.11.0 (Currently using 64-bit executable)

    $ node -v
    v13.11.0
    ```

 [~](#Table-of-Contents)

## other-tools

1. [Screen Recorder to GIF](https://www.screentogif.com/)
2. Notepad++ Plugins
   - [Markdown](https://github.com/nea/MarkdownViewerPlusPlus)
3. [VS Code](https://code.visualstudio.com/) Extensions
   - [Auto-Open Markdown Preview](https://marketplace.visualstudio.com/items?itemName=hnw.vscode-auto-open-markdown-preview)
   - [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)
   - [API Blueprint Viewer](https://marketplace.visualstudio.com/items?itemName=develiteio.api-blueprint-viewer)
4. Chrome Plugins
   - [Markdown Preview Plus](https://chrome.google.com/webstore/detail/markdown-preview-plus/febilkbfcbhebfnokafefeacimjdckgl)

 [~](#Table-of-Contents)

## other-config

1. Chrome Search Engine
   - Chrome > Settings > Search Engine > Manage Search Engines
   - Enter the following:
      - Search Engine: git-scm
      - Keyword: gs
      - URL: `https://git-scm.com/docs/%s`
   - For local file storage
     - Search Engine: file
     - Keyword: f
     - URL: `file:///C:/etc`

[<<](../)
