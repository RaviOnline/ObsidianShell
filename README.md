# ObsidianShell
Languages: [English](README.md), [简体中文](README.zh-Hans.md)

## Features
- Associate Markdown files with Obsidian  
  In addition to making it easy to open notes, associating files helps integrate Obsidian into your workflows. For example, you can use a launcher to quickly open notes.
  
  For Chinese users:  
  配合支持拼音搜索的启动器，还可以间接实现通过拼音搜索笔记文件，比如：
  - [Everything](https://www.voidtools.com/) + [IbEverythingExt](https://github.com/Chaoses-Ib/IbEverythingExt)
  - [Listary](https://www.listarypro.com/)
- VaultRecent/Recent mode
  - Open standalone Markdown files in Obsidian, i.e., use Obsidian as a Markdown editor.
  - Enable the *global vault pattern*, which means that you can share one config with your notes at different locations.
- Open Markdown files in Obsidian through command line

## Installation
[Releases](https://github.com/Chaoses-Ib/ObsidianShell/releases)

Config file location: `%LOCALAPPDATA%\Chaoses Ib\ObsidianShell\ObsidianShell.Config`

### Set as the default program for Markdown files
![](images/File%20list.png)

1. Right-click on a .md file
2. Select `Open with` → `Choose another app` → `ObsidianCLI`
3. Check `Always use this app to open .md files`
4. Click `OK`

## CLI
A command line interface program for opening Markdown files in Obsidian.

It supports three opening modes:
- VaultFallback (default)  
  If the Markdown file is in a vault, open the vault, otherwise open the file using the Markdown fallback (see below).
- VaultRecent  
  If the Markdown file is in a vault, open the vault, otherwise link the file to Recent vault and open the vault.

  The idea to implement it comes from [@etienne](https://forum.obsidian.md/t/open-and-edit-standalone-markdown-files/14977).
- Recent  
  Link the Markdown file to Recent vault and open the vault.

You can change the opening mode in `ObsidianShell.Config`:
```xml
<add key="OpenMode" value="VaultFallback" />
```

Notice: The vault where the Markdown file in must be in the vault list before opening the file, i.e., you must have opened that vault before, otherwise Obsidian will report an error.

### Markdown fallback
You can change the Markdown fallback editor in `ObsidianShell.Config`.

Notepad (default):
```xml
<add key="MarkdownFallback" value="notepad" />
<add key="MarkdownFallbackArguments" value="{0}" />
```

[Visual Studio Code](https://code.visualstudio.com/):
```xml
<add key="MarkdownFallback" value="%LOCALAPPDATA%\Programs\Microsoft VS Code\Code.exe" />
<add key="MarkdownFallbackArguments" value="{0}" />
```
(The use of `code` is not recommended since it is actually an batch file and leads to a delay)

[Typora](https://typora.io/) (≥ 1.1):
```xml
<add key="MarkdownFallback" value="C:\Program Files\Typora\Typora.exe" />
<add key="MarkdownFallbackArguments" value="{0}" />
```

### Recent vault
You can set the location of your Recent vault in `ObsidianShell.Config`:
```xml
<add key="RecentVault" value="C:\path\to\Recent" />
```
And the maximum number of subdirectories in Recent:
```xml
<add key="RecentLimit" value="10" />
```

Notice: You must have opened the Recent vault before, otherwise Obsidian will report an error when opening files.

## ContextMenu
![](images/ContextMenu.png)

It is used to open the corresponding directory in Obsidian, complementing the defect that the CLI cannot be associated with directories.