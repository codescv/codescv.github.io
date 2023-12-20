---
layout: post
keywords: fastai
description: 
title: Python parallel processing
toc: true 
badges: true
comments: true
categories: [Python, Programming]
hide: false
draft: 
nb_path: notebooks/2020-08-30-python-parallel-processing.ipynb
date: 2020-08-30
---

<!--
#################################################
### THIS FILE WAS AUTOGENERATED! DO NOT EDIT! ###
#################################################
# file to edit: notebooks/2020-08-30-python-parallel-processing.ipynb
-->

<div class="container" id="notebook-container">

  <p><a href="https://colab.research.google.com/github/codescv/codescv.github.io/blob/main/notebooks/2020-08-30-python-parallel-processing.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="" /></a></p>

  
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>I came across this function called <code>parallel</code> in <a href="https://github.com/fastai/fastai">fastai</a>, and it seems very interesting.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="A-Simple-Example">A Simple Example<a class="anchor-link" href="#A-Simple-Example"> </a></h1>
</div>
</div>
</div>
    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">fastcore.all</span> <span class="kn">import</span> <span class="n">parallel</span>
</pre></div>

    </div>
</div>
</div>

</div>
    {% endraw %}

    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">nbdev.showdoc</span> <span class="kn">import</span> <span class="n">doc</span>
</pre></div>

    </div>
</div>
</div>

</div>
    {% endraw %}

    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">doc</span><span class="p">(</span><span class="n">parallel</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">


<div class="output_html rendered_html output_subarea "><h4 id="parallel" class="doc_header"><code>parallel</code><a href="https://github.com/fastai/fastcore/tree/master/fastcore/utils.py#L715" class="source_link" style="float:right">[source]</a></h4><blockquote><p><code>parallel</code>(<strong><code>f</code></strong>, <strong><code>items</code></strong>, <strong>*<code>args</code></strong>, <strong><code>n_workers</code></strong>=<em><code>8</code></em>, <strong><code>total</code></strong>=<em><code>None</code></em>, <strong><code>progress</code></strong>=<em><code>None</code></em>, <strong><code>pause</code></strong>=<em><code>0</code></em>, <strong>**<code>kwargs</code></strong>)</p>
</blockquote>
<p>Applies <code>func</code> in parallel to <code>items</code>, using <code>n_workers</code></p>
<p><a href="https://fastcore.fast.ai/utils#parallel" target="_blank" rel="noreferrer noopener">Show in docs</a></p>
</div>

</div>

</div>
</div>

</div>
    {% endraw %}

<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>As the documentation states, the <code>parallel</code> function can run any python function <code>f</code> with <code>items</code> using multiple workers, and collect the results.</p>
<p>Let's try a simple examples:</p>

</div>
</div>
</div>
    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">math</span>
<span class="kn">import</span> <span class="nn">time</span>

<span class="k">def</span> <span class="nf">f</span><span class="p">(</span><span class="n">x</span><span class="p">):</span>
  <span class="n">time</span><span class="o">.</span><span class="n">sleep</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
  <span class="k">return</span> <span class="n">x</span> <span class="o">*</span> <span class="mi">2</span>

<span class="n">numbers</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">10</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
    {% endraw %}

    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>

<span class="nb">list</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="n">f</span><span class="p">,</span> <span class="n">numbers</span><span class="p">))</span>
<span class="nb">print</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">
<pre>
CPU times: user 0 ns, sys: 0 ns, total: 0 ns
Wall time: 10 s
</pre>
</div>
</div>

</div>
</div>

</div>
    {% endraw %}

    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>

<span class="nb">list</span><span class="p">(</span><span class="n">parallel</span><span class="p">(</span><span class="n">f</span><span class="p">,</span> <span class="n">numbers</span><span class="p">))</span>
<span class="nb">print</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">


<div class="output_html rendered_html output_subarea "></div>

</div>

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">
<pre>
CPU times: user 32 ms, sys: 52 ms, total: 84 ms
Wall time: 2.08 s
</pre>
</div>
</div>

</div>
</div>

</div>
    {% endraw %}

