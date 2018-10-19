---
title: 一款比man更好用的工具：tldr
toc: true
comment: true
date: 2018-10-16 23:05:10
categories: [IT]
tags: shell
---

感谢duang duang给我介绍的一款实用的小工具:tldr

[tldr的官网介绍](http://tldr-pages.github.io/)

tldr = too long don't read

通常我们碰到一个陌生或很长时间没用过的command命令的时候不会用，会用man来查看这个命令的用法，但是man的介绍太详细了，如下所示：

<!--more-->

以下是截取的一部分命令介绍：

```
BSDTAR(1)                 BSD General Commands Manual                BSDTAR(1)

NAME
     tar -- manipulate tape archives

SYNOPSIS
     tar [bundled-flags <args>] [<file> | <pattern> ...]
     tar {-c} [options] [files | directories]
     tar {-r | -u} -f archive-file [options] [files | directories]
     tar {-t | -x} [options] [patterns]

DESCRIPTION
     tar creates and manipulates streaming archive files.  This implementation
     can extract from tar, pax, cpio, zip, jar, ar, and ISO 9660 cdrom images
     and can create tar, pax, cpio, ar, and shar archives.

     The first synopsis form shows a ``bundled'' option word.  This usage is
     provided for compatibility with historical implementations.  See COMPATI-
     BILITY below for details.

     The other synopsis forms show the preferred usage.  The first option to
     tar is a mode indicator from the following list:
     -c      Create a new archive containing the specified items.
     -r      Like -c, but new entries are appended to the archive.  Note that
             this only works on uncompressed archives stored in regular files.
             The -f option is required.
     -t      List archive contents to stdout.
     -u      Like -r, but new entries are added only if they have a modifica-
             tion date newer than the corresponding entry in the archive.
             Note that this only works on uncompressed archives stored in reg-
             ular files.  The -f option is required.
```

急等着一个命令用的时候，真的是欲仙欲死。

比较一下，用`tldr`查询`tar`的结果：

```shell
➜  ~ tldr tar
Local data is older than two weeks, use --update to update it.


tar

Archiving utility.
Often combined with a compression method, such as gzip or bzip.

- Create an archive from files:
    tar cf target.tar file1 file2 file3

- Create a gzipped archive:
    tar czf target.tar.gz file1 file2 file3

- Extract an archive in a target folder:
    tar xf source.tar -C folder

- Extract a gzipped archive in the current directory:
    tar xzf source.tar.gz

- Extract a bzipped archive in the current directory:
    tar xjf source.tar.bz2

- Create a compressed archive, using archive suffix to determine the compression program:
    tar caf target.tar.xz file1 file2 file3

- List the contents of a tar file:
    tar tvf source.tar

- Extract files matching a pattern:
    tar xf source.tar --wildcards "*.html"
```

根据示例，立马就知道这个命令的常见用法了。

最后，把tldr设置成man的alias别名，更方便日常的使用

```shell
alias man="tldr"
```

