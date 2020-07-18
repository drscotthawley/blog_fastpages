---
layout: post
title: Resolving Mac OS X Aliases in Python
subtitle: (or "How I Spent Monday Night")
description: Mac OSX aliases are not symbolic links. Trying to read one will probably crash your code.
image: http://cdn.osxdaily.com/wp-content/uploads/2012/06/remove-alias-arrows-mac.jpg
bg-image: http://cdn.osxdaily.com/wp-content/uploads/2012/06/remove-alias-arrows-mac.jpg
comments: true
---
Mac OSX aliases are not symbolic links. Trying to read one may crash your code.

In an app I'm developing, I want users to be able to easily create a "library" of symbolic links to
other places on their machine, and this is most easily achieved for many of them by Cmd-Option-Dragging and dropping the files.
This creates an "alias", which is a special file that Apple dreamed up.  UNIX users are accustomed to symbolic links, and codes
written in UNIX will not follow or "resolve" Mac aliases. Instead, they will cause an exception to be thrown.

There used to be some libraries to handle this, but they relied on Apple's old Carbon framework which is no longer supported.
There is a [mac_alias](https://mac-alias.readthedocs.io/en/latest/) package but the documentation is lacking. So, I found an
[old post on MacWorld](https://hints.macworld.com/article.php?story=20021024064107356) where one solution is given, and I ported that
for what I need.

Happy to share with you, so that you won't have to worry about this.  As an added bonus, you can tell it to convert aliases to symbolic
links, so that "next time" you won't have to deal with this.  Enjoy.

```python
#!/usr/bin/env python3
#
# Resolve Mac OS X 'aliases' by finding where they point to
# Author: Scott H. Hawley
#
# Description:
# Mac OSX aliases are not symbolic links. Trying to read one will probably crash your code.
# Here a few routines to help. Run these to change the filename before trying to read a file.
# Intended to be called from within other python code
#
# Python port modified from https://hints.macworld.com/article.php?story=20021024064107356
#
# Requirements: osascript (AppleScript), platform, subprocess, shlex
#
# TODO: - could make it work in parallel when mutliple filenames are given
#
# NOTE: By default, this only returns the names of the original source files,
#       but if you set convert=True, it will also convert aliases to symbolic links.
#
import subprocess
import platform
import os

# returns true if a file is an OSX alias, false otherwise
def isAlias(path, already_checked_os=False):
    if (not already_checked_os) and ('Darwin' != platform.system()):  # already_checked just saves a few microseconds ;-)
        return False
    checkpath = os.path.abspath(path)       # osascript needs absolute paths
    # Next several lines are AppleScript
    line_1='tell application "Finder"'
    line_2='set theItem to (POSIX file "'+checkpath+'") as alias'
    line_3='if the kind of theItem is "alias" then'
    line_4='   return true'
    line_5='else'
    line_6='   return false'
    line_7='end if'
    line_8='end tell'
    cmd = "osascript -e '"+line_1+"' -e '"+line_2+"' -e '"+line_3+"' -e '"+line_4+"' -e '"+line_5+"' -e '"+line_6+"' -e '"+line_7+"' -e '"+line_8+"'"
    args = shlex.split(cmd)      # shlex splits cmd up appropriately so we can call subprocess.Popen with shell=False (better security)
    p = subprocess.Popen(args, shell=False, stdout=subprocess.PIPE, stderr=subprocess.STDOUT)
    retval = p.wait()
    if (0 == retval):
        line = p.stdout.readlines()[0]
        line2 = line.decode('UTF-8').replace('\n','')
        if ('true' == line2):
            return True
        else:
            return False
    else:
        print('resolve_osx_alias: Error: subprocess returned non-zero exit code '+str(retval))
    return None


# returns the full path of the file "pointed to" by the alias
def resolve_osx_alias(path, already_checked_os=False, convert=False):        # single file/path name
    if (not already_checked_os) and ('Darwin' != platform.system()):  # already_checked just saves a few microseconds ;-)
        return path
    checkpath = os.path.abspath(path)       # osascript needs absolute paths
    # Next several lines are AppleScript
    line_1='tell application "Finder"'
    line_2='set theItem to (POSIX file "'+checkpath+'") as alias'
    line_3='if the kind of theItem is "alias" then'
    line_4='   get the posix path of (original item of theItem as text)'
    line_5='else'
    line_6='return "'+checkpath+'"'
    line_7 ='end if'
    line_8 ='end tell'
    cmd = "osascript -e '"+line_1+"' -e '"+line_2+"' -e '"+line_3+"' -e '"+line_4+"' -e '"+line_5+"' -e '"+line_6+"' -e '"+line_7+"' -e '"+line_8+"'"
    args = shlex.split(cmd)              # shlex splits cmd up appropriately so we can call subprocess.Popen with shell=False (better security)
    p = subprocess.Popen(args, shell=False, stdout=subprocess.PIPE, stderr=subprocess.STDOUT)
    retval = p.wait()
    if (0 == retval):
        line = p.stdout.readlines()[0]        
        source = line.decode('UTF-8').replace('\n','')
        if (convert):
            os.remove(checkpath)
            os.symlink(source, checkpath)
    else:
        print('resolve_osx_aliases: Error: subprocess returned non-zero exit code '+str(retval))
        source = ''
    return source


# used for multiple files at a time, just a looped call to resolve_osx_alias
def resolve_osx_aliases(filelist, convert=False):  # multiple files
    #print("filelist = ",filelist)
    if ('Darwin' != platform.system()):
        return filelist
    outlist = []
    for infile in filelist:
        source = resolve_osx_alias(infile, already_checked_os=True, convert=convert)
        if ('' != source):
            outlist.append(source)
    #print("outlist = ",outlist)
    return outlist


if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description='Resolve OSX aliases')
    parser.add_argument('file', help="alias files to resolve", nargs='+')
    args = parser.parse_args()
    outlist = resolve_osx_aliases(args.file)
    print("outlist = ",outlist)
```
The above code is part of the `utils/` directory in my [Panotti](https://github.com/drscotthawley/panotti/tree/master/utils) package.
The way it's called is in the context of trying to read an audio file, called in the file [panotti/datautils.py](https://github.com/drscotthawley/panotti/blob/master/panotti/datautils.py):

```python
def load_audio(audio_path, mono=None, sr=None, convertOSXaliases=True):  # wrapper for librosa.load
    try:
        signal, sr = librosa.load(audio_path, mono=mono, sr=sr)       # try to read the file 'normally'
    except NoBackendError as e:                                      
        if ('Darwin' == platform.system()):                           # if an exception is thrown, check: Am I on a Mac? If so try to resolve an alias
            source = resolve_osx_alias(audio_path, convert=convertOSXaliases, already_checked_os=True) # ...and convert to symlinks for next time
            try:
                signal, sr = librosa.load(source, mono=mono, sr=sr)   # Now try to read again
            except NoBackendError as e:                               # Ok, even that didn't work, giving up (for now).
                print("\n*** ERROR: Could not open audio file {}".format(audio_path),"\n",flush=True)
                raise e
        else:                                                         # Failure for some other reason.
            print("\n*** ERROR: Could not open audio file {}".format(audio_path),"\n",flush=True)
            raise e
    return signal, sr
```

Happy coding!

*NOTE: Currently this code only follows _one_ alias.  If there's an alias pointing to an alias to a file, it won't resolve to that file.
Full generality would involve adding an iterative or recursive way of traversing multiple aliases which...I may do later. ;-)*
