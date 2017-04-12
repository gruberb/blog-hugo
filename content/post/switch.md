+++
title = "Back to the basics and Sublime Text"
Description = ""
Tags = ["tools"]
Categories = []
date = "2017-04-12T10:40:41+01:00"
+++

<img src="https://preview.ibb.co/jMyYBQ/sublime.png" alt="sublime">

Since the beginning of JavaScript on the desktop, aka <a href="https://electron.atom.io/">Electron</a>, I was happily switching to <a href="https://atom.io/">GitHubs Atom text editor</a>. The benefits are obvious:

- Open Source
- Written in JavaScript, my main langauge
- Comes from a cool brand
- Faster development cycles

Ever since I switched, I loved Atom. Many plugins are enhancing your life as a developer. A few glitches here and there didn't let me question my decision a few years ago.

Since today. I read on Hacker News that <a href="https://www.sublimetext.com/3">Sublime Text</a> released a new (sub) version of their third version. Sublime Text was (or still is?) the standard text editor when it comes to coding. Or lets say the standard for everybody who is using macOS and a MacBook. So I gave the newest version a shot, and found out:

- Who needs Open Source in your text editor if it runs so smoothly?
- It's written in C++ and Python, blazing fast 
- Who cares about the brand?
- Slow development cycles, but very stable product

I changed a few things (themes, line heights etc.) and I am happier than ever. Here are my `user preferences`:

```
{
	"bold_folder_labels": true,
	"caret_style": "phase",
	"color_scheme": "Packages/Theme - One Dark/One Dark.tmTheme",
	"fade_fold_buttons": false,
	"font_size": 14,
	"highlight_line": true,
	"find_selected_text": true,
	"ignored_packages":
	[
		"Vintage"
	],
	"line_padding_bottom": 2,
	"line_padding_top": 2,
	"tab_size": 2,
	"theme": "One Dark.sublime-theme",
}
```

The most important steps were:

- <a href="https://packagecontrol.io/installation">Install the Package Manager</a>
- <a href="https://packagecontrol.io/packages/Theme%20-%20One%20Dark">Switch to the One Dark theme from Atom</a> 
- Increase the font size to 14px
- Add a bit of line padding to have more space for each line

I found some cool options like a fancy cursor:

`"caret_style": "phase"`


Overall, this is the way to go. I feel super happy and hope that besides the cool new shiny Sublime Text logo is just the beginning of a new developer journey. Now, I am enjoying the same fancy look from Atom on top of a blazing fast and stable Sublime Text 3.