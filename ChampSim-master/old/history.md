(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ gcc -v
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/usr/lib/gcc/x86_64-linux-gnu/9/lto-wrapper
OFFLOAD_TARGET_NAMES=nvptx-none:hsa
OFFLOAD_TARGET_DEFAULT=1
Target: x86_64-linux-gnu
Configured with: ../src/configure -v --with-pkgversion='Ubuntu 9.4.0-1ubuntu1~20.04.1' --with-bugurl=file:///usr/share/doc/gcc-9/README.Bugs --enable-languages=c,ada,c++,go,brig,d,fortran,objc,obj-c++,gm2 --prefix=/usr --with-gcc-major-version-only --program-suffix=-9 --program-prefix=x86_64-linux-gnu- --enable-shared --enable-linker-build-id --libexecdir=/usr/lib --without-included-gettext --enable-threads=posix --libdir=/usr/lib --enable-nls --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --with-default-libstdcxx-abi=new --enable-gnu-unique-object --disable-vtable-verify --enable-plugin --enable-default-pie --with-system-zlib --with-target-system-zlib=auto --enable-objc-gc=auto --enable-multiarch --disable-werror --with-arch-32=i686 --with-abi=m64 --with-multilib-list=m32,m64,mx32 --enable-multilib --with-tune=generic --enable-offload-targets=nvptx-none=/build/gcc-9-Av3uEd/gcc-9-9.4.0/debian/tmp-nvptx/usr,hsa --without-cuda-driver --enable-checking=release --build=x86_64-linux-gnu --host=x86_64-linux-gnu --target=x86_64-linux-gnu
Thread model: posix
gcc version 9.4.0 (Ubuntu 9.4.0-1ubuntu1~20.04.1) 
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ bash -v
# System-wide .bashrc file for interactive bash(1) shells.

# To enable the settings / commands in this file for login shells as well,
# this file has to be sourced in /etc/profile.

# If not running interactively, don't do anything
[ -z "$PS1" ] && return

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, overwrite the one in /etc/profile)
# but only if not SUDOing and have SUDO_PS1 set; then assume smart user.
if ! [ -n "${SUDO_USER}" -a -n "${SUDO_PS1}" ]; then
  PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi

# Commented out, don't overwrite xterm -T "title" -n "icontitle" by default.
# If this is an xterm set the title to user@host:dir
#case "$TERM" in
#xterm*|rxvt*)
#    PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME}: ${PWD}\007"'
#    ;;
#*)
#    ;;
#esac

# enable bash completion in interactive shells
#if ! shopt -oq posix; then
#  if [ -f /usr/share/bash-completion/bash_completion ]; then
#    . /usr/share/bash-completion/bash_completion
#  elif [ -f /etc/bash_completion ]; then
#    . /etc/bash_completion
#  fi
#fi

# sudo hint
if [ ! -e "$HOME/.sudo_as_admin_successful" ] && [ ! -e "$HOME/.hushlogin" ] ; then
    case " $(groups) " in *\ admin\ *|*\ sudo\ *)
    if [ -x /usr/bin/sudo ]; then
	cat <<-EOF
	To run a command as administrator (user "root"), use "sudo <command>".
	See "man sudo_root" for details.
	
	EOF
    fi
    esac
fi

# if the command-not-found package is installed, use it
if [ -x /usr/lib/command-not-found -o -x /usr/share/command-not-found/command-not-found ]; then
	function command_not_found_handle {
	        # check because c-n-f could've been removed in the meantime
                if [ -x /usr/lib/command-not-found ]; then
		   /usr/lib/command-not-found -- "$1"
                   return $?
                elif [ -x /usr/share/command-not-found/command-not-found ]; then
		   /usr/share/command-not-found/command-not-found -- "$1"
                   return $?
		else
		   printf "%s: command not found\n" "$1" >&2
		   return 127
		fi
	}
fi
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"
export LESSOPEN="| /usr/bin/lesspipe %s";
export LESSCLOSE="/usr/bin/lesspipe %s %s";

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
	# We have color support; assume it's compliant with Ecma-48
	# (ISO/IEC-6429). (Lack of such support is extremely rare, and such
	# a case would tend to support setf rather than setaf.)
	color_prompt=yes
    else
	color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi
LS_COLORS='rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:';
export LS_COLORS

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi
#                                                          -*- shell-script -*-
#
#   bash_completion - programmable completion functions for bash 4.1+
#
#   Copyright © 2006-2008, Ian Macdonald <ian@caliban.org>
#             © 2009-2019, Bash Completion Maintainers
#
#   This program is free software; you can redistribute it and/or modify
#   it under the terms of the GNU General Public License as published by
#   the Free Software Foundation; either version 2, or (at your option)
#   any later version.
#
#   This program is distributed in the hope that it will be useful,
#   but WITHOUT ANY WARRANTY; without even the implied warranty of
#   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#   GNU General Public License for more details.
#
#   You should have received a copy of the GNU General Public License
#   along with this program; if not, write to the Free Software Foundation,
#   Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
#
#   The latest version of this software can be obtained here:
#
#   https://github.com/scop/bash-completion

BASH_COMPLETION_VERSINFO=(2 10)

if [[ $- == *v* ]]; then
    BASH_COMPLETION_ORIGINAL_V_VALUE="-v"
else
    BASH_COMPLETION_ORIGINAL_V_VALUE="+v"
fi

if [[ ${BASH_COMPLETION_DEBUG-} ]]; then
    set -v
else
    set +v
fi
unset BASH_COMPLETION_ORIGINAL_V_VALUE

# ex: filetype=sh

# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/bella/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/bella/anaconda3/etc/profile.d/conda.sh" ]; then
        . "/home/bella/anaconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/bella/anaconda3/bin:$PATH"
    fi
fi
export CONDA_EXE='/home/bella/anaconda3/bin/conda'
export _CE_M=''
export _CE_CONDA=''
export CONDA_PYTHON_EXE='/home/bella/anaconda3/bin/python'

# Copyright (C) 2012 Anaconda, Inc
# SPDX-License-Identifier: BSD-3-Clause

__add_sys_prefix_to_path() {
    # In dev-mode CONDA_EXE is python.exe and on Windows
    # it is in a different relative location to condabin.
    if [ -n "${_CE_CONDA}" ] && [ -n "${WINDIR+x}" ]; then
        SYSP=$(\dirname "${CONDA_EXE}")
    else
        SYSP=$(\dirname "${CONDA_EXE}")
        SYSP=$(\dirname "${SYSP}")
    fi

    if [ -n "${WINDIR+x}" ]; then
        PATH="${SYSP}/bin:${PATH}"
        PATH="${SYSP}/Scripts:${PATH}"
        PATH="${SYSP}/Library/bin:${PATH}"
        PATH="${SYSP}/Library/usr/bin:${PATH}"
        PATH="${SYSP}/Library/mingw-w64/bin:${PATH}"
        PATH="${SYSP}:${PATH}"
    else
        PATH="${SYSP}/bin:${PATH}"
    fi
    \export PATH
}

__conda_hashr() {
    if [ -n "${ZSH_VERSION:+x}" ]; then
        \rehash
    elif [ -n "${POSH_VERSION:+x}" ]; then
        :  # pass
    else
        \hash -r
    fi
}

__conda_activate() {
    if [ -n "${CONDA_PS1_BACKUP:+x}" ]; then
        # Handle transition from shell activated with conda <= 4.3 to a subsequent activation
        # after conda updated to >= 4.4. See issue #6173.
        PS1="$CONDA_PS1_BACKUP"
        \unset CONDA_PS1_BACKUP
    fi

    \local cmd="$1"
    shift
    \local ask_conda
    CONDA_INTERNAL_OLDPATH="${PATH}"
    __add_sys_prefix_to_path
    ask_conda="$(PS1="$PS1" "$CONDA_EXE" $_CE_M $_CE_CONDA shell.posix "$cmd" "$@")" || \return $?
    rc=$?
    PATH="${CONDA_INTERNAL_OLDPATH}"
    \eval "$ask_conda"
    if [ $rc != 0 ]; then
        \export PATH
    fi
    __conda_hashr
}

__conda_reactivate() {
    \local ask_conda
    CONDA_INTERNAL_OLDPATH="${PATH}"
    __add_sys_prefix_to_path
    ask_conda="$(PS1="$PS1" "$CONDA_EXE" $_CE_M $_CE_CONDA shell.posix reactivate)" || \return $?
    PATH="${CONDA_INTERNAL_OLDPATH}"
    \eval "$ask_conda"
    __conda_hashr
}

conda() {
    if [ "$#" -lt 1 ]; then
        "$CONDA_EXE" $_CE_M $_CE_CONDA
    else
        \local cmd="$1"
        shift
        case "$cmd" in
            activate|deactivate)
                __conda_activate "$cmd" "$@"
                ;;
            install|update|upgrade|remove|uninstall)
                CONDA_INTERNAL_OLDPATH="${PATH}"
                __add_sys_prefix_to_path
                "$CONDA_EXE" $_CE_M $_CE_CONDA "$cmd" "$@"
                \local t1=$?
                PATH="${CONDA_INTERNAL_OLDPATH}"
                if [ $t1 = 0 ]; then
                    __conda_reactivate
                else
                    return $t1
                fi
                ;;
            *)
                CONDA_INTERNAL_OLDPATH="${PATH}"
                __add_sys_prefix_to_path
                "$CONDA_EXE" $_CE_M $_CE_CONDA "$cmd" "$@"
                \local t1=$?
                PATH="${CONDA_INTERNAL_OLDPATH}"
                return $t1
                ;;
        esac
    fi
}

if [ -z "${CONDA_SHLVL+x}" ]; then
    \export CONDA_SHLVL=0
    # In dev-mode CONDA_EXE is python.exe and on Windows
    # it is in a different relative location to condabin.
    if [ -n "${_CE_CONDA+x}" ] && [ -n "${WINDIR+x}" ]; then
        PATH="$(\dirname "$CONDA_EXE")/condabin${PATH:+":${PATH}"}"
    else
        PATH="$(\dirname "$(\dirname "$CONDA_EXE")")/condabin${PATH:+":${PATH}"}"
    fi
    \export PATH

    # We're not allowing PS1 to be unbound. It must at least be set.
    # However, we're not exporting it, which can cause problems when starting a second shell
    # via a first shell (i.e. starting zsh from bash).
    if [ -z "${PS1+x}" ]; then
        PS1=
    fi
fi

conda activate base
PS1='(base) \[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
export PATH='/usr/local/cuda-11.3/bin:/home/bella/anaconda3/bin:/home/bella/anaconda3/condabin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin'
export CONDA_SHLVL='1'
export CONDA_PROMPT_MODIFIER='(base) '
unset __conda_setup
# <<< conda initialize <<<

