---
layout: post
title: "AlgoRaving on OS X with Tidal"
description: ""
category: ""
tags: []
---
{% include JB/setup %}

AlgoRaving?
==========
I recently read [this article](http://www.vice.com/read/algorave-is-the-future-of-dance-music-if-youre-an-html-coder), and was instantly fascinated. Electronic music and programming are two of my biggest passions, and I've never seen such an awesome marriage between the two. I wanted to try out the software the Algoravers were using, especially since it was written in Haskell!

[Alex McLean](http://yaxu.org) is the maintainer of [Tidal](http://yaxu.org/tidal/), a Haskell library for the "Live coding of pattern". The documentation is pretty solid, but since I ran into a few bumps installing it on OS X (Mavericks), I wanted to share some tips.

Most of this is adapted from the official pdf documentation for Tidal.

Installation
============
You'll need [HomeBrew](http://brew.sh) on your Mac to get started.

We’re installing emacs with brew since OS X ships with a fairly dated version. If you already have the Haskell platform installed, you should omit it here.

	brew install haskell-platform emacs jack liblo wget

	cabal update
	cabal install cabal-install # if suggested
	cabal install tidal

Get the required emacs file

	mkdir ~/tidal && cd ~/tidal
	wget https://raw.github.com/yaxu/Tidal/master/tidal.el

Edit your ~/.emacs file to include the tidal.el file.

	(add-to-list 'load-path "∼/tidal")
	(require 'tidal)

Add the marmalade package repository for emacs so we can install haskell-mode for emacs.
If you didn't install emacs with brew, you also need to install package.el, which I won't cover.
This was taken from (https://github.com/haskell/haskell-mode)

	(require 'package)
	(add-to-list 'package-archives
    	'("marmalade" . "http://marmalade-repo.org/packages/"))
	(package-initialize)


Now we install haskell-mode for emacs.

Note that we specify the version when running emacs so the version installed with brew is started instead of OS X’s included (old) version

	emacs-24.3
	M-x eval-buffer
	M-x package-refresh-contents
	M-x package-install \[RET\] haskell-mode
	C-c C-x 


Compile the dirt synthesizer.

	git clone https://github.com/yaxu/Dirt.git
	cd Dirt
	make clean; make


Start Jack and the Dirt synthesizer that Tidal uses.

	jackd -d coreaudio &
	./dirt &
	
Run emacs!

	emacs-24.3

You should follow the tutorial in the official pdf to start making music with Tidal.
 
