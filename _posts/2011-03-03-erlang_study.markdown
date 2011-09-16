---
layout: default
title: Erlang Study
---

# {{page.title}}

## Erlang程序编译运行的方法

### 方法1：直接在shell中编译运行

<table class="highlighttable"><tr><td class="linenos"><div class="linenodiv"><pre>1
2
3
4
5
6</pre></div></td><td class="code"><div class="highlight"><pre><span class="n">hello</span><span class="p">.</span><span class="n">erl</span>
    <span class="o">-</span><span class="n">module</span><span class="p">(</span><span class="n">hello</span><span class="p">).</span>
    <span class="o">-</span><span class="n">export</span><span class="p">([</span><span class="n">start</span><span class="o">/</span><span class="mi">0</span><span class="p">]).</span>

    <span class="n">start</span><span class="p">()</span> <span class="o">-&gt;</span>
        <span class="nn">io</span><span class="p">:</span><span class="n">format</span><span class="p">(</span><span class="s">&quot;Hello world</span><span class="si">~n</span><span class="s">&quot;</span><span class="p">).</span>
</pre></div>
</td></tr></table>



<div class="highlight"><pre><span class="gp">$</span> erl
<span class="gp">&gt;</span>c<span class="o">(</span>hello<span class="o">)</span>.
<span class="go">{ok,hello}</span>
<span class="gp">&gt;</span>hello:start<span class="o">()</span>.
<span class="go">Hello world</span>
<span class="go">ok</span>
<span class="gp">&gt;</span>
</pre></div>




### 方法2：在命令行编译运行

<div class="highlight"><pre><span class="err">$ erlc hello</span>
<span class="err">$ erl -noshell -pa path -s hello start -s init stop</span>
</pre></div>



### 方法3：把方法2的命令写入一个脚本，作为批处理的东西

<div class="highlight"><pre>hello.sh
    <span class="c">#!/bin/sh</span>
    
    erl -noshell -pa path -s hello start -s init <span class="nb">stop</span>
</pre></div>



<div class="highlight"><pre><span class="gp">$</span> ./hello.sh
</pre></div>



### 方法4：用makefile来编译，

一个标准的makefile模板


.SUFFIXES: .erl .bem .yrl
.erl .beam
    erlc -W $<

.yrl .erl
    erlc -W $<

ERL=erl -boot start_clean
MODS=mod1 mod2 mod3 …

all:compile
compile: ${MODS:%=%.beam} subdirs
special1.beam: special1.erl
    ${ERL} -Dflag | -w0 special1.erl

application1: compile
    ${ERL} -pa Dir1 -s application1 start Arg1 Arg2

subdirs:
    cd dir1; moke
    cd dir2: make

clean:
    rm -rf *.beam erl_crash.dump
    cd dir1; make clean
    cd dir2; make clean