export LD_LIBRARY_PATH=~/.mujoco/mujoco200/bin${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
export MUJOCO_KEY_PATH=~/.mujoco${MUJOCO_KEY_PATH}
export PATH=/usr/local/cuda-11.3/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-11.3/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/nvidia
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/nvidia-430

export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libGL.so


(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ curl --version
curl --version
curl 7.68.0 (x86_64-conda_cos6-linux-gnu) libcurl/7.68.0 OpenSSL/1.1.1d zlib/1.2.11 libssh2/1.8.2
Release-Date: 2020-01-08
Protocols: dict file ftp ftps gopher http https imap imaps pop3 pop3s rtsp scp sftp smb smbs smtp smtps telnet tftp 
Features: AsynchDNS GSS-API HTTPS-proxy IPv6 Kerberos Largefile libz NTLM NTLM_WB SPNEGO SSL TLS-SRP UnixSockets
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ bash --version
bash --version
GNU bash，版本 5.0.17(1)-release (x86_64-pc-linux-gnu)
Copyright (C) 2019 Free Software Foundation, Inc.
许可证 GPLv3+: GNU GPL 许可证第三版或者更新版本 <http://gnu.org/licenses/gpl.html>

本软件是自由软件，您可以自由地更改和重新发布。
在法律许可的情况下特此明示，本软件不提供任何担保。
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ ./run.sh -h
./run.sh -h
Run Berti Artificat
Options: 
 -h: help
 -v: verbose mode
 -p [num]: run using [num] threads
 -g: build GCC7.5 from scratch
 -d: compile with docker
 -c: clean all generated files (traces and gcc7.5)
 -l: generate a log for debug purpose
 -r: always download SPEC CPU2K17 traces
 -n: no build the simulator
 -f: execute GAP, CloudSuite, and Multi-Level prefetcher
 -m: execute 4-Core
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ conda deactivate
conda deactivate
export PATH='/usr/local/cuda-11.3/bin:/usr/local/cuda-11.3/bin:/home/bella/anaconda3/condabin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin'
unset CONDA_PREFIX
unset CONDA_DEFAULT_ENV
unset CONDA_PROMPT_MODIFIER
PS1='\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
export CONDA_SHLVL='0'
export CONDA_EXE='/home/bella/anaconda3/bin/conda'
export _CE_M=''
export _CE_CONDA=''
export CONDA_PYTHON_EXE='/home/bella/anaconda3/bin/python'
bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ python --version
python --version

Command 'python' not found, did you mean:

  command 'python3' from deb python3
  command 'python' from deb python-is-python3

bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ python3 --version
python3 --version
Python 3.8.10
bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ ls
ls
4core.in  compile_gcc.sh        format_cloudsuite.sh  Python     run.sh
ChampSim  download_spec2k17.sh  LICENSE               README.md
bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ ./run.sh -d -p 127
./run.sh -d -p 127
Building with Docker
Running in Parallel

Download SPEC CPU2017 traces [0/44] 
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [1/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [2/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [3/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [4/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [5/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [6/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [7/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [8/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [9/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [10/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [11/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [12/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [13/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [14/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [15/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [16/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [17/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [18/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [19/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [20/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [21/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [22/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [23/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [24/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [25/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [26/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [27/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [28/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [29/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [30/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [31/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [32/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [33/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [34/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [35/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [36/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [37/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [38/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [39/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [40/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [41/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [42/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [43/44]
./download_spec2k17.sh: 行 75: curl：未找到命令Download SPEC CPU2017 traces [44/44]
Download SPEC CPU2017 traces [44/44]
Building Berti... ERROR
bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ curl --help
curl --help

Command 'curl' not found, but can be installed with:

sudo apt install curl

bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ curl --version
curl --version

Command 'curl' not found, but can be installed with:

sudo apt install curl

bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ conda activate base
conda activate base
PS1='(base) \[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
export PATH='/home/bella/anaconda3/bin:/usr/local/cuda-11.3/bin:/usr/local/cuda-11.3/bin:/home/bella/anaconda3/condabin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin'
export CONDA_PREFIX='/home/bella/anaconda3'
export CONDA_SHLVL='1'
export CONDA_DEFAULT_ENV='base'
export CONDA_PROMPT_MODIFIER='(base) '
export CONDA_EXE='/home/bella/anaconda3/bin/conda'
export _CE_M=''
export _CE_CONDA=''
export CONDA_PYTHON_EXE='/home/bella/anaconda3/bin/python'
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ curl --version
curl --version
curl 7.68.0 (x86_64-conda_cos6-linux-gnu) libcurl/7.68.0 OpenSSL/1.1.1d zlib/1.2.11 libssh2/1.8.2
Release-Date: 2020-01-08
Protocols: dict file ftp ftps gopher http https imap imaps pop3 pop3s rtsp scp sftp smb smbs smtp smtps telnet tftp 
Features: AsynchDNS GSS-API HTTPS-proxy IPv6 Kerberos Largefile libz NTLM NTLM_WB SPNEGO SSL TLS-SRP UnixSockets
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ ./run.sh -d -p 127
./run.sh -d -p 127
Building with Docker
Running in Parallel

(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ ./run.sh -d -p 127
./run.sh -d -p 127
Building with Docker
Running in Parallel

Building Berti... ERROR
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ ./download_spec2k17.sh 
./download_spec2k17.sh 
Download SPEC CPU2017 traces [0/44] 
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [1/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [2/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [3/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [4/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [5/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [6/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [7/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [8/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [9/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [10/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [11/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [12/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [13/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [14/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [15/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [16/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [17/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [18/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [19/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [20/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [21/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [22/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [23/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [24/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [25/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [26/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [27/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [28/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [29/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [30/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [31/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [32/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [33/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [34/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [35/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [36/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [37/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [38/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [39/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [40/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [41/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [42/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [43/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [44/44]
Download SPEC CPU2017 traces [44/44]
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ ./run -d -p 127
./run -d -p 127
bash: ./run: 没有那个文件或目录
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ ./run.sh -d -p 127
./run.sh -d -p 127
Building with Docker
Running in Parallel

Building Berti... ERROR
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ ./run.sh -d -p 127
./run.sh -d -p 127
Building with Docker
Running in Parallel

Download SPEC CPU2017 traces [0/44] 
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [1/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [2/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [3/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [4/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [5/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [6/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [7/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [8/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [9/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [10/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [11/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [12/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [13/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [14/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [15/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [16/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [17/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [18/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [19/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [20/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [21/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [22/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [23/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [24/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [25/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [26/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [27/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [28/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [29/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [30/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [31/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [32/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [33/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [34/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [35/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [36/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [37/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [38/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [39/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [40/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [41/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [42/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [43/44]
curl: (6) Could not resolve host: hpca23.cse.tamu.eduDownload SPEC CPU2017 traces [44/44]
Download SPEC CPU2017 traces [44/44]
Building Berti... ERROR
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ cd .
cd .
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ cd ..
cd ..
(base) bella@bella-v:~/Downloads/IPCP20$ ls
ls
Berti-MICRO2022-main      ChampSim-master      IPCP_ISCA2020-master
Berti-MICRO2022-main.zip  ChampSim-master.zip  IPCP_ISCA2020-master.zip
(base) bella@bella-v:~/Downloads/IPCP20$ cd Champwords=("${@:3:2}")
cword="$3"
cur="$3"
cur="$3"
cword="$3"
prev="$3"
words=("${@:3:2}")


(base) bella@bella-v:~/Downloads/IPCP20$ cd ChampSim-master
cd ChampSim-master
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ ./config.sh <configuration file>
./config.sh <configuration file>
bash: 未预期的符号“newline”附近有语法错误
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$c
./config.sh champsim_config.json
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ ./config.sh
./config.sh
No configuration specified. Building default ChampSim with no prefetching.
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ ./config.sh <champsim_config.json>
./config.sh <champsim_config.json>
bash: 未预期的符号“newline”附近有语法错误
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ make
make
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/ptw.o src/ptw.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/tracereader.o src/tracereader.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/ooo_cpu.o src/ooo_cpu.cc
src/ooo_cpu.cc: In member function ‘void O3_CPU::init_instruction(ooo_model_instr)’:
src/ooo_cpu.cc:112:21: warning: comparison of integer expressions of different signedness: ‘int’ and ‘const size_t’ {aka ‘const long unsigned int’} [-Wsign-compare]
  112 |   for (int i = 0; i < NUM_INSTR_SOURCES; i++) {
      |                   ~~^~~~~~~~~~~~~~~~~~~
src/ooo_cpu.cc:262:23: warning: comparison of integer expressions of different signedness: ‘int’ and ‘const size_t’ {aka ‘const long unsigned int’} [-Wsign-compare]
  262 |     for (int i = 0; i < NUM_INSTR_SOURCES; i++) {
      |                     ~~^~~~~~~~~~~~~~~~~~~
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/main.o src/main.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/cache.o src/cache.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/dram_controller.o src/dram_controller.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/vmem.o src/vmem.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/core_inst.o src/core_inst.cc
g++ -Wall -O3 -std=c++17 -Ireplacement/lru -Dinitialize_replacement=repl_rreplacementDlru_initialize -Dfind_victim=repl_rreplacementDlru_victim -Dupdate_replacement_state=repl_rreplacementDlru_update -Dreplacement_final_stats=repl_rreplacementDlru_final_stats -Iinc -MMD -MP  -c -o replacement/lru/lru.o replacement/lru/lru.cc
ar -rcs obj/repl_rreplacementDlru.a replacement/lru/lru.o
g++ -Wall -O3 -std=c++17 -Iprefetcher/no -Dprefetcher_initialize=pref_pprefetcherDno_initialize -Dprefetcher_cache_operate=pref_pprefetcherDno_cache_operate -Dprefetcher_cache_fill=pref_pprefetcherDno_cache_fill -Dprefetcher_cycle_operate=pref_pprefetcherDno_cycle_operate -Dprefetcher_final_stats=pref_pprefetcherDno_final_stats -Dl1d_prefetcher_initialize=pref_pprefetcherDno_initialize -Dl2c_prefetcher_initialize=pref_pprefetcherDno_initialize -Dllc_prefetcher_initialize=pref_pprefetcherDno_initialize -Dl1d_prefetcher_operate=pref_pprefetcherDno_cache_operate -Dl2c_prefetcher_operate=pref_pprefetcherDno_cache_operate -Dllc_prefetcher_operate=pref_pprefetcherDno_cache_operate -Dl1d_prefetcher_cache_fill=pref_pprefetcherDno_cache_fill -Dl2c_prefetcher_cache_fill=pref_pprefetcherDno_cache_fill -Dllc_prefetcher_cache_fill=pref_pprefetcherDno_cache_fill -Dl1d_prefetcher_final_stats=pref_pprefetcherDno_final_stats -Dl2c_prefetcher_final_stats=pref_pprefetcherDno_final_stats -Dllc_prefetcher_final_stats=pref_pprefetcherDno_final_stats -Iinc -MMD -MP  -c -o prefetcher/no/no.o prefetcher/no/no.cc
ar -rcs obj/pref_pprefetcherDno.a prefetcher/no/no.o
g++ -Wall -O3 -std=c++17 -Iprefetcher/no_instr -Dprefetcher_initialize=pref_pprefetcherDno_instr_initialize -Dprefetcher_branch_operate=pref_pprefetcherDno_instr_branch_operate -Dprefetcher_cache_operate=pref_pprefetcherDno_instr_cache_operate -Dprefetcher_cycle_operate=pref_pprefetcherDno_instr_cycle_operate -Dprefetcher_cache_fill=pref_pprefetcherDno_instr_cache_fill -Dprefetcher_final_stats=pref_pprefetcherDno_instr_final_stats -Dl1i_prefetcher_initialize=pref_pprefetcherDno_instr_initialize -Dl1i_prefetcher_branch_operate=pref_pprefetcherDno_instr_branch_operate -Dl1i_prefetcher_cache_operate=pref_pprefetcherDno_instr_cache_operate -Dl1i_prefetcher_cycle_operate=pref_pprefetcherDno_instr_cycle_operate -Dl1i_prefetcher_cache_fill=pref_pprefetcherDno_instr_cache_fill -Dl1i_prefetcher_final_stats=pref_pprefetcherDno_instr_final_stats -Iinc -MMD -MP  -c -o prefetcher/no_instr/no.o prefetcher/no_instr/no.cc
ar -rcs obj/pref_pprefetcherDno_instr.a prefetcher/no_instr/no.o
g++ -Wall -O3 -std=c++17 -Ibranch/bimodal -Dinitialize_branch_predictor=bpred_bbranchDbimodal_initialize -Dlast_branch_result=bpred_bbranchDbimodal_last_result -Dpredict_branch=bpred_bbranchDbimodal_predict -Iinc -MMD -MP  -c -o branch/bimodal/bimodal.o branch/bimodal/bimodal.cc
ar -rcs obj/bpred_bbranchDbimodal.a branch/bimodal/bimodal.o
g++ -Wall -O3 -std=c++17 -Ibtb/basic_btb -Dinitialize_btb=btb_bbtbDbasic_btb_initialize -Dupdate_btb=btb_bbtbDbasic_btb_update -Dbtb_prediction=btb_bbtbDbasic_btb_predict -Iinc -MMD -MP  -c -o btb/basic_btb/basic_btb.o btb/basic_btb/basic_btb.cc
ar -rcs obj/btb_bbtbDbasic_btb.a btb/basic_btb/basic_btb.o
g++  -o bin/champsim src/ptw.o src/tracereader.o src/ooo_cpu.o src/main.o src/cache.o src/dram_controller.o src/vmem.o src/core_inst.o obj/repl_rreplacementDlru.a obj/pref_pprefetcherDno.a obj/pref_pprefetcherDno_instr.a obj/bpred_bbranchDbimodal.a obj/btb_bbtbDbasic_btb.a 
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ bin/champsim --warmup_instructions 200000000 --simulation_instructions 500000000 ~/path/to/traces/600.perlbench_s-210B.champsimtrace.xz
bin/champsim --warmup_instructions 200000000 --simulation_instructions 500000000 ~/path/to/traces/600.perlbench_s-210B.champsimtrace.xz

*** ChampSim Multicore Out-of-Order Simulator ***

Warmup Instructions: 200000000
Simulation Instructions: 500000000
Number of CPUs: 1
Off-chip DRAM Size: 4 GiB Channels: 1 Width: 64-bit Data Rate: 3200 MT/s

VirtualMemory physical capacity: 8588881920 num_ppages: 2096895
VirtualMemory page size: 4096 log2_page_size: 12

CPU 0 runs /home/bella/path/to/traces/600.perlbench_s-210B.champsimtrace.xz
TRACE FILE NOT FOUND
champsim: src/tracereader.cc:43: tracereader::tracereader(uint8_t, std::string): Assertion `0' failed.
已放弃 (核心已转储)
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ bin/champsim --warmup_instructions 200000000 --simulation_instructions 500000000 ~/path/to/traces/400.perlbench-41B.champsimtrace.xz
bin/champsim --warmup_instructions 200000000 --simulation_instructions 500000000 ~/path/to/traces/400.perlbench-41B.champsimtrace.xz

*** ChampSim Multicore Out-of-Order Simulator ***

Warmup Instructions: 200000000
Simulation Instructions: 500000000
Number of CPUs: 1
Off-chip DRAM Size: 4 GiB Channels: 1 Width: 64-bit Data Rate: 3200 MT/s

VirtualMemory physical capacity: 8588881920 num_ppages: 2096895
VirtualMemory page size: 4096 log2_page_size: 12

CPU 0 runs /home/bella/path/to/traces/400.perlbench-41B.champsimtrace.xz
CPU 0 Bimodal branch predictor
Basic BTB sets: 1024 ways: 8 indirect buffer size: 4096 RAS size: 64
Heartbeat CPU 0 instructions: 10000001 cycles: 2501286 heartbeat IPC: 3.99794 cumulative IPC: 3.99794 (Simulation time: 0 hr 0 min 24 sec) 
Heartbeat CPU 0 instructions: 20000003 cycles: 5105895 heartbeat IPC: 3.83935 cumulative IPC: 3.91704 (Simulation time: 0 hr 0 min 49 sec) 
Heartbeat CPU 0 instructions: 30000003 cycles: 7605895 heartbeat IPC: 4 cumulative IPC: 3.94431 (Simulation time: 0 hr 1 min 11 sec) 
Heartbeat CPU 0 instructions: 40000003 cycles: 10105895 heartbeat IPC: 4 cumulative IPC: 3.95809 (Simulation time: 0 hr 1 min 33 sec) 
Heartbeat CPU 0 instructions: 50000003 cycles: 12605895 heartbeat IPC: 4 cumulative IPC: 3.9664 (Simulation time: 0 hr 1 min 56 sec) 
Heartbeat CPU 0 instructions: 60000003 cycles: 15105895 heartbeat IPC: 4 cumulative IPC: 3.97196 (Simulation time: 0 hr 2 min 18 sec) 
Heartbeat CPU 0 instructions: 70000003 cycles: 17605895 heartbeat IPC: 4 cumulative IPC: 3.97594 (Simulation time: 0 hr 2 min 40 sec) 
Heartbeat CPU 0 instructions: 80000003 cycles: 20105895 heartbeat IPC: 4 cumulative IPC: 3.97893 (Simulation time: 0 hr 3 min 2 sec) 
Heartbeat CPU 0 instructions: 90000003 cycles: 22605895 heartbeat IPC: 4 cumulative IPC: 3.98126 (Simulation time: 0 hr 3 min 24 sec) 
Heartbeat CPU 0 instructions: 100000003 cycles: 25105895 heartbeat IPC: 4 cumulative IPC: 3.98313 (Simulation time: 0 hr 3 min 46 sec) 
Heartbeat CPU 0 instructions: 110000003 cycles: 27605895 heartbeat IPC: 4 cumulative IPC: 3.98466 (Simulation time: 0 hr 4 min 9 sec) 
Heartbeat CPU 0 instructions: 120000003 cycles: 30105895 heartbeat IPC: 4 cumulative IPC: 3.98593 (Simulation time: 0 hr 4 min 31 sec) 
Heartbeat CPU 0 instructions: 130000003 cycles: 32605895 heartbeat IPC: 4 cumulative IPC: 3.98701 (Simulation time: 0 hr 4 min 54 sec) 
Heartbeat CPU 0 instructions: 140000003 cycles: 35105895 heartbeat IPC: 4 cumulative IPC: 3.98793 (Simulation time: 0 hr 5 min 17 sec) 
Heartbeat CPU 0 instructions: 150000003 cycles: 37605895 heartbeat IPC: 4 cumulative IPC: 3.98874 (Simulation time: 0 hr 5 min 39 sec) 
Heartbeat CPU 0 instructions: 160000003 cycles: 40105903 heartbeat IPC: 3.99999 cumulative IPC: 3.98944 (Simulation time: 0 hr 6 min 1 sec) 
Heartbeat CPU 0 instructions: 170000003 cycles: 42606773 heartbeat IPC: 3.99861 cumulative IPC: 3.98998 (Simulation time: 0 hr 6 min 24 sec) 
Heartbeat CPU 0 instructions: 180000000 cycles: 45117533 heartbeat IPC: 3.98286 cumulative IPC: 3.98958 (Simulation time: 0 hr 6 min 48 sec) 
Heartbeat CPU 0 instructions: 190000000 cycles: 47849116 heartbeat IPC: 3.66088 cumulative IPC: 3.97082 (Simulation time: 0 hr 7 min 15 sec) 
Heartbeat CPU 0 instructions: 200000000 cycles: 50349116 heartbeat IPC: 4 cumulative IPC: 3.97226 (Simulation time: 0 hr 7 min 38 sec) 

Warmup complete CPU 0 instructions: 200000004 cycles: 50349117 (Simulation time: 0 hr 7 min 38 sec) 

Heartbeat CPU 0 instructions: 210000002 cycles: 59841792 heartbeat IPC: 1.05344 cumulative IPC: 1.05344 (Simulation time: 0 hr 8 min 4 sec) 
Heartbeat CPU 0 instructions: 220000001 cycles: 69651120 heartbeat IPC: 1.01944 cumulative IPC: 1.03616 (Simulation time: 0 hr 8 min 29 sec) 
Heartbeat CPU 0 instructions: 230000003 cycles: 78387860 heartbeat IPC: 1.14459 cumulative IPC: 1.06995 (Simulation time: 0 hr 8 min 53 sec) 
Heartbeat CPU 0 instructions: 240000003 cycles: 87713957 heartbeat IPC: 1.07226 cumulative IPC: 1.07053 (Simulation time: 0 hr 9 min 20 sec) 
Heartbeat CPU 0 instructions: 250000003 cycles: 97231140 heartbeat IPC: 1.05073 cumulative IPC: 1.06651 (Simulation time: 0 hr 9 min 46 sec) 
Heartbeat CPU 0 instructions: 260000000 cycles: 106570059 heartbeat IPC: 1.07079 cumulative IPC: 1.06722 (Simulation time: 0 hr 10 min 10 sec) 
Heartbeat CPU 0 instructions: 270000002 cycles: 116476039 heartbeat IPC: 1.00949 cumulative IPC: 1.05857 (Simulation time: 0 hr 10 min 36 sec) 
Heartbeat CPU 0 instructions: 280000000 cycles: 125814061 heartbeat IPC: 1.07089 cumulative IPC: 1.06009 (Simulation time: 0 hr 11 min 1 sec) 
Heartbeat CPU 0 instructions: 290000000 cycles: 136275825 heartbeat IPC: 0.955862 cumulative IPC: 1.0474 (Simulation time: 0 hr 11 min 28 sec) 
Heartbeat CPU 0 instructions: 300000003 cycles: 145743791 heartbeat IPC: 1.05619 cumulative IPC: 1.04828 (Simulation time: 0 hr 11 min 54 sec) 
Heartbeat CPU 0 instructions: 310000002 cycles: 155184187 heartbeat IPC: 1.05928 cumulative IPC: 1.04927 (Simulation time: 0 hr 12 min 20 sec) 
Heartbeat CPU 0 instructions: 320000000 cycles: 164827435 heartbeat IPC: 1.03699 cumulative IPC: 1.04823 (Simulation time: 0 hr 12 min 45 sec) 
Heartbeat CPU 0 instructions: 330000002 cycles: 173909025 heartbeat IPC: 1.10113 cumulative IPC: 1.05212 (Simulation time: 0 hr 13 min 9 sec) 
Heartbeat CPU 0 instructions: 340000001 cycles: 188771781 heartbeat IPC: 0.672823 cumulative IPC: 1.0114 (Simulation time: 0 hr 13 min 42 sec) 
Heartbeat CPU 0 instructions: 350000002 cycles: 203333778 heartbeat IPC: 0.686719 cumulative IPC: 0.98049 (Simulation time: 0 hr 14 min 20 sec) 
Heartbeat CPU 0 instructions: 360000002 cycles: 218998210 heartbeat IPC: 0.638389 cumulative IPC: 0.948715 (Simulation time: 0 hr 14 min 55 sec) 
Heartbeat CPU 0 instructions: 370000002 cycles: 228701113 heartbeat IPC: 1.03062 cumulative IPC: 0.953171 (Simulation time: 0 hr 15 min 22 sec) 
Heartbeat CPU 0 instructions: 380000004 cycles: 238854564 heartbeat IPC: 0.984887 cumulative IPC: 0.95488 (Simulation time: 0 hr 15 min 47 sec) 
Heartbeat CPU 0 instructions: 390000001 cycles: 248424728 heartbeat IPC: 1.04491 cumulative IPC: 0.95923 (Simulation time: 0 hr 16 min 14 sec) 
Heartbeat CPU 0 instructions: 400000002 cycles: 258569330 heartbeat IPC: 0.985746 cumulative IPC: 0.960522 (Simulation time: 0 hr 16 min 39 sec) 
Heartbeat CPU 0 instructions: 410000001 cycles: 267907118 heartbeat IPC: 1.07092 cumulative IPC: 0.96526 (Simulation time: 0 hr 17 min 5 sec) 
Heartbeat CPU 0 instructions: 420000000 cycles: 277191069 heartbeat IPC: 1.07713 cumulative IPC: 0.969838 (Simulation time: 0 hr 17 min 29 sec) 
Heartbeat CPU 0 instructions: 430000004 cycles: 286686306 heartbeat IPC: 1.05316 cumulative IPC: 0.973186 (Simulation time: 0 hr 17 min 58 sec) 
Heartbeat CPU 0 instructions: 440000001 cycles: 296459045 heartbeat IPC: 1.02325 cumulative IPC: 0.975174 (Simulation time: 0 hr 18 min 23 sec) 
Heartbeat CPU 0 instructions: 450000003 cycles: 306128990 heartbeat IPC: 1.03413 cumulative IPC: 0.977403 (Simulation time: 0 hr 18 min 48 sec) 
Heartbeat CPU 0 instructions: 460000001 cycles: 315584157 heartbeat IPC: 1.05762 cumulative IPC: 0.980263 (Simulation time: 0 hr 19 min 13 sec) 
Heartbeat CPU 0 instructions: 470000002 cycles: 325829081 heartbeat IPC: 0.976093 cumulative IPC: 0.980108 (Simulation time: 0 hr 19 min 40 sec) 
Heartbeat CPU 0 instructions: 480000004 cycles: 335425398 heartbeat IPC: 1.04207 cumulative IPC: 0.982193 (Simulation time: 0 hr 20 min 4 sec) 
Heartbeat CPU 0 instructions: 490000000 cycles: 345143502 heartbeat IPC: 1.02901 cumulative IPC: 0.983737 (Simulation time: 0 hr 20 min 31 sec) 
Heartbeat CPU 0 instructions: 500000002 cycles: 355394061 heartbeat IPC: 0.975557 cumulative IPC: 0.983462 (Simulation time: 0 hr 20 min 56 sec) 
Heartbeat CPU 0 instructions: 510000004 cycles: 366198408 heartbeat IPC: 0.925554 cumulative IPC: 0.981481 (Simulation time: 0 hr 21 min 22 sec) 
Heartbeat CPU 0 instructions: 520000004 cycles: 375637141 heartbeat IPC: 1.05946 cumulative IPC: 0.983744 (Simulation time: 0 hr 21 min 49 sec) 
Heartbeat CPU 0 instructions: 530000003 cycles: 385595189 heartbeat IPC: 1.00421 cumulative IPC: 0.984352 (Simulation time: 0 hr 22 min 16 sec) 
Heartbeat CPU 0 instructions: 540000001 cycles: 395508328 heartbeat IPC: 1.00876 cumulative IPC: 0.985053 (Simulation time: 0 hr 22 min 40 sec) 
Heartbeat CPU 0 instructions: 550000002 cycles: 404758841 heartbeat IPC: 1.08102 cumulative IPC: 0.987558 (Simulation time: 0 hr 23 min 5 sec) 
Heartbeat CPU 0 instructions: 560000001 cycles: 414263413 heartbeat IPC: 1.05213 cumulative IPC: 0.989244 (Simulation time: 0 hr 23 min 28 sec) 
Heartbeat CPU 0 instructions: 570000002 cycles: 426074891 heartbeat IPC: 0.846634 cumulative IPC: 0.984761 (Simulation time: 0 hr 23 min 57 sec) 
Heartbeat CPU 0 instructions: 580000000 cycles: 442951736 heartbeat IPC: 0.592528 cumulative IPC: 0.9679 (Simulation time: 0 hr 24 min 32 sec) 
Heartbeat CPU 0 instructions: 590000000 cycles: 459770259 heartbeat IPC: 0.594583 cumulative IPC: 0.952564 (Simulation time: 0 hr 25 min 7 sec) 
Heartbeat CPU 0 instructions: 600000001 cycles: 468663250 heartbeat IPC: 1.12448 cumulative IPC: 0.956219 (Simulation time: 0 hr 25 min 30 sec) 
Heartbeat CPU 0 instructions: 610000000 cycles: 478034392 heartbeat IPC: 1.06711 cumulative IPC: 0.958649 (Simulation time: 0 hr 25 min 54 sec) 
Heartbeat CPU 0 instructions: 620000001 cycles: 487976484 heartbeat IPC: 1.00582 cumulative IPC: 0.959721 (Simulation time: 0 hr 26 min 16 sec) 
Heartbeat CPU 0 instructions: 630000004 cycles: 497262145 heartbeat IPC: 1.07693 cumulative IPC: 0.962156 (Simulation time: 0 hr 26 min 38 sec) 
Heartbeat CPU 0 instructions: 640000000 cycles: 506790687 heartbeat IPC: 1.04948 cumulative IPC: 0.963979 (Simulation time: 0 hr 27 min 2 sec) 
Heartbeat CPU 0 instructions: 650000000 cycles: 516345218 heartbeat IPC: 1.04662 cumulative IPC: 0.965673 (Simulation time: 0 hr 27 min 25 sec) 
Heartbeat CPU 0 instructions: 660000000 cycles: 524990479 heartbeat IPC: 1.1567 cumulative IPC: 0.969153 (Simulation time: 0 hr 27 min 47 sec) 
Heartbeat CPU 0 instructions: 670000000 cycles: 533364053 heartbeat IPC: 1.19423 cumulative IPC: 0.973055 (Simulation time: 0 hr 28 min 8 sec) 
Heartbeat CPU 0 instructions: 680000000 cycles: 542500581 heartbeat IPC: 1.09451 cumulative IPC: 0.975309 (Simulation time: 0 hr 28 min 31 sec) 
Heartbeat CPU 0 instructions: 690000000 cycles: 551625813 heartbeat IPC: 1.09586 cumulative IPC: 0.977504 (Simulation time: 0 hr 28 min 56 sec) 
Heartbeat CPU 0 instructions: 700000002 cycles: 561075564 heartbeat IPC: 1.05823 cumulative IPC: 0.978998 (Simulation time: 0 hr 29 min 17 sec) 
Finished CPU 0 instructions: 500000001 cycles: 510726456 cumulative IPC: 0.978998 (Simulation time: 0 hr 29 min 17 sec) 

ChampSim completed all CPUs

Region of Interest Statistics

CPU 0 cumulative IPC: 0.978998 instructions: 500000001 cycles: 510726456
cpu0_DTLB TOTAL     ACCESS:  109291560  HIT:  108951474  MISS:     340086
cpu0_DTLB LOAD      ACCESS:   72998395  HIT:   72707241  MISS:     291154
cpu0_DTLB RFO       ACCESS:   36293165  HIT:   36244233  MISS:      48932
cpu0_DTLB PREFETCH  ACCESS:          0  HIT:          0  MISS:          0
cpu0_DTLB WRITEBACK ACCESS:          0  HIT:          0  MISS:          0
cpu0_DTLB TRANSLATION ACCESS:          0  HIT:          0  MISS:          0
cpu0_DTLB PREFETCH  REQUESTED:          0  ISSUED:          0  USEFUL:          0  USELESS:          0
cpu0_DTLB AVERAGE MISS LATENCY: 9.50998 cycles
cpu0_ITLB TOTAL     ACCESS:   46933274  HIT:   46920728  MISS:      12546
cpu0_ITLB LOAD      ACCESS:   46933274  HIT:   46920728  MISS:      12546
cpu0_ITLB RFO       ACCESS:          0  HIT:          0  MISS:          0
cpu0_ITLB PREFETCH  ACCESS:          0  HIT:          0  MISS:          0
cpu0_ITLB WRITEBACK ACCESS:          0  HIT:          0  MISS:          0
cpu0_ITLB TRANSLATION ACCESS:          0  HIT:          0  MISS:          0
cpu0_ITLB PREFETCH  REQUESTED:          0  ISSUED:          0  USEFUL:          0  USELESS:          0
cpu0_ITLB AVERAGE MISS LATENCY: 9.47896 cycles
cpu0_L1I TOTAL     ACCESS:   21406947  HIT:   21064798  MISS:     342149
cpu0_L1I LOAD      ACCESS:   21406947  HIT:   21064798  MISS:     342149
cpu0_L1I RFO       ACCESS:          0  HIT:          0  MISS:          0
cpu0_L1I PREFETCH  ACCESS:          0  HIT:          0  MISS:          0
cpu0_L1I WRITEBACK ACCESS:          0  HIT:          0  MISS:          0
cpu0_L1I TRANSLATION ACCESS:          0  HIT:          0  MISS:          0
cpu0_L1I PREFETCH  REQUESTED:          0  ISSUED:          0  USEFUL:          0  USELESS:          0
cpu0_L1I AVERAGE MISS LATENCY: 15.6681 cycles
cpu0_STLB TOTAL     ACCESS:     352632  HIT:     336775  MISS:      15857
cpu0_STLB LOAD      ACCESS:     303700  HIT:     289486  MISS:      14214
cpu0_STLB RFO       ACCESS:      48932  HIT:      47289  MISS:       1643
cpu0_STLB PREFETCH  ACCESS:          0  HIT:          0  MISS:          0
cpu0_STLB WRITEBACK ACCESS:          0  HIT:          0  MISS:          0
cpu0_STLB TRANSLATION ACCESS:          0  HIT:          0  MISS:          0
cpu0_STLB PREFETCH  REQUESTED:          0  ISSUED:          0  USEFUL:          0  USELESS:          0
cpu0_STLB AVERAGE MISS LATENCY: 11.1868 cycles
cpu0_L1D TOTAL     ACCESS:  136336562  HIT:  135914932  MISS:     421630
cpu0_L1D LOAD      ACCESS:   69773983  HIT:   69392663  MISS:     381320
cpu0_L1D RFO       ACCESS:   66546764  HIT:   66508005  MISS:      38759
cpu0_L1D PREFETCH  ACCESS:          0  HIT:          0  MISS:          0
cpu0_L1D WRITEBACK ACCESS:          0  HIT:          0  MISS:          0
cpu0_L1D TRANSLATION ACCESS:      15815  HIT:      14264  MISS:       1551
cpu0_L1D PREFETCH  REQUESTED:          0  ISSUED:          0  USEFUL:          0  USELESS:          0
cpu0_L1D AVERAGE MISS LATENCY: 85.7723 cycles
cpu0_L2C TOTAL     ACCESS:     872860  HIT:     638836  MISS:     234024
cpu0_L2C LOAD      ACCESS:     723457  HIT:     508190  MISS:     215267
cpu0_L2C RFO       ACCESS:      38758  HIT:      20756  MISS:      18002
cpu0_L2C PREFETCH  ACCESS:          0  HIT:          0  MISS:          0
cpu0_L2C WRITEBACK ACCESS:     109094  HIT:     108421  MISS:        673
cpu0_L2C TRANSLATION ACCESS:       1551  HIT:       1469  MISS:         82
cpu0_L2C PREFETCH  REQUESTED:          0  ISSUED:          0  USEFUL:          0  USELESS:          0
cpu0_L2C AVERAGE MISS LATENCY: 141.498 cycles
LLC TOTAL     ACCESS:     279565  HIT:      91694  MISS:     187871
LLC LOAD      ACCESS:     215267  HIT:      40092  MISS:     175175
LLC RFO       ACCESS:      18002  HIT:       5992  MISS:      12010
LLC PREFETCH  ACCESS:          0  HIT:          0  MISS:          0
LLC WRITEBACK ACCESS:      46214  HIT:      45552  MISS:        662
LLC TRANSLATION ACCESS:         82  HIT:         58  MISS:         24
LLC PREFETCH  REQUESTED:          0  ISSUED:          0  USEFUL:          0  USELESS:          0
LLC AVERAGE MISS LATENCY: 150.175 cycles

DRAM Statistics
 CHANNEL 0
 RQ ROW_BUFFER_HIT:      26691  ROW_BUFFER_MISS:     160510
 DBUS AVG_CONGESTED_CYCLE:    3.83137
 WQ ROW_BUFFER_HIT:      19972  ROW_BUFFER_MISS:      12843  FULL:          0


CPU 0 Branch Prediction Accuracy: 93.861% MPKI: 12.7172 Average ROB Occupancy at Mispredict: 41.6894
Branch type MPKI
BRANCH_DIRECT_JUMP: 0.00021
BRANCH_INDIRECT: 0.334994
BRANCH_CONDITIONAL: 12.2144
BRANCH_DIRECT_CALL: 0.000294
BRANCH_INDIRECT_CALL: 0.165144
BRANCH_RETURN: 0.002222








(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ make
make
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/ptw.o src/ptw.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/ooo_cpu.o src/ooo_cpu.cc
src/ooo_cpu.cc: In member function ‘void O3_CPU::init_instruction(ooo_model_instr)’:
src/ooo_cpu.cc:112:21: warning: comparison of integer expressions of different signedness: ‘int’ and ‘const size_t’ {aka ‘const long unsigned int’} [-Wsign-compare]
  112 |   for (int i = 0; i < NUM_INSTR_SOURCES; i++) {
      |                   ~~^~~~~~~~~~~~~~~~~~~
src/ooo_cpu.cc:262:23: warning: comparison of integer expressions of different signedness: ‘int’ and ‘const size_t’ {aka ‘const long unsigned int’} [-Wsign-compare]
  262 |     for (int i = 0; i < NUM_INSTR_SOURCES; i++) {
      |                     ~~^~~~~~~~~~~~~~~~~~~
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/main.o src/main.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/cache.o src/cache.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/vmem.o src/vmem.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/dram_controller.o src/dram_controller.cc
g++ -Wall -O3 -std=c++17 -Iinc -MMD -MP  -c -o src/core_inst.o src/core_inst.cc
g++ -Wall -O3 -std=c++17 -Ireplacement/lru -Dinitialize_replacement=repl_rreplacementDlru_initialize -Dfind_victim=repl_rreplacementDlru_victim -Dupdate_replacement_state=repl_rreplacementDlru_update -Dreplacement_final_stats=repl_rreplacementDlru_final_stats -Iinc -MMD -MP  -c -o replacement/lru/lru.o replacement/lru/lru.cc
ar -rcs obj/repl_rreplacementDlru.a replacement/lru/lru.o
g++ -Wall -O3 -std=c++17 -Iprefetcher/no -Dprefetcher_initialize=pref_pprefetcherDno_initialize -Dprefetcher_cache_operate=pref_pprefetcherDno_cache_operate -Dprefetcher_cache_fill=pref_pprefetcherDno_cache_fill -Dprefetcher_cycle_operate=pref_pprefetcherDno_cycle_operate -Dprefetcher_final_stats=pref_pprefetcherDno_final_stats -Dl1d_prefetcher_initialize=pref_pprefetcherDno_initialize -Dl2c_prefetcher_initialize=pref_pprefetcherDno_initialize -Dllc_prefetcher_initialize=pref_pprefetcherDno_initialize -Dl1d_prefetcher_operate=pref_pprefetcherDno_cache_operate -Dl2c_prefetcher_operate=pref_pprefetcherDno_cache_operate -Dllc_prefetcher_operate=pref_pprefetcherDno_cache_operate -Dl1d_prefetcher_cache_fill=pref_pprefetcherDno_cache_fill -Dl2c_prefetcher_cache_fill=pref_pprefetcherDno_cache_fill -Dllc_prefetcher_cache_fill=pref_pprefetcherDno_cache_fill -Dl1d_prefetcher_final_stats=pref_pprefetcherDno_final_stats -Dl2c_prefetcher_final_stats=pref_pprefetcherDno_final_stats -Dllc_prefetcher_final_stats=pref_pprefetcherDno_final_stats -Iinc -MMD -MP  -c -o prefetcher/no/no.o prefetcher/no/no.cc
ar -rcs obj/pref_pprefetcherDno.a prefetcher/no/no.o
g++ -Wall -O3 -std=c++17 -Iprefetcher/no_instr -Dprefetcher_initialize=pref_pprefetcherDno_instr_initialize -Dprefetcher_branch_operate=pref_pprefetcherDno_instr_branch_operate -Dprefetcher_cache_operate=pref_pprefetcherDno_instr_cache_operate -Dprefetcher_cycle_operate=pref_pprefetcherDno_instr_cycle_operate -Dprefetcher_cache_fill=pref_pprefetcherDno_instr_cache_fill -Dprefetcher_final_stats=pref_pprefetcherDno_instr_final_stats -Dl1i_prefetcher_initialize=pref_pprefetcherDno_instr_initialize -Dl1i_prefetcher_branch_operate=pref_pprefetcherDno_instr_branch_operate -Dl1i_prefetcher_cache_operate=pref_pprefetcherDno_instr_cache_operate -Dl1i_prefetcher_cycle_operate=pref_pprefetcherDno_instr_cycle_operate -Dl1i_prefetcher_cache_fill=pref_pprefetcherDno_instr_cache_fill -Dl1i_prefetcher_final_stats=pref_pprefetcherDno_instr_final_stats -Iinc -MMD -MP  -c -o prefetcher/no_instr/no.o prefetcher/no_instr/no.cc
ar -rcs obj/pref_pprefetcherDno_instr.a prefetcher/no_instr/no.o
ar -rcs obj/pref_pprefetcherDmypref.a 
g++ -Wall -O3 -std=c++17 -Ibranch/bimodal -Dinitialize_branch_predictor=bpred_bbranchDbimodal_initialize -Dlast_branch_result=bpred_bbranchDbimodal_last_result -Dpredict_branch=bpred_bbranchDbimodal_predict -Iinc -MMD -MP  -c -o branch/bimodal/bimodal.o branch/bimodal/bimodal.cc
ar -rcs obj/bpred_bbranchDbimodal.a branch/bimodal/bimodal.o
g++ -Wall -O3 -std=c++17 -Ibtb/basic_btb -Dinitialize_btb=btb_bbtbDbasic_btb_initialize -Dupdate_btb=btb_bbtbDbasic_btb_update -Dbtb_prediction=btb_bbtbDbasic_btb_predict -Iinc -MMD -MP  -c -o btb/basic_btb/basic_btb.o btb/basic_btb/basic_btb.cc
ar -rcs obj/btb_bbtbDbasic_btb.a btb/basic_btb/basic_btb.o
g++  -o bin/champsim src/ptw.o src/tracereader.o src/ooo_cpu.o src/main.o src/cache.o src/vmem.o src/dram_controller.o src/core_inst.o obj/repl_rreplacementDlru.a obj/pref_pprefetcherDno.a obj/pref_pprefetcherDno_instr.a obj/pref_pprefetcherDmypref.a obj/bpred_bbranchDbimodal.a obj/btb_bbtbDbasic_btb.a 
/usr/bin/ld: src/main.o: in function `main':
main.cc:(.text.startup+0x8e0): undefined reference to `CACHE::pref_pprefetcherDmypref_final_stats()'
/usr/bin/ld: main.cc:(.text.startup+0x15c8): undefined reference to `CACHE::pref_pprefetcherDmypref_initialize()'
/usr/bin/ld: src/cache.o: in function `CACHE::readlike_hit(unsigned long, unsigned long, PACKET&)':
cache.cc:(.text+0xee9): undefined reference to `CACHE::pref_pprefetcherDmypref_cache_operate(unsigned long, unsigned long, unsigned char, unsigned char, unsigned int)'
/usr/bin/ld: src/cache.o: in function `CACHE::filllike_miss(unsigned long, unsigned long, PACKET&)':
cache.cc:(.text+0x2d9f): undefined reference to `CACHE::pref_pprefetcherDmypref_cache_fill(unsigned long, unsigned int, unsigned int, unsigned char, unsigned long, unsigned int)'
/usr/bin/ld: src/cache.o: in function `CACHE::readlike_miss(PACKET&)':
cache.cc:(.text+0x4d71): undefined reference to `CACHE::pref_pprefetcherDmypref_cache_operate(unsigned long, unsigned long, unsigned char, unsigned char, unsigned int)'
/usr/bin/ld: src/cache.o: in function `CACHE::operate()':
cache.cc:(.text+0x676a): undefined reference to `CACHE::pref_pprefetcherDmypref_cycle_operate()'
collect2: error: ld returned 1 exit status
make: *** [Makefile:36：bin/champsim] 错误 1
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ make
make
g++ -Wall -O3 -std=c++17 -Iprefetcher/mypref -Dprefetcher_initialize=pref_pprefetcherDmypref_initialize -Dprefetcher_cache_operate=pref_pprefetcherDmypref_cache_operate -Dprefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dprefetcher_cycle_operate=pref_pprefetcherDmypref_cycle_operate -Dprefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dl1d_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dl2c_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dllc_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dl1d_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dl2c_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dllc_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dl1d_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dl2c_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dllc_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dl1d_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dl2c_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dllc_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Iinc -MMD -MP  -c -o prefetcher/mypref/mypref.o prefetcher/mypref/mypref.cc
prefetcher/mypref/mypref.cc: In member function ‘void CACHE::pref_pprefetcherDmypref_initialize()’:
prefetcher/mypref/mypref.cc:358:21: warning: comparison of integer expressions of different signedness: ‘int’ and ‘long unsigned int’ [-Wsign-compare]
  358 |     for( int i=0; i <NUM_CPUS; i++)
prefetcher/mypref/mypref.cc: At global scope:
prefetcher/mypref/mypref.cc:371:6: error: no declaration matches ‘void CACHE::pref_pprefetcherDmypref_cache_operate(uint64_t, uint64_t, uint8_t, uint8_t)’
  371 | void CACHE::l1d_prefetcher_operate(uint64_t addr, uint64_t ip, uint8_t cache_hit, uint8_t type)
      |      ^~~~~
In file included from inc/cache.h:107,
                 from prefetcher/mypref/mypref.cc:20:
inc/cache_modules.inc:52:10: note: candidate is: ‘uint32_t CACHE::pref_pprefetcherDmypref_cache_operate(uint64_t, uint64_t, uint8_t, uint8_t, uint32_t)’
   52 | uint32_t pref_pprefetcherDmypref_cache_operate(uint64_t, uint64_t, uint8_t, uint8_t, uint32_t);
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In file included from prefetcher/mypref/mypref.cc:20:
inc/cache.h:36:7: note: ‘class CACHE’ defined here
   36 | class CACHE : public champsim::operable, public MemoryRequestConsumer, public MemoryRequestProducer
      |       ^~~~~
prefetcher/mypref/mypref.cc:829:6: error: no declaration matches ‘void CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t)’
  829 | void CACHE::l1d_prefetcher_cache_fill(uint64_t addr, uint32_t set, uint32_t way, uint8_t prefetch, uint64_t evicted_addr, uint32_t metadata_in)
      |      ^~~~~
In file included from inc/cache.h:107,
                 from prefetcher/mypref/mypref.cc:20:
inc/cache_modules.inc:61:10: note: candidate is: ‘uint32_t CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t)’
   61 | uint32_t pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t);
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In file included from prefetcher/mypref/mypref.cc:20:
inc/cache.h:36:7: note: ‘class CACHE’ defined here
   36 | class CACHE : public champsim::operable, public MemoryRequestConsumer, public MemoryRequestProducer
      |       ^~~~~
prefetcher/mypref/mypref.cc: In member function ‘void CACHE::pref_pprefetcherDmypref_final_stats()’:
prefetcher/mypref/mypref.cc:851:22: error: ‘pref_filled’ was not declared in this scope; did you mean ‘pf_fill’?
  851 |     total_request += pref_filled[cpu][i];
      |                      ^~~~~~~~~~~
      |                      pf_fill
prefetcher/mypref/mypref.cc:853:21: error: ‘pref_useful’ was not declared in this scope; did you mean ‘pf_useful’?
  853 |     total_useful += pref_useful[cpu][i];
      |                     ^~~~~~~~~~~
      |                     pf_useful
prefetcher/mypref/mypref.cc:854:19: error: ‘pref_late’ was not declared in this scope; did you mean ‘pref_type’?
  854 |     total_late += pref_late[cpu][i];
      |                   ^~~~~~~~~
      |                   pref_type
prefetcher/mypref/mypref.cc:859:35: error: ‘pref_filled’ was not declared in this scope; did you mean ‘pf_fill’?
  859 | cout << "stream:pref_filled: " << pref_filled[cpu][1] << endl;
      |                                   ^~~~~~~~~~~
      |                                   pf_fill
prefetcher/mypref/mypref.cc:860:35: error: ‘pref_useful’ was not declared in this scope; did you mean ‘pf_useful’?
  860 | cout << "stream:pref_useful: " << pref_useful[cpu][1] << endl;
      |                                   ^~~~~~~~~~~
      |                                   pf_useful
prefetcher/mypref/mypref.cc:861:33: error: ‘pref_late’ was not declared in this scope; did you mean ‘pref_type’?
  861 | cout << "stream:pref_late: " << pref_late[cpu][1] << endl;
      |                                 ^~~~~~~~~
      |                                 pref_type
make: *** [<内置>：prefetcher/mypref/mypref.o] 错误 1
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ make
make
g++ -Wall -O3 -std=c++17 -Iprefetcher/mypref -Dprefetcher_initialize=pref_pprefetcherDmypref_initialize -Dprefetcher_cache_operate=pref_pprefetcherDmypref_cache_operate -Dprefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dprefetcher_cycle_operate=pref_pprefetcherDmypref_cycle_operate -Dprefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dl1d_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dl2c_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dllc_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dl1d_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dl2c_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dllc_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dl1d_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dl2c_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dllc_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dl1d_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dl2c_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dllc_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Iinc -MMD -MP  -c -o prefetcher/mypref/mypref.o prefetcher/mypref/mypref.cc
prefetcher/mypref/mypref.cc: In member function ‘void CACHE::pref_pprefetcherDmypref_initialize()’:
prefetcher/mypref/mypref.cc:358:21: warning: comparison of integer expressions of different signedness: ‘int’ and ‘long unsigned int’ [-Wsign-compare]
  358 |     for( int i=0; i <NUM_CPUS; i++)
prefetcher/mypref/mypref.cc: At global scope:
prefetcher/mypref/mypref.cc:371:6: error: no declaration matches ‘void CACHE::pref_pprefetcherDmypref_cache_operate(uint64_t, uint64_t, uint8_t, uint8_t)’
  371 | void CACHE::l1d_prefetcher_operate(uint64_t addr, uint64_t ip, uint8_t cache_hit, uint8_t type)
      |      ^~~~~
In file included from inc/cache.h:107,
                 from prefetcher/mypref/mypref.cc:20:
inc/cache_modules.inc:52:10: note: candidate is: ‘uint32_t CACHE::pref_pprefetcherDmypref_cache_operate(uint64_t, uint64_t, uint8_t, uint8_t, uint32_t)’
   52 | uint32_t pref_pprefetcherDmypref_cache_operate(uint64_t, uint64_t, uint8_t, uint8_t, uint32_t);
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In file included from prefetcher/mypref/mypref.cc:20:
inc/cache.h:36:7: note: ‘class CACHE’ defined here
   36 | class CACHE : public champsim::operable, public MemoryRequestConsumer, public MemoryRequestProducer
      |       ^~~~~
prefetcher/mypref/mypref.cc:829:6: error: no declaration matches ‘void CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t)’
  829 | void CACHE::l1d_prefetcher_cache_fill(uint64_t addr, uint32_t set, uint32_t way, uint8_t prefetch, uint64_t evicted_addr, uint32_t metadata_in)
      |      ^~~~~
In file included from inc/cache.h:107,
                 from prefetcher/mypref/mypref.cc:20:
inc/cache_modules.inc:61:10: note: candidate is: ‘uint32_t CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t)’
   61 | uint32_t pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t);
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In file included from prefetcher/mypref/mypref.cc:20:
inc/cache.h:36:7: note: ‘class CACHE’ defined here
   36 | class CACHE : public champsim::operable, public MemoryRequestConsumer, public MemoryRequestProducer
      |       ^~~~~
prefetcher/mypref/mypref.cc: In member function ‘void CACHE::pref_pprefetcherDmypref_final_stats()’:
prefetcher/mypref/mypref.cc:851:22: error: ‘pref_filled’ was not declared in this scope; did you mean ‘pf_fill’?
  851 |     total_request += pref_filled[cpu][i];
      |                      ^~~~~~~~~~~
      |                      pf_fill
prefetcher/mypref/mypref.cc:853:21: error: ‘pref_useful’ was not declared in this scope; did you mean ‘pf_useful’?
  853 |     total_useful += pref_useful[cpu][i];
      |                     ^~~~~~~~~~~
      |                     pf_useful
prefetcher/mypref/mypref.cc:854:19: error: ‘pref_late’ was not declared in this scope; did you mean ‘pref_type’?
  854 |     total_late += pref_late[cpu][i];
      |                   ^~~~~~~~~
      |                   pref_type
prefetcher/mypref/mypref.cc:859:35: error: ‘pref_filled’ was not declared in this scope; did you mean ‘pf_fill’?
  859 | cout << "stream:pref_filled: " << pref_filled[cpu][1] << endl;
      |                                   ^~~~~~~~~~~
      |                                   pf_fill
prefetcher/mypref/mypref.cc:860:35: error: ‘pref_useful’ was not declared in this scope; did you mean ‘pf_useful’?
  860 | cout << "stream:pref_useful: " << pref_useful[cpu][1] << endl;
      |                                   ^~~~~~~~~~~
      |                                   pf_useful
prefetcher/mypref/mypref.cc:861:33: error: ‘pref_late’ was not declared in this scope; did you mean ‘pref_type’?
  861 | cout << "stream:pref_late: " << pref_late[cpu][1] << endl;
      |                                 ^~~~~~~~~
      |                                 pref_type
make: *** [<内置>：prefetcher/mypref/mypref.o] 错误 1
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ make
make
g++ -Wall -O3 -std=c++17 -Iprefetcher/mypref -Dprefetcher_initialize=pref_pprefetcherDmypref_initialize -Dprefetcher_cache_operate=pref_pprefetcherDmypref_cache_operate -Dprefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dprefetcher_cycle_operate=pref_pprefetcherDmypref_cycle_operate -Dprefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dl1d_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dl2c_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dllc_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dl1d_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dl2c_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dllc_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dl1d_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dl2c_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dllc_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dl1d_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dl2c_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dllc_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Iinc -MMD -MP  -c -o prefetcher/mypref/mypref.o prefetcher/mypref/mypref.cc
In file included from prefetcher/mypref/mypref.cc:19:
prefetcher/mypref/ooo_cpu.h:5:10: fatal error: page_table_walker.h: 没有那个文件或目录
    5 | #include "page_table_walker.h"
      |          ^~~~~~~~~~~~~~~~~~~~~
compilation terminated.
make: *** [<内置>：prefetcher/mypref/mypref.o] 错误 1
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ make
make
g++ -Wall -O3 -std=c++17 -Iprefetcher/mypref -Dprefetcher_initialize=pref_pprefetcherDmypref_initialize -Dprefetcher_cache_operate=pref_pprefetcherDmypref_cache_operate -Dprefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dprefetcher_cycle_operate=pref_pprefetcherDmypref_cycle_operate -Dprefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dl1d_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dl2c_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dllc_prefetcher_initialize=pref_pprefetcherDmypref_initialize -Dl1d_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dl2c_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dllc_prefetcher_operate=pref_pprefetcherDmypref_cache_operate -Dl1d_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dl2c_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dllc_prefetcher_cache_fill=pref_pprefetcherDmypref_cache_fill -Dl1d_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dl2c_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Dllc_prefetcher_final_stats=pref_pprefetcherDmypref_final_stats -Iinc -MMD -MP  -c -o prefetcher/mypref/mypref.o prefetcher/mypref/mypref.cc
<command-line>: error: ‘void CACHE::pref_pprefetcherDmypref_initialize()’ cannot be overloaded with ‘void CACHE::pref_pprefetcherDmypref_initialize()’
<command-line>: note: in definition of macro ‘l2c_prefetcher_initialize’
<command-line>: note: previous declaration ‘void CACHE::pref_pprefetcherDmypref_initialize()’
<command-line>: note: in definition of macro ‘l1d_prefetcher_initialize’
<command-line>: error: ‘void CACHE::pref_pprefetcherDmypref_initialize()’ cannot be overloaded with ‘void CACHE::pref_pprefetcherDmypref_initialize()’
<command-line>: note: in definition of macro ‘llc_prefetcher_initialize’
<command-line>: note: previous declaration ‘void CACHE::pref_pprefetcherDmypref_initialize()’
<command-line>: note: in definition of macro ‘l1d_prefetcher_initialize’
<command-line>: error: ‘void CACHE::pref_pprefetcherDmypref_final_stats()’ cannot be overloaded with ‘void CACHE::pref_pprefetcherDmypref_final_stats()’
<command-line>: note: in definition of macro ‘l2c_prefetcher_final_stats’
<command-line>: note: previous declaration ‘void CACHE::pref_pprefetcherDmypref_final_stats()’
<command-line>: note: in definition of macro ‘l1d_prefetcher_final_stats’
<command-line>: error: ‘void CACHE::pref_pprefetcherDmypref_final_stats()’ cannot be overloaded with ‘void CACHE::pref_pprefetcherDmypref_final_stats()’
<command-line>: note: in definition of macro ‘llc_prefetcher_final_stats’
<command-line>: note: previous declaration ‘void CACHE::pref_pprefetcherDmypref_final_stats()’
<command-line>: note: in definition of macro ‘l1d_prefetcher_final_stats’
<command-line>: error: ‘uint32_t CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t)’ cannot be overloaded with ‘uint32_t CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t)’
<command-line>: note: in definition of macro ‘llc_prefetcher_cache_fill’
<command-line>: note: previous declaration ‘uint32_t CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t)’
<command-line>: note: in definition of macro ‘l2c_prefetcher_cache_fill’
prefetcher/mypref/mypref.cc:371:6: error: no declaration matches ‘void CACHE::pref_pprefetcherDmypref_cache_operate(uint64_t, uint64_t, uint8_t, uint8_t)’
  371 | void CACHE::l1d_prefetcher_operate(uint64_t addr, uint64_t ip, uint8_t cache_hit, uint8_t type)
      |      ^~~~~
<command-line>: note: candidates are: ‘uint32_t CACHE::pref_pprefetcherDmypref_cache_operate(uint64_t, uint64_t, uint8_t, uint8_t, uint32_t)’
<command-line>: note: in definition of macro ‘llc_prefetcher_operate’
<command-line>: note:                 ‘uint32_t CACHE::pref_pprefetcherDmypref_cache_operate(uint64_t, uint64_t, uint8_t, uint8_t, uint32_t, uint8_t)’
<command-line>: note: in definition of macro ‘l2c_prefetcher_operate’
<command-line>: note:                 ‘void CACHE::pref_pprefetcherDmypref_cache_operate(uint64_t, uint64_t, uint8_t, uint8_t, uint8_t)’
<command-line>: note: in definition of macro ‘l1d_prefetcher_operate’
In file included from prefetcher/mypref/ooo_cpu.h:4,
                 from prefetcher/mypref/mypref.cc:19:
prefetcher/mypref/cache.h:110:7: note: ‘class CACHE’ defined here
  110 | class CACHE : public MEMORY {
      |       ^~~~~
prefetcher/mypref/mypref.cc:829:6: error: no declaration matches ‘void CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t)’
  829 | void CACHE::l1d_prefetcher_cache_fill(uint64_t addr, uint32_t set, uint32_t way, uint8_t prefetch, uint64_t evicted_addr, uint32_t metadata_in)
      |      ^~~~~
<command-line>: note: candidates are: ‘uint32_t CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint32_t)’
<command-line>: note: in definition of macro ‘l2c_prefetcher_cache_fill’
<command-line>: note:                 ‘void CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint64_t, uint32_t, uint32_t, uint8_t, uint64_t, uint64_t, uint32_t)’
<command-line>: note: in definition of macro ‘l1d_prefetcher_cache_fill’
<command-line>: note:                 ‘void CACHE::pref_pprefetcherDmypref_cache_fill(uint64_t, uint32_t, uint32_t, uint8_t, uint64_t)’
<command-line>: note: in definition of macro ‘prefetcher_cache_fill’
In file included from prefetcher/mypref/ooo_cpu.h:4,
                 from prefetcher/mypref/mypref.cc:19:
prefetcher/mypref/cache.h:110:7: note: ‘class CACHE’ defined here
  110 | class CACHE : public MEMORY {
      |       ^~~~~
make: *** [<内置>：prefetcher/mypref/mypref.o] 错误 1
(base) bella@bella-v:~/Downloads/IPCP20/ChampSim-master$ bin/champsim --warmup_instructions 200000000 --simulation_instructions 500000000 ~/path/to/traces/400.perlbench-41B.champsimtrace.xz












(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ ./run_champsim.sh
bash: ./run_champsim.sh: 没有那个文件或目录
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ ./build_champsim.sh bimodal no no no lru 1
Illegal number of parameters
Usage: ./build_champsim.sh [branch_pred] [l1i_pref] [l1d_pref]
    [l2c_pref] [llc_pref] [itlb_pref] [dtlb_pref] [stlb_pref] [btb_repl]
    [l1i_repl] [l1d_repl] [l2c_repl] [llc_repl] [itlb_repl] [dtlb_repl]
    [stlb_repl] [num_core] [tail_name]
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ ./build_champsim.sh bimodal no no no no no no no no lru lru lru lru lru lru lru lru 1 tail
[ERROR] Cannot find BTB replacement policy
[ERROR] Possible BTB replacement policy from replacement/*.btb_repl
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Othe(base(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ 
./build_champsim.sh bimodal no no no no no no no no lru lru lru lru lru lru lr
u lru 1 tail
[ERROR] Cannot find BTB replacement policy
[ERROR] Possible BTB replacement policy from replacement/*.btb_repl
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$
 ./build_champsim.sh
Illegal number of parameters
Usage: ./build_champsim.sh [branch_pred] [l1i_pref] [l1d_pref]
    [l2c_pref] [llc_pref] [itlb_pref] [dtlb_pref] [stlb_pref] [btb_repl]
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ ./build_champsim.sh bimodal no no no no no no no no lru lru lru lru lru lru lru lru 1 tail
[ERROR] Cannot find BTB replacement policy
[ERROR] Possible BTB replacement policy from replacement/*.btb_repl
replacement/lru.btb_repl
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ ./build_champsim.sh bimodal no no no no no no no lru lru lru lru lru lru lru lru 1 tail
Building single-core ChampSim...

rm -f -r obj
Generating dependencies for src/cache.cc...
Compiling src/cache.cc...
src/cache.cc: In member function ‘void CACHE::handle_read()’:
src/cache.cc:1750:27: warning: suggest explicit braces to avoid ambiguous ‘else’ [-Wdangling-else]
 1750 |                         if(warmup_complete[read_cpu])
      |                           ^
src/cache.cc:1749:34: warning: variable ‘l2c_mpki’ set but not used [-Wunused-but-set-variable]
 1749 |                         uint32_t l2c_mpki; // = (ooo_cpu[fill_cpu].L2C.sim_access[fill_cpu][0]*1000)/(ooo_cpu[fill_cpu].num_retired);
      |                                  ^~~~~~~~
src/cache.cc:2375:39: warning: suggest explicit braces to avoid ambiguous ‘else’ [-Wdangling-else]
 2375 |                                     if(warmup_complete[read_cpu])
      |                                       ^
src/cache.cc:2374:46: warning: variable ‘l2c_mpki’ set but not used [-Wunused-but-set-variable]
 2374 |                                     uint32_t l2c_mpki; // = (ooo_cpu[fill_cpu].L2C.sim_access[fill_cpu][0]*1000)/(ooo_cpu[fill_cpu].num_retired);
      |                                              ^~~~~~~~
src/cache.cc:2243:61: warning: ‘prior_data’ may be used uninitialized in this function [-Wmaybe-uninitialized]
 2243 |                                 MSHR.entry[mshr_index].data = prior_data;
      |                                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~
Generating dependencies for src/ooo_cpu.cc...
Compiling src/ooo_cpu.cc...
src/ooo_cpu.cc:508:25: warning: "/*" within comment [-Wcomment]
  508 |                         /*
      |                          
src/ooo_cpu.cc:895:40: warning: "/*" within comment [-Wcomment]
  895 |  ////DP ( if (warmup_complete[cpu]) { //*******************************************************************************************
      |                                         
src/ooo_cpu.cc:927:9: warning: "/*" within comment [-Wcomment]
  927 |         /*fetch_packet.address = ROB.entry[fetch_index].instruction_pa >> 6;
      |          
src/ooo_cpu.cc:949:13: warning: "/*" within comment [-Wcomment]
  949 |             /*
      |              
src/ooo_cpu.cc: In member function ‘void O3_CPU::complete_instr_fetch(PACKET_QUEUE*, uint8_t)’:
src/ooo_cpu.cc:2344:19: warning: comparison of integer expressions of different signedness: ‘uint32_t’ {aka ‘unsigned int’} and ‘int’ [-Wsign-compare]
 2344 |     if (rob_index != (a = check_rob(queue->entry[index].instr_id)))
      |         ~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Generating dependencies for src/dram_controller.cc...
Compiling src/dram_controller.cc...
Generating dependencies for src/main.cc...
Compiling src/main.cc...
In file included from /usr/include/getopt.h:24,
                 from src/main.cc:3:
/usr/include/features.h:187:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [-Wcpp]
  187 | # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
      |   ^~~~~~~
src/main.cc: In function ‘int main(int, char**)’:
src/main.cc:1183:43: warning: format ‘%d’ expects argument of type ‘int*’, but argument 4 has type ‘uint8_t*’ {aka ‘unsigned char*’} [-Wformat=]
 1183 |  while((fscanf(context_switch_file, "%ld %d %d", &cs_file[index].cycle, &cs_file[index].swap_cpu[0], &cs_file[index].swap_cpu[1]))!=EOF)
      |                                          ~^                             ~~~~~~~~~~~~~~~~~~~~~~~~~~~
      |                                           |                             |
      |                                           int*                          uint8_t* {aka unsigned char*}
      |                                          %hhd
src/main.cc:1183:46: warning: format ‘%d’ expects argument of type ‘int*’, but argument 5 has type ‘uint8_t*’ {aka ‘unsigned char*’} [-Wformat=]
 1183 |  while((fscanf(context_switch_file, "%ld %d %d", &cs_file[index].cycle, &cs_file[index].swap_cpu[0], &cs_file[index].swap_cpu[1]))!=EOF)
      |                                             ~^                                                       ~~~~~~~~~~~~~~~~~~~~~~~~~~~
      |                                              |                                                       |
      |                                              int*                                                    uint8_t* {aka unsigned char*}
      |                                             %hhd
src/main.cc:1500:49: warning: comparison of integer expressions of different signedness: ‘uint64_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
 1500 |      if( cs_index!=-1 && ( current_core_cycle[i]==cs_file[cs_index].cycle) && (i==cs_file[cs_index].swap_cpu[0] || i==cs_file[cs_index].swap_cpu[1]))
      |                            ~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~
src/main.cc:1511:11: warning: ‘index’ may be used uninitialized in this function [-Wmaybe-uninitialized]
 1511 |           if(cs_index >= index)
      |           ^~
Generating dependencies for src/uncore.cc...
Compiling src/uncore.cc...
Generating dependencies for src/page_table_walker.cc...
Compiling src/page_table_walker.cc...
src/page_table_walker.cc: In member function ‘uint64_t PAGE_TABLE_WALKER::handle_page_fault(PAGE_TABLE_PAGE*, PACKET*, uint8_t)’:
src/page_table_walker.cc:425:1: warning: control reaches end of non-void function [-Wreturn-type]
  425 | }
      | ^
Generating dependencies for src/block.cc...
Compiling src/block.cc...
Generating dependencies for branch/branch_predictor.cc...
Compiling branch/branch_predictor.cc...
Generating dependencies for replacement/l1d_replacement.cc...
Compiling replacement/l1d_replacement.cc...
Generating dependencies for replacement/base_replacement.cc...
Compiling replacement/base_replacement.cc...
Generating dependencies for replacement/stlb_replacement.cc...
Compiling replacement/stlb_replacement.cc...
Generating dependencies for replacement/llc_replacement.cc...
Compiling replacement/llc_replacement.cc...
Generating dependencies for replacement/dtlb_replacement.cc...
Compiling replacement/dtlb_replacement.cc...
Generating dependencies for replacement/l2c_replacement.cc...
Compiling replacement/l2c_replacement.cc...
Generating dependencies for replacement/itlb_replacement.cc...
Compiling replacement/itlb_replacement.cc...
Generating dependencies for replacement/btb_replacement.cc...
Compiling replacement/btb_replacement.cc...
Generating dependencies for replacement/l1i_replacement.cc...
Compiling replacement/l1i_replacement.cc...
Generating dependencies for prefetcher/l2c_prefetcher.cc...
Compiling prefetcher/l2c_prefetcher.cc...
Generating dependencies for prefetcher/itlb_prefetcher.cc...
Compiling prefetcher/itlb_prefetcher.cc...
Generating dependencies for prefetcher/llc_prefetcher.cc...
Compiling prefetcher/llc_prefetcher.cc...
Generating dependencies for prefetcher/l1d_prefetcher.cc...
Compiling prefetcher/l1d_prefetcher.cc...
Generating dependencies for prefetcher/dtlb_prefetcher.cc...
Compiling prefetcher/dtlb_prefetcher.cc...
Generating dependencies for prefetcher/stlb_prefetcher.cc...
Compiling prefetcher/stlb_prefetcher.cc...
Generating dependencies for prefetcher/l1i_prefetcher.cc...
Compiling prefetcher/l1i_prefetcher.cc...
Linking bin/champsim...

ChampSim is successfully built
Branch Predictor: bimodal
L1I Prefetcher: no
L1D Prefetcher: no
L2C Prefetcher: no
LLC Prefetcher: no
ITLB Prefetcher: no
DTLB Prefetcher: no
STLB Prefetcher: no
BTB Replacement: lru
L1I Replacement: lru
L1D Replacement: lru
L2C Replacement: lru
LLC Replacement: lru
ITLB Replacement: lru
DTLB Replacement: lru
STLB Replacement: lru
Cores: 1
Binary: bin/bimodal-no-no-no-no-no-no-no-lru-lru-lru-lru-lru-lru-lru-lru-1core-tail

(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ make
Generating dependencies for branch/branch_predictor.cc...
Compiling branch/branch_predictor.cc...
Generating dependencies for replacement/l1d_replacement.cc...
Compiling replacement/l1d_replacement.cc...
Generating dependencies for replacement/stlb_replacement.cc...
Compiling replacement/stlb_replacement.cc...
Generating dependencies for replacement/llc_replacement.cc...
Compiling replacement/llc_replacement.cc...
Generating dependencies for replacement/dtlb_replacement.cc...
Compiling replacement/dtlb_replacement.cc...
Generating dependencies for replacement/l2c_replacement.cc...
Compiling replacement/l2c_replacement.cc...
Generating dependencies for replacement/itlb_replacement.cc...
Compiling replacement/itlb_replacement.cc...
Generating dependencies for replacement/btb_replacement.cc...
Compiling replacement/btb_replacement.cc...
Generating dependencies for replacement/l1i_replacement.cc...
Compiling replacement/l1i_replacement.cc...
Generating dependencies for prefetcher/l2c_prefetcher.cc...
Compiling prefetcher/l2c_prefetcher.cc...
Generating dependencies for prefetcher/itlb_prefetcher.cc...
Compiling prefetcher/itlb_prefetcher.cc...
Generating dependencies for prefetcher/llc_prefetcher.cc...
Compiling prefetcher/llc_prefetcher.cc...
Generating dependencies for prefetcher/l1d_prefetcher.cc...
Compiling prefetcher/l1d_prefetcher.cc...
Generating dependencies for prefetcher/dtlb_prefetcher.cc...
Compiling prefetcher/dtlb_prefetcher.cc...
Generating dependencies for prefetcher/stlb_prefetcher.cc...
Compiling prefetcher/stlb_prefetcher.cc...
Generating dependencies for prefetcher/l1i_prefetcher.cc...
Compiling prefetcher/l1i_prefetcher.cc...
Linking bin/champsim...
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ bin/champsim --warmup_instructions 200000000 --simulation_instructions 500000000 ~/path/to/traces/400.perlbench-41B.champsimtrace.xz

*** ChampSim Multicore Out-of-Order Simulator ***

Warmup Instructions: 200000000
Simulation Instructions: 500000000
Number of CPUs: 1
LLC sets: 2048
LLC ways: 16
Off-chip DRAM Size: 4096 MB Channels: 1 Width: 64-bit Data Rate: 6400 MT/s

*** Not enough traces for the configured number of cores ***

champsim: src/main.cc:1195: int main(int, char**): Assertion `0' failed.
已放弃 (核心已转储)
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ bin/champsim --warmup_instructions 200000000 --simulation_instructions 500000000 600.perlbench_s-210B.champsimtrace.xz

*** ChampSim Multicore Out-of-Order Simulator ***

Warmup Instructions: 200000000
Simulation Instructions: 500000000
Number of CPUs: 1
LLC sets: 2048
LLC ways: 16
Off-chip DRAM Size: 4096 MB Channels: 1 Width: 64-bit Data Rate: 6400 MT/s

*** Not enough traces for the configured number of cores ***

champsim: src/main.cc:1195: int main(int, char**): Assertion `0' failed.
已放弃 (核心已转储)
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ bin/champsim --warmup_instructions 1 --simulation_instructions 10 600.perlbench_s-210B.champsimtrace.xz

*** ChampSim Multicore Out-of-Order Simulator ***

Warmup Instructions: 1
Simulation Instructions: 10
Number of CPUs: 1
LLC sets: 2048
LLC ways: 16
Off-chip DRAM Size: 4096 MB Channels: 1 Width: 64-bit Data Rate: 6400 MT/s

*** Not enough traces for the configured number of cores ***

champsim: src/main.cc:1195: int main(int, char**): Assertion `0' failed.
已放弃 (核心已转储)
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ bin/champsim --warmup_instructions 1 --simulation_instructions 10 --traces 600.perlbench_s-210B.champsimtrace.xz

*** ChampSim Multicore Out-of-Order Simulator ***

Warmup Instructions: 1
Simulation Instructions: 10
Number of CPUs: 1
LLC sets: 2048
LLC ways: 16
Off-chip DRAM Size: 4096 MB Channels: 1 Width: 64-bit Data Rate: 6400 MT/s

*** Not enough traces for the configured number of cores ***

champsim: src/main.cc:1195: int main(int, char**): Assertion `0' failed.
已放弃 (核心已转储)
(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Ot(base(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main/ChampSim/Other_PF$ 




















(base) bella@bella-v:~/Downloads/IPCP20/Berti-MICRO2022-main$ ./run.sh -p 127
Running in Parallel

Building Berti... done
Building MLOP... done
Building IPCP... done
Building IP Stride... done
Making everything ready to run... done
Running...bash：行 1: 152765 段错误               （核心已转储） ./ChampSim/Berti/bin/hashed_perceptron-no-vberti-no-no-no-no-no-lru-lru-lru-srrip-drrip-lru-lru-lru-1core-no -warmup_instructions 50000000 -simulation_instructions 200000000 -traces traces/spec2k17/600.perlbench_s-210B.champsimtrace.xz > output/spec2k17/hashed_perceptron-no-vberti-no-no-no-no-no-lru-lru-lru-srrip-drrip-lru-lru-lru-1core-no---600.perlbench_s-210B.champsimtrace.xz 2> /dev/null
bash：行 1: 152769 段错误               （核心已转储） ./ChampSim/Other_PF/bin/hashed_perceptron-no-mlop_dpc3-no-no-no-no-no-lru-lru-lru-srrip-drrip-lru-lru-lru-1core-no -warmup_instructions 50000000 -simulation_instructions 200000000 -traces traces/spec2k17/600.perlbench_s-210B.champsimtrace.xz > output/spec2k17/hashed_perceptron-no-mlop_dpc3-no-no-no-no-no-lru-lru-lru-srrip-drrip-lru-lru-lru-1core-no---600.perlbench_s-210B.champsimtrace.xz 2> /dev/null
bash：行 1: 152767 段错误               （核心已转储） ./ChampSim/Other_PF/bin/hashed_perceptron-no-ipcp_isca2020-no-no-no-no-no-lru-lru-lru-srrip-drrip-lru-lru-lru-1core-no -warmup_instructions 50000000 -simulation_instructions 200000000 -traces traces/spec2k17/600.perlbench_s-210B.champsimtrace.xz > output/spec2k17/hashed_perceptron-no-ipcp_isca2020-no-no-no-no-no-lru-lru-lru-srrip-drrip-lru-lru-lru-1core-no---600.perlbench_s-210B.champsimtrace.xz 2> /dev/null
bash：行 1: 152768 段错误               （核心已转储） ./ChampSim/Other_PF/bin/hashed_perceptron-no-ip_stride-no-no-no-no-no-lru-lru-lru-srrip-drrip-lru-lru-lru-1core-no -warmup_instructions 50000000 -simulation_instructions 200000000 -traces traces/spec2k17/600.perlbench_s-210B.champsimtrace.xz > output/spec2k17/hashed_perceptron-no-ip_stride-no-no-no-no-no-lru-lru-lru-srrip-drrip-lru-lru-lru-1core-no---600.perlbench_s-210B.champsimtrace.xz 2> /dev/null
bash：行 1: 152766 已放弃               （核心已转储） ./ChampSim/Other_PF/bin/bimodal-no-no-no-no-no-no-no-lru-lru-lru-lru-lru-lru-lru-lru-1core-tail -warmup_instructions 50000000 -simulation_instructions 200000000 -traces traces/spec2k17/600.perlbench_s-210B.champsimtrace.xz > output/spec2k17/bimodal-no-no-no-no-no-no-no-lru-lru-lru-lru-lru-lru-lru-lru-1core-tail---600.perlbench_s-210B.champsimtrace.xz 2> /dev/null
 done

Results, it requires numpy, scipy, maptlotlib and pprint

SPEC CPU2K17 Parsing data... done
SPEC CPU2K17 Memory Intensive SpeedUp
--------------------------------------
| Prefetch | Speedup | L1D Accuracy |
--------------------------------------
Generating Figure 8 SPEC17-MemInt... ERROR

