<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The function <code>f</code> we have in this example is very simple: it sleeps for one second and then returns <code>x*2</code>. When executed in serial, it takes 10 seconds which is exactly
what we expect. When using more workers(8 by default), it takes only 2 seconds.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Dig-into-the-Implementation">Dig into the Implementation<a class="anchor-link" href="#Dig-into-the-Implementation"> </a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Let's see how <code>parallel</code> is implemented:</p>

</div>
</div>
</div>
    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span>parallel<span class="o">??</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">



<div class="output_text output_subarea ">
<pre><span class="ansi-red-fg">Signature:</span>
parallel<span class="ansi-blue-fg">(</span>
    f<span class="ansi-blue-fg">,</span>
    items<span class="ansi-blue-fg">,</span>
    <span class="ansi-blue-fg">*</span>args<span class="ansi-blue-fg">,</span>
    n_workers<span class="ansi-blue-fg">=</span><span class="ansi-cyan-fg">8</span><span class="ansi-blue-fg">,</span>
    total<span class="ansi-blue-fg">=</span><span class="ansi-green-fg">None</span><span class="ansi-blue-fg">,</span>
    progress<span class="ansi-blue-fg">=</span><span class="ansi-green-fg">None</span><span class="ansi-blue-fg">,</span>
    pause<span class="ansi-blue-fg">=</span><span class="ansi-cyan-fg">0</span><span class="ansi-blue-fg">,</span>
    <span class="ansi-blue-fg">**</span>kwargs<span class="ansi-blue-fg">,</span>
<span class="ansi-blue-fg">)</span>
<span class="ansi-red-fg">Source:</span>   
<span class="ansi-green-fg">def</span> parallel<span class="ansi-blue-fg">(</span>f<span class="ansi-blue-fg">,</span> items<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">*</span>args<span class="ansi-blue-fg">,</span> n_workers<span class="ansi-blue-fg">=</span>defaults<span class="ansi-blue-fg">.</span>cpus<span class="ansi-blue-fg">,</span> total<span class="ansi-blue-fg">=</span><span class="ansi-green-fg">None</span><span class="ansi-blue-fg">,</span> progress<span class="ansi-blue-fg">=</span><span class="ansi-green-fg">None</span><span class="ansi-blue-fg">,</span> pause<span class="ansi-blue-fg">=</span><span class="ansi-cyan-fg">0</span><span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">**</span>kwargs<span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">:</span>
    <span class="ansi-blue-fg">&#34;Applies `func` in parallel to `items`, using `n_workers`&#34;</span>
    <span class="ansi-green-fg">if</span> progress <span class="ansi-green-fg">is</span> <span class="ansi-green-fg">None</span><span class="ansi-blue-fg">:</span> progress <span class="ansi-blue-fg">=</span> progress_bar <span class="ansi-green-fg">is</span> <span class="ansi-green-fg">not</span> <span class="ansi-green-fg">None</span>
    <span class="ansi-green-fg">with</span> ProcessPoolExecutor<span class="ansi-blue-fg">(</span>n_workers<span class="ansi-blue-fg">,</span> pause<span class="ansi-blue-fg">=</span>pause<span class="ansi-blue-fg">)</span> <span class="ansi-green-fg">as</span> ex<span class="ansi-blue-fg">:</span>
        r <span class="ansi-blue-fg">=</span> ex<span class="ansi-blue-fg">.</span>map<span class="ansi-blue-fg">(</span>f<span class="ansi-blue-fg">,</span>items<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">*</span>args<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">**</span>kwargs<span class="ansi-blue-fg">)</span>
        <span class="ansi-green-fg">if</span> progress<span class="ansi-blue-fg">:</span>
            <span class="ansi-green-fg">if</span> total <span class="ansi-green-fg">is</span> <span class="ansi-green-fg">None</span><span class="ansi-blue-fg">:</span> total <span class="ansi-blue-fg">=</span> len<span class="ansi-blue-fg">(</span>items<span class="ansi-blue-fg">)</span>
            r <span class="ansi-blue-fg">=</span> progress_bar<span class="ansi-blue-fg">(</span>r<span class="ansi-blue-fg">,</span> total<span class="ansi-blue-fg">=</span>total<span class="ansi-blue-fg">,</span> leave<span class="ansi-blue-fg">=</span><span class="ansi-green-fg">False</span><span class="ansi-blue-fg">)</span>
        <span class="ansi-green-fg">return</span> L<span class="ansi-blue-fg">(</span>r<span class="ansi-blue-fg">)</span>
<span class="ansi-red-fg">File:</span>      /opt/conda/lib/python3.7/site-packages/fastcore/utils.py
<span class="ansi-red-fg">Type:</span>      function
</pre>
</div>

</div>

</div>
</div>

</div>
    {% endraw %}

    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="o">??</span>ProcessPoolExecutor
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">



<div class="output_text output_subarea ">
<pre><span class="ansi-red-fg">Init signature:</span>
ProcessPoolExecutor<span class="ansi-blue-fg">(</span>
    max_workers<span class="ansi-blue-fg">=</span><span class="ansi-cyan-fg">8</span><span class="ansi-blue-fg">,</span>
    on_exc<span class="ansi-blue-fg">=</span><span class="ansi-blue-fg">&lt;</span>built<span class="ansi-blue-fg">-</span><span class="ansi-green-fg">in</span> function print<span class="ansi-blue-fg">&gt;</span><span class="ansi-blue-fg">,</span>
    pause<span class="ansi-blue-fg">=</span><span class="ansi-cyan-fg">0</span><span class="ansi-blue-fg">,</span>
    mp_context<span class="ansi-blue-fg">=</span><span class="ansi-green-fg">None</span><span class="ansi-blue-fg">,</span>
    initializer<span class="ansi-blue-fg">=</span><span class="ansi-green-fg">None</span><span class="ansi-blue-fg">,</span>
    initargs<span class="ansi-blue-fg">=</span><span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">,</span>
<span class="ansi-blue-fg">)</span>
<span class="ansi-red-fg">Source:</span>        
<span class="ansi-green-fg">class</span> ProcessPoolExecutor<span class="ansi-blue-fg">(</span>concurrent<span class="ansi-blue-fg">.</span>futures<span class="ansi-blue-fg">.</span>ProcessPoolExecutor<span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">:</span>
    <span class="ansi-blue-fg">&#34;Same as Python&#39;s ProcessPoolExecutor, except can pass `max_workers==0` for serial execution&#34;</span>
    <span class="ansi-green-fg">def</span> __init__<span class="ansi-blue-fg">(</span>self<span class="ansi-blue-fg">,</span> max_workers<span class="ansi-blue-fg">=</span>defaults<span class="ansi-blue-fg">.</span>cpus<span class="ansi-blue-fg">,</span> on_exc<span class="ansi-blue-fg">=</span>print<span class="ansi-blue-fg">,</span> pause<span class="ansi-blue-fg">=</span><span class="ansi-cyan-fg">0</span><span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">**</span>kwargs<span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">:</span>
        <span class="ansi-green-fg">if</span> max_workers <span class="ansi-green-fg">is</span> <span class="ansi-green-fg">None</span><span class="ansi-blue-fg">:</span> max_workers<span class="ansi-blue-fg">=</span>defaults<span class="ansi-blue-fg">.</span>cpus
        self<span class="ansi-blue-fg">.</span>not_parallel <span class="ansi-blue-fg">=</span> max_workers<span class="ansi-blue-fg">==</span><span class="ansi-cyan-fg">0</span>
        store_attr<span class="ansi-blue-fg">(</span>self<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">&#39;on_exc,pause,max_workers&#39;</span><span class="ansi-blue-fg">)</span>
        <span class="ansi-green-fg">if</span> self<span class="ansi-blue-fg">.</span>not_parallel<span class="ansi-blue-fg">:</span> max_workers<span class="ansi-blue-fg">=</span><span class="ansi-cyan-fg">1</span>
        super<span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">.</span>__init__<span class="ansi-blue-fg">(</span>max_workers<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">**</span>kwargs<span class="ansi-blue-fg">)</span>

    <span class="ansi-green-fg">def</span> map<span class="ansi-blue-fg">(</span>self<span class="ansi-blue-fg">,</span> f<span class="ansi-blue-fg">,</span> items<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">*</span>args<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">**</span>kwargs<span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">:</span>
        self<span class="ansi-blue-fg">.</span>lock <span class="ansi-blue-fg">=</span> Manager<span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">.</span>Lock<span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">)</span>
        g <span class="ansi-blue-fg">=</span> partial<span class="ansi-blue-fg">(</span>f<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">*</span>args<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">**</span>kwargs<span class="ansi-blue-fg">)</span>
        <span class="ansi-green-fg">if</span> self<span class="ansi-blue-fg">.</span>not_parallel<span class="ansi-blue-fg">:</span> <span class="ansi-green-fg">return</span> map<span class="ansi-blue-fg">(</span>g<span class="ansi-blue-fg">,</span> items<span class="ansi-blue-fg">)</span>
        <span class="ansi-green-fg">try</span><span class="ansi-blue-fg">:</span> <span class="ansi-green-fg">return</span> super<span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">.</span>map<span class="ansi-blue-fg">(</span>partial<span class="ansi-blue-fg">(</span>_call<span class="ansi-blue-fg">,</span> self<span class="ansi-blue-fg">.</span>lock<span class="ansi-blue-fg">,</span> self<span class="ansi-blue-fg">.</span>pause<span class="ansi-blue-fg">,</span> self<span class="ansi-blue-fg">.</span>max_workers<span class="ansi-blue-fg">,</span> g<span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">,</span> items<span class="ansi-blue-fg">)</span>
        <span class="ansi-green-fg">except</span> Exception <span class="ansi-green-fg">as</span> e<span class="ansi-blue-fg">:</span> self<span class="ansi-blue-fg">.</span>on_exc<span class="ansi-blue-fg">(</span>e<span class="ansi-blue-fg">)</span>
<span class="ansi-red-fg">File:</span>           /opt/conda/lib/python3.7/site-packages/fastcore/utils.py
<span class="ansi-red-fg">Type:</span>           type
<span class="ansi-red-fg">Subclasses:</span>     
</pre>
</div>

</div>

</div>
</div>

</div>
    {% endraw %}

<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>As we can see in the source code, under the hood, this is using the <a href="https://docs.python.org/3/library/concurrent.futures.html#concurrent.futures.ProcessPoolExecutor">concurrent.futures.ProcessPoolExecutor</a> class from Python.</p>
<p>Note that this class is essentially different than Python Threads, which is subject to the Global Interpreter Lock.</p>
<p>The ProcessPoolExecutor class is an Executor subclass that uses a pool of processes to execute calls asynchronously. ProcessPoolExecutor uses the multiprocessing module, which allows it to side-step the Global Interpreter Lock but also means that only picklable objects can be executed and returned.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Use-cases">Use cases<a class="anchor-link" href="#Use-cases"> </a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>This function can be quite useful for long running tasks and you want to take advantage of multi-core CPUs to speed up your processing. For example, if you want to download a lot of images from the internet, you may want to use this to parallize your download jobs.</p>
<p>If your function <code>f</code> is very fast, there can be suprising cases, here is an example:</p>

</div>
</div>
</div>
    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">math</span>
<span class="kn">import</span> <span class="nn">time</span>

<span class="k">def</span> <span class="nf">f</span><span class="p">(</span><span class="n">x</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">x</span> <span class="o">*</span> <span class="mi">2</span>

<span class="n">numbers</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">10000</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
    {% endraw %}

    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>

<span class="nb">list</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="n">f</span><span class="p">,</span> <span class="n">numbers</span><span class="p">))</span>
<span class="nb">print</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">
<pre>
CPU times: user 0 ns, sys: 0 ns, total: 0 ns
Wall time: 1.24 ms
</pre>
</div>
</div>

</div>
</div>

</div>
    {% endraw %}

    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>

<span class="nb">list</span><span class="p">(</span><span class="n">parallel</span><span class="p">(</span><span class="n">f</span><span class="p">,</span> <span class="n">numbers</span><span class="p">))</span>
<span class="nb">print</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">


<div class="output_html rendered_html output_subarea "></div>

</div>

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">
<pre>
CPU times: user 3.96 s, sys: 940 ms, total: 4.9 s
Wall time: 12.4 s
</pre>
</div>
</div>

</div>
</div>

</div>
    {% endraw %}

<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>In the above example, <code>f</code> is very fast and the overhead of creating a lot of tasks outweigh the advantage of multi-processing. So use this with caution, and always take profiles.</p>

</div>
</div>
</div>

</div>

