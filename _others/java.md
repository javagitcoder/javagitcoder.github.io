---
title: Java
author: Chu Ying
date: 2022-02-04
category: java
layout: post
---
<h2>一、Java基础</h2> 
<h3>1. Java中基本数据类型有哪些？</h3> 
<p>Java有8种基本数据类型，分为4类：</p> 
<ul>
 <li><strong>整数类型</strong>：byte（1字节）、short（2字节）、int（4字节）、long（8字节）。</li>
 <li><strong>浮点类型</strong>：float（4字节）、double（8字节）。</li>
 <li><strong>字符类型</strong>：char（2字节）。</li>
 <li><strong>布尔类型</strong>：boolean（理论上1位，实际实现中通常是1字节）。</li>
</ul> 
<h3>2. 请解释一下自动装箱和拆箱</h3> 
<ul>
 <li><strong>自动装箱</strong>：是指将基本数据类型自动转换为对应的包装类对象。例如，<code>int i = 10; Integer integer = i;</code> 这里<code>int</code>类型的<code>i</code>自动装箱成了<code>Integer</code>类型的<code>integer</code>。</li>
 <li><strong>自动拆箱</strong>：是指将包装类对象自动转换为对应的基本数据类型。例如，<code>Integer integer = 20; int j = integer;</code> 这里<code>Integer</code>类型的<code>integer</code>自动拆箱成了<code>int</code>类型的<code>j</code>。</li>
</ul> 
<h3>3. 简述String、StringBuilder和StringBuffer的区别</h3> 
<ul>
 <li><strong>可变性</strong>：
  <ul>
   <li><code>String</code>是不可变的，一旦创建，其值不能被修改。每次对<code>String</code>进行操作都会创建一个新的<code>String</code>对象。例如，<code>String s = "hello"; s = s + "world";</code> 在执行<code>s = s + "world";</code>时，会创建一个新的<code>String</code>对象，内容为<code>"helloworld"</code>，原来的<code>"hello"</code>对象依然存在于内存中，只是<code>String</code>类型的变量<code>s</code>指向了新的对象。</li>
   <li><code>StringBuilder</code>和<code>StringBuffer</code>是可变的，它们可以在原对象上进行修改，不会创建新对象。例如，<code>StringBuilder sb = new StringBuilder("hello"); sb.append("world");</code> 这里<code>sb</code>对象本身被修改，其内容变为<code>"helloworld"</code>，而不是创建一个新的对象。</li>
  </ul> </li>
 <li><strong>线程安全性</strong>：
  <ul>
   <li><code>String</code>是线程安全的，因为它是不可变的，多个线程同时访问同一个<code>String</code>对象时，不会出现数据不一致的问题。</li>
   <li><code>StringBuffer</code>是线程安全的，它的方法都使用了<code>synchronized</code>关键字进行同步。例如，<code>StringBuffer sb = new StringBuffer(); sb.append("a");</code> 当多个线程同时调用<code>sb.append("a");</code>时，由于<code>synchronized</code>的存在，同一时间只有一个线程能够执行该方法，保证了线程安全。</li>
   <li><code>StringBuilder</code>是非线程安全的，但其性能比<code>StringBuffer</code>高，因为不需要进行同步操作。在单线程环境下，使用<code>StringBuilder</code>进行字符串操作可以获得更好的性能。例如，在一个只在单线程中执行的方法中，频繁进行字符串拼接操作，使用<code>StringBuilder</code>会比<code>StringBuffer</code>更高效。</li>
  </ul> </li>
 <li><strong>应用场景</strong>：
  <ul>
   <li>如果字符串操作较少，使用<code>String</code>。例如，只是定义一个固定的字符串常量，如<code>String message = "This is a message";</code></li>
   <li>如果是单线程环境下进行大量字符串拼接，使用<code>StringBuilder</code>。比如在一个单线程的日志记录方法中，需要不断拼接日志信息，使用<code>StringBuilder</code>能提高效率。</li>
   <li>如果是多线程环境下进行大量字符串拼接，使用<code>StringBuffer</code>。例如在一个多线程的网络通信模块中，多个线程需要向同一个字符串缓冲区中追加数据，就需要使用<code>StringBuffer</code>来保证线程安全。</li>
  </ul> </li>
</ul> 
<h2>二、面向对象</h2> 
<h3>1. 什么是面向对象编程的三大特性？</h3> 
<p>面向对象编程的三大特性是封装、继承和多态。</p> 
<ul>
 <li><strong>封装</strong>：是指将数据和操作数据的方法绑定在一起，隐藏对象的内部实现细节，只对外提供必要的接口。这样可以提高代码的安全性和可维护性。例如，一个银行账户类<code>BankAccount</code>，将账户余额<code>balance</code>这个数据以及存款<code>deposit</code>、取款<code>withdraw</code>等操作方法封装在类中，外部代码只能通过调用这些公开的方法来操作账户余额，而不能直接访问和修改<code>balance</code>属性，保证了数据的安全性。</li>
 <li><strong>继承</strong>：是指一个类可以继承另一个类的属性和方法，被继承的类称为父类（基类），继承的类称为子类（派生类）。继承可以实现代码的复用和扩展。例如，有一个父类<code>Animal</code>，具有<code>eat</code>方法，子类<code>Dog</code>继承自<code>Animal</code>，那么<code>Dog</code>类就自动拥有了<code>eat</code>方法，同时还可以根据<code>Dog</code>类的特点添加自己特有的方法，如<code>bark</code>，这就是对父类功能的扩展。</li>
 <li><strong>多态</strong>：是指同一个方法调用可以根据对象的不同类型表现出不同的行为。多态通过继承、接口和方法重写来实现。例如，父类<code>Shape</code>有一个<code>draw</code>方法，子类<code>Circle</code>和<code>Rectangle</code>都继承自<code>Shape</code>并重写了<code>draw</code>方法。当创建<code>Circle</code>和<code>Rectangle</code>的对象并调用<code>draw</code>方法时，会根据对象的实际类型（<code>Circle</code>或<code>Rectangle</code>）调用各自重写后的<code>draw</code>方法，从而表现出不同的绘制行为。</li>
</ul> 
<h3>2. 请解释一下方法重载和方法重写</h3> 
<ul>
 <li><strong>方法重载（Overloading）</strong>：是指在同一个类中，多个方法可以有相同的方法名，但参数列表不同（参数的类型、个数或顺序不同）。例如，在一个<code>Calculator</code>类中，可以定义多个<code>add</code>方法：</li>
</ul> 
<pre><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Calculator</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">int</span> a<span class="token punctuation">,</span> <span class="token keyword">int</span> b<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        <span class="token keyword">return</span> a <span class="token operator">+</span> b<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">public</span> <span class="token keyword">double</span> <span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">double</span> a<span class="token punctuation">,</span> <span class="token keyword">double</span> b<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        <span class="token keyword">return</span> a <span class="token operator">+</span> b<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">int</span> a<span class="token punctuation">,</span> <span class="token keyword">int</span> b<span class="token punctuation">,</span> <span class="token keyword">int</span> c<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        <span class="token keyword">return</span> a <span class="token operator">+</span> b <span class="token operator">+</span> c<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 
<p>这里定义了三个<code>add</code>方法，分别接收不同类型和个数的参数，这就是方法重载。调用时，编译器会根据传入参数的实际情况来决定调用哪个<code>add</code>方法。</p> 
<ul>
 <li><strong>方法重写（Overriding）</strong>：是指子类重写父类中具有相同方法名、参数列表和返回值类型的方法。重写时，子类的方法访问权限不能低于父类的方法，抛出的异常范围不能比父类大。例如：</li>
</ul> 
<pre><code class="lang-java"><span class="token keyword">class</span> <span class="token class-name">Animal</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">makeSound</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Animal makes a sound"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">class</span> <span class="token class-name">Dog</span> <span class="token keyword">extends</span> <span class="token class-name">Animal</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">makeSound</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Dog barks"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 
<p>在这个例子中，<code>Dog</code>类重写了<code>Animal</code>类的<code>makeSound</code>方法，当创建<code>Dog</code>类的对象并调用<code>makeSound</code>方法时，会执行<code>Dog</code>类中重写后的方法，输出<code>"Dog barks"</code>。</p> 
<h2>三、多线程与并发</h2> 
<h3>1. 如何创建一个线程？</h3> 
<p>在Java中创建线程有三种方式：</p> 
<ul>
 <li><strong>继承Thread类</strong>：</li>
</ul> 
<pre><code class="lang-java"><span class="token keyword">class</span> <span class="token class-name">MyThread</span> <span class="token keyword">extends</span> <span class="token class-name">Thread</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">run</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Thread is running"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Main</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span>String<span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        MyThread myThread <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">MyThread</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        myThread<span class="token punctuation">.</span><span class="token function">start</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 
<p>在这个例子中，定义了一个继承自<code>Thread</code>类的<code>MyThread</code>类，重写了<code>run</code>方法，然后在<code>main</code>方法中创建<code>MyThread</code>类的对象并调用<code>start</code>方法启动线程。</p> 
<ul>
 <li><strong>实现Runnable接口</strong>：</li>
</ul> 
<pre><code class="lang-java"><span class="token keyword">class</span> <span class="token class-name">MyRunnable</span> <span class="token keyword">implements</span> <span class="token class-name">Runnable</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">run</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Runnable is running"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Main</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span>String<span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        MyRunnable myRunnable <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">MyRunnable</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Thread thread <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Thread</span><span class="token punctuation">(</span>myRunnable<span class="token punctuation">)</span><span class="token punctuation">;</span>
        thread<span class="token punctuation">.</span><span class="token function">start</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 
<p>这里定义了一个实现<code>Runnable</code>接口的<code>MyRunnable</code>类，实现了<code>run</code>方法。在<code>main</code>方法中，创建<code>MyRunnable</code>类的对象，并将其作为参数传递给<code>Thread</code>类的构造函数来创建线程，最后调用<code>start</code>方法启动线程。</p> 
<ul>
 <li><strong>实现Callable接口</strong>：</li>
</ul> 
<pre><code class="lang-java"><span class="token keyword">import</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>concurrent<span class="token punctuation">.</span>Callable<span class="token punctuation">;</span>
<span class="token keyword">import</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>concurrent<span class="token punctuation">.</span>ExecutionException<span class="token punctuation">;</span>
<span class="token keyword">import</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>concurrent<span class="token punctuation">.</span>FutureTask<span class="token punctuation">;</span>
<span class="token keyword">class</span> <span class="token class-name">MyCallable</span> <span class="token keyword">implements</span> <span class="token class-name">Callable</span><span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> String <span class="token function">call</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token keyword">throws</span> Exception <span class="token punctuation">{
   <!-- --></span>
        <span class="token keyword">return</span> <span class="token string">"Callable task completed"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Main</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span>String<span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        MyCallable myCallable <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">MyCallable</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        FutureTask<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> futureTask <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">FutureTask</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span>myCallable<span class="token punctuation">)</span><span class="token punctuation">;</span>
        Thread thread <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Thread</span><span class="token punctuation">(</span>futureTask<span class="token punctuation">)</span><span class="token punctuation">;</span>
        thread<span class="token punctuation">.</span><span class="token function">start</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">try</span> <span class="token punctuation">{
   <!-- --></span>
            String result <span class="token operator">=</span> futureTask<span class="token punctuation">.</span><span class="token function">get</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">InterruptedException</span> <span class="token operator">|</span> ExecutionException e<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
            e<span class="token punctuation">.</span><span class="token function">printStackTrace</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 
<p>此方式定义了一个实现<code>Callable</code>接口的<code>MyCallable</code>类，实现了<code>call</code>方法，该方法可以有返回值并且可以抛出异常。在<code>main</code>方法中，创建<code>MyCallable</code>类的对象，将其封装在<code>FutureTask</code>中，再通过<code>FutureTask</code>创建线程并启动。最后通过<code>futureTask.get()</code>方法获取<code>call</code>方法的返回值。</p> 
<h3>2. 什么是线程安全问题？</h3> 
<p>当多个线程同时访问共享资源时，可能会导致数据不一致、脏读、幻读等问题，这就是线程安全问题。例如，假设有一个银行账户类<code>BankAccount</code>，其中有一个余额属性<code>balance</code>和一个取款方法<code>withdraw</code>：</p> 
<pre><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">BankAccount</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> balance <span class="token operator">=</span> <span class="token number">1000</span><span class="token punctuation">;</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">withdraw</span><span class="token punctuation">(</span><span class="token keyword">int</span> amount<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span>balance <span class="token operator">&gt;=</span> amount<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
            <span class="token keyword">try</span> <span class="token punctuation">{
   <!-- --></span>
                Thread<span class="token punctuation">.</span><span class="token function">sleep</span><span class="token punctuation">(</span><span class="token number">100</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">InterruptedException</span> e<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
                e<span class="token punctuation">.</span><span class="token function">printStackTrace</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span>
            balance <span class="token operator">=</span> balance <span class="token operator">-</span> amount<span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">getBalance</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        <span class="token keyword">return</span> balance<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 
<p>现在有两个线程同时调用<code>withdraw</code>方法进行取款操作：</p> 
<pre><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Main</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span>String<span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        BankAccount account <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">BankAccount</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Thread thread1 <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Thread</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token punctuation">{
   <!-- --></span>
            account<span class="token punctuation">.</span><span class="token function">withdraw</span><span class="token punctuation">(</span><span class="token number">500</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Thread thread2 <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Thread</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token punctuation">{
   <!-- --></span>
            account<span class="token punctuation">.</span><span class="token function">withdraw</span><span class="token punctuation">(</span><span class="token number">300</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        thread1<span class="token punctuation">.</span><span class="token function">start</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        thread2<span class="token punctuation">.</span><span class="token function">start</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">try</span> <span class="token punctuation">{
   <!-- --></span>
            thread1<span class="token punctuation">.</span><span class="token function">join</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            thread2<span class="token punctuation">.</span><span class="token function">join</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">InterruptedException</span> e<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
            e<span class="token punctuation">.</span><span class="token function">printStackTrace</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Final balance: "</span> <span class="token operator">+</span> account<span class="token punctuation">.</span><span class="token function">getBalance</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 
<p>由于<code>withdraw</code>方法中存在<code>Thread.sleep(100);</code>模拟业务逻辑处理时间，当两个线程同时执行到<code>if (balance &gt;= amount);</code>判断时，都可能认为余额足够，然后分别进行取款操作，导致最终余额出现错误。这就是典型的线程安全问题。</p> 
<h3>3. 解决线程安全问题的方法</h3> 
<ul>
 <li><strong>使用synchronized关键字</strong>：可以修饰方法或代码块，保证同一时间只有一个线程可以访问被修饰的资源。例如，将上述<code>BankAccount</code>类的<code>withdraw</code>方法修改为：</li>
</ul> 
<pre><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">BankAccount</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> balance <span class="token operator">=</span> <span class="token number">1000</span><span class="token punctuation">;</span>
    <span class="token keyword">public</span> <span class="token keyword">synchronized</span> <span class="token keyword">void</span> <span class="token function">withdraw</span><span class="token punctuation">(</span><span class="token keyword">int</span> amount<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span>balance <span class="token operator">&gt;=</span> amount<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
            <span class="token keyword">try</span> <span class="token punctuation">{
   <!-- --></span>
                Thread<span class="token punctuation">.</span><span class="token function">sleep</span><span class="token punctuation">(</span><span class="token number">100</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">InterruptedException</span> e<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
                e<span class="token punctuation">.</span><span class="token function">printStackTrace</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span>
            balance <span class="token operator">=</span> balance <span class="token operator">-</span> amount<span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">getBalance</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        <span class="token keyword">return</span> balance<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 
<p>此时，当一个线程进入<code>withdraw</code>方法时，其他线程必须等待该线程执行完毕才能进入，从而保证了线程安全。</p> 
<ul>
 <li><strong>使用Lock接口</strong>：如<code>ReentrantLock</code>，它提供了更灵活的锁机制。例如：</li>
</ul> 
<pre><code class="lang-java"><span class="token keyword">import</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>concurrent<span class="token punctuation">.</span>locks<span class="token punctuation">.</span>Lock<span class="token punctuation">;</span>
<span class="token keyword">import</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>concurrent<span class="token punctuation">.</span>locks<span class="token punctuation">.</span>ReentrantLock<span class="token punctuation">;</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">BankAccount</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> balance <span class="token operator">=</span> <span class="token number">1000</span><span class="token punctuation">;</span>
    <span class="token keyword">private</span> Lock lock <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ReentrantLock</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">withdraw</span><span class="token punctuation">(</span><span class="token keyword">int</span> amount<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        lock<span class="token punctuation">.</span><span class="token function">lock</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">try</span> <span class="token punctuation">{
   <!-- --></span>
            <span class="token keyword">if</span> <span class="token punctuation">(</span>balance <span class="token operator">&gt;=</span> amount<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
                <span class="token keyword">try</span> <span class="token punctuation">{
   <!-- --></span>
                    Thread<span class="token punctuation">.</span><span class="token function">sleep</span><span class="token punctuation">(</span><span class="token number">100</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">InterruptedException</span> e<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
                    e<span class="token punctuation">.</span><span class="token function">printStackTrace</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token punctuation">}</span>
                balance <span class="token operator">=</span> balance <span class="token operator">-</span> amount<span class="token punctuation">;</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span> <span class="token keyword">finally</span> <span class="token punctuation">{
   <!-- --></span>
            lock<span class="token punctuation">.</span><span class="token function">unlock</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">getBalance</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        <span class="token keyword">return</span> balance<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 
<p>在这个例子中，通过<code>ReentrantLock</code>的<code>lock</code>和<code>unlock</code>方法来手动控制锁的获取和释放，在<code>try - finally</code>块中释放锁，确保即使出现异常也能正确释放锁，避免死锁。</p> 
<ul>
 <li><strong>使用并发集合</strong>：如<code>ConcurrentHashMap</code>、<code>CopyOnWriteArrayList</code>等，这些集合在设计上已经考虑了线程安全问题。例如，使用<code>ConcurrentHashMap</code>来存储数据：</li>
</ul> 
<pre><code class="lang-java"><span class="token keyword">import</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>concurrent<span class="token punctuation">.</span>ConcurrentHashMap<span class="token punctuation">;</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Main</span> <span class="token punctuation">{
   <!-- --></span>
    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span>String<span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
        ConcurrentHashMap<span class="token operator">&lt;</span>String<span class="token punctuation">,</span> Integer<span class="token operator">&gt;</span> map <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ConcurrentHashMap</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Thread thread1 <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Thread</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token punctuation">{
   <!-- --></span>
            map<span class="token punctuation">.</span><span class="token function">put</span><span class="token punctuation">(</span><span class="token string">"key1"</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        Thread thread2 <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Thread</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token punctuation">{
   <!-- --></span>
            map<span class="token punctuation">.</span><span class="token function">put</span><span class="token punctuation">(</span><span class="token string">"key2"</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        thread1<span class="token punctuation">.</span><span class="token function">start</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        thread2<span class="token punctuation">.</span><span class="token function">start</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">try</span> <span class="token punctuation">{
   <!-- --></span>
            thread1<span class="token punctuation">.</span><span class="token function">join</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            thread2<span class="token punctuation">.</span><span class="token function">join</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">InterruptedException</span> e<span class="token punctuation">)</span> <span class="token punctuation">{
   <!-- --></span>
            e<span class="token punctuation">.</span><span class="token function">printStackTrace</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>map<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 
<p><code>ConcurrentHashMap</code>允许多个线程同时进行读操作，并且在写操作时采用了分段锁等机制，大大提高了并发性能，同时保证了线程安全。</p> 
<h2>四、集合框架</h2> 
<h3>1. 简述ArrayList和LinkedList的区别</h3> 
<ul>
 <li><strong>数据结构</strong>：
  <ul>
   <li><code>ArrayList</code>是基于动态数组实现的，它可以随机访问元素，通过索引可以快速定位元素。例如，<code>ArrayList&lt;Integer&gt; list = new ArrayList&lt;&gt;(); list.add(1); list.add(2); int value = list.get(1);</code> 这里通过<code>list.get(1);</code>可以直接获取索引为1的元素，时间复杂度为O(1)。</li>
   <li><code>LinkedList</code>是基于双向链表实现的，每个节点包含数据和指向前一个节点和后一个节点的引用。例如，在<code>LinkedList</code>中插入一个元素时，只需要修改相关节点的引用即可，对于在链表中间插入元素的操作，时间复杂度为O(1)。</li>
  </ul> </li>
 <li><strong>性能</strong>：
  <ul>
   <li><strong>随机访问</strong>：<code>ArrayList</code>的随机访问性能更好，时间复杂度为O(1)。因为它可以通过数组的索引直接定位到元素在内存中的位置。</li>
   <li><strong>插入和删除</strong>：<code>LinkedList</code>在插入和删除元素时性能更好，尤其是在列表中间插入或删除元素，时间复杂度为O(1)。而<code>ArrayList</code>在插入和删除元素时需要移动元素，时间复杂度为O(n)。例如，在<code>ArrayList</code>的中间位置插入一个元素，需要将插入位置后面的所有元素向后移动一位。</li>
  </ul> </li>
 <li><strong>内存占用</strong>：
  <ul>
   <li><code>ArrayList</code>会预先分配一定的内存空间，可能会造成内存浪费。如果预先分配的空间过大，而实际存储的元素较少，就会有一部分内存没有被充分利用。</li>
   <li><code>LinkedList</code>每个节点需要额外的引用，会占用更多的内存。因为每个节点除了存储数据外，还需要存储指向前一个节点和后一个节点的引用。</li>
  </ul> </li>
</ul> 
<h3>2. 请解释一下HashMap的工作原理</h3> 
<p><code>HashMap</code>是基于哈希表实现的，它通过<code>key</code>的<code>hashCode()</code>方法计算哈希值，然后根据哈希值找到对应的桶（数组的索引位置）。</p> 
<ul>
 <li><strong>存储过程</strong>：当添加一个键值对时，首先计算<code>key</code>的哈希值，例如<code>int hash = key.hashCode();</code> 然后通过哈希值与数组长度进行取模运算得到桶的索引位置，即<code>int index = hash % table.length;</code> 如果该桶为空，直接将键值对封装成一个<code>Entry</code>对象存储在该桶中。如果该桶不为空，就发生了哈希冲突。在JDK 1.7及之前，采用链表法来解决冲突，即新的键值对会被添加到链表的头部（后插入的元素在链表头部）。在JDK 8及以后，当链表长度达到8且数组长度达到64时，链表会转换为红黑树，以提高查找效率。例如：</li>
</ul> 
<h3>2. 请解释一下HashMap的工作原理</h3> 
<p>HashMap 是一种常用的数据结构，用于存储键值对（key-value pairs），并能高效地根据键（key）进行查找、插入和删除操作。下面详细解释其工作原理：</p> 
<ol>
 <li>基本结构：数组 + 链表 / 红黑树<br>HashMap 本质上是一个 哈希表（Hash Table），其核心结构是一个 数组，每个数组元素称为一个 桶（bucket） 或 槽（slot）。当发生哈希冲突时，桶内会以 链表 或 红黑树 的形式存储多个元素。</li>
</ol> 
<p>JDK 8 及以后：当链表长度超过阈值（默认 8）且数组长度 ≥ 64 时，链表会转换为红黑树，以提高查找效率（时间复杂度从 O (n) 降为 O (log n)）。</p> 
<ol>
 <li><p>哈希函数与索引计算<br>HashMap 使用键的 hashCode() 方法计算哈希值，然后通过 哈希值与数组长度取模 确定元素在数组中的位置：</p> <pre><code class="lang-java">index <span class="token operator">=</span> <span class="token punctuation">(</span>n <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">&amp;</span> hash  <span class="token comment">// 等效于 hash % n，但位运算效率更高</span>
</code></pre> </li>
 <li><p>哈希冲突的处理<br>当两个不同的键计算出相同的索引时，就会发生 哈希冲突。HashMap 使用 链地址法（Chaining） 解决冲突：</p> </li>
</ol> 
<p>链表：冲突的元素会被添加到对应桶的链表中。<br>红黑树：当链表长度超过阈值（默认 8）且数组长度 ≥ 64 时，链表会转换为红黑树，以优化查找性能。</p> 
<ol>
 <li>插入与查找流程<br>插入（put）流程：<br>计算键的哈希值，确定数组索引。<br>若桶为空，直接插入新节点。<br>若桶不为空：<br>若为链表，遍历链表，找到相同键则覆盖值，否则插入尾部。<br>若为红黑树，调用树的插入方法。<br>插入后检查链表长度是否超过阈值（8），若是则转换为红黑树。<br>检查元素总数是否超过扩容阈值（容量 × 负载因子），若是则扩容。<br>查找（get）流程：<br>计算键的哈希值，确定数组索引。<br>若桶为空，返回 null。<br>若为链表，遍历链表查找键。<br>若为红黑树，调用树的查找方法。</li>
 <li>扩容机制<br>当 HashMap 中的元素数量超过 扩容阈值（threshold） 时，会触发扩容：</li>
</ol> 
<p>扩容阈值 = 数组容量 × 负载因子（默认 0.75）。<br>扩容步骤：<br>创建一个新数组，容量为原数组的 2 倍。<br>重新计算每个元素的哈希值和索引，将所有元素迁移到新数组中。<br>容量要求：数组长度始终为 2 的幂次方，确保 (n - 1) &amp; hash 等效于取模运算。</p> 
<ol>
 <li><p>关键特性<br>无序性：元素的存储顺序与插入顺序无关。<br>允许 null 键和 null 值：null 键始终存储在数组的第一个位置（索引 0）。<br>非线程安全：多线程环境下需使用 ConcurrentHashMap 或通过 Collections.synchronizedMap 包装。<br>初始容量与负载因子：<br>初始容量（默认 16）：创建 HashMap 时的数组大小。<br>负载因子（默认 0.75）：控制扩容的时机，过小会频繁扩容，过大会增加哈希冲突。<br>示例代码<br>以下是一个简单的 HashMap 使用示例：</p> <p>```java<br>import java.util.HashMap;</p> </li>
</ol> 
<p>public class HashMapExample {
 <!-- --><br> public static void main(String[] args) {
 <!-- --><br> // 创建 HashMap，键为 String，值为 Integer<br> HashMap map = new HashMap&lt;&gt;();</p> 
<pre><code>    // 插入元素
    map.put("apple", 1);
    map.put("banana", 2);
    map.put(null, 0); // 允许 null 键

    // 查找元素
    System.out.println(map.get("apple")); // 输出: 1
    System.out.println(map.get(null));   // 输出: 0

    // 遍历元素
    for (String key : map.keySet()) {
        System.out.println(key + ": " + map.get(key));
    }
}
</code></pre>
<p>}<br>```<br>总结<br>HashMap 通过哈希函数将键映射到数组索引，并使用链表或红黑树处理冲突，从而实现高效的插入、查找和删除操作。其核心优势在于 平均时间复杂度为 O (1)，但需注意哈希冲突和扩容对性能的影响。<br>Java 面试题，2025 面试题，Java 基础面试题，Java 多线程面试题，JVM 面试题，Spring 面试</p> 

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;

public class GoBoard extends JPanel {
    private static final int BOARD_SIZE = 19; // 19x19 标准围棋棋盘
    private static final int CELL_SIZE = 30; // 每个格子的像素大小
    private static final int MARGIN = 30; // 边距

    // 棋子状态: 0=空, 1=黑子, 2=白子
    private int[][] boardState = new int[BOARD_SIZE][BOARD_SIZE];

    // 当前玩家: 1=黑, 2=白
    private int currentPlayer = 1;

    public GoBoard() {
        setPreferredSize(new Dimension(
                BOARD_SIZE * CELL_SIZE + 2 * MARGIN,
                BOARD_SIZE * CELL_SIZE + 2 * MARGIN
        ));

        // 添加鼠标监听器处理落子
        addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                handleClick(e.getX(), e.getY());
            }
        });
    }

    private void handleClick(int x, int y) {
        // 转换为棋盘坐标
        int boardX = (x - MARGIN + CELL_SIZE / 2) / CELL_SIZE;
        int boardY = (y - MARGIN + CELL_SIZE / 2) / CELL_SIZE;

        // 检查是否在棋盘范围内
        if (boardX >= 0 && boardX < BOARD_SIZE && boardY >= 0 && boardY < BOARD_SIZE) {
            // 检查该位置是否已有棋子
            if (boardState[boardX][boardY] == 0) {
                // 落子
                boardState[boardX][boardY] = currentPlayer;

                // 切换玩家
                currentPlayer = (currentPlayer == 1) ? 2 : 1;

                // 重绘棋盘
                repaint();
            } else {
                // 位置已有棋子，可以添加提示音或消息
                Toolkit.getDefaultToolkit().beep();
            }
        }
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

        // 设置抗锯齿
        Graphics2D g2d = (Graphics2D) g;
        g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);

        // 绘制棋盘背景
        g2d.setColor(new Color(220, 179, 92)); // 木质颜色
        g2d.fillRect(0, 0, getWidth(), getHeight());

        // 绘制网格线
        g2d.setColor(Color.BLACK);
        for (int i = 0; i < BOARD_SIZE; i++) {
            // 横线
            g2d.drawLine(
                    MARGIN,
                    MARGIN + i * CELL_SIZE,
                    MARGIN + (BOARD_SIZE - 1) * CELL_SIZE,
                    MARGIN + i * CELL_SIZE
            );
            // 竖线
            g2d.drawLine(
                    MARGIN + i * CELL_SIZE,
                    MARGIN,
                    MARGIN + i * CELL_SIZE,
                    MARGIN + (BOARD_SIZE - 1) * CELL_SIZE
            );
        }

        // 绘制天元和星位
        int[] starPoints = {3, 9, 15}; // 19路棋盘的星位坐标
        for (int x : starPoints) {
            for (int y : starPoints) {
                g2d.fillOval(
                        MARGIN + x * CELL_SIZE - 4,
                        MARGIN + y * CELL_SIZE - 4,
                        8, 8
                );
            }
        }

        // 绘制棋子
        for (int i = 0; i < BOARD_SIZE; i++) {
            for (int j = 0; j < BOARD_SIZE; j++) {
                if (boardState[i][j] != 0) {
                    if (boardState[i][j] == 1) {
                        g2d.setColor(Color.BLACK); // 黑子
                    } else {
                        g2d.setColor(Color.WHITE); // 白子
                    }

                    // 绘制棋子
                    g2d.fillOval(
                            MARGIN + i * CELL_SIZE - CELL_SIZE / 2,
                            MARGIN + j * CELL_SIZE - CELL_SIZE / 2,
                            CELL_SIZE, CELL_SIZE
                    );

                    // 为白子添加黑色边框
                    if (boardState[i][j] == 2) {
                        g2d.setColor(Color.BLACK);
                        g2d.drawOval(
                                MARGIN + i * CELL_SIZE - CELL_SIZE / 2,
                                MARGIN + j * CELL_SIZE - CELL_SIZE / 2,
                                CELL_SIZE, CELL_SIZE
                        );
                    }
                }
            }
        }

        // 显示当前玩家
        g2d.setColor(Color.BLACK);
        g2d.setFont(new Font("Arial", Font.BOLD, 16));
        String playerText = (currentPlayer == 1) ? "Player: Black" : "Player: White";
        g2d.drawString(playerText, MARGIN, 20);
    }

    // 重置棋盘
    public void resetBoard() {
        boardState = new int[BOARD_SIZE][BOARD_SIZE];
        currentPlayer = 1;
        repaint();
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            JFrame frame = new JFrame("围棋棋盘");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

            GoBoard board = new GoBoard();
            frame.add(board, BorderLayout.CENTER);

            // 添加重置按钮
            JButton resetButton = new JButton("重置棋盘");
            resetButton.addActionListener(e -> board.resetBoard());

            JPanel buttonPanel = new JPanel();
            buttonPanel.add(resetButton);
            frame.add(buttonPanel, BorderLayout.SOUTH);

            frame.pack();
            frame.setLocationRelativeTo(null);
            frame.setVisible(true);
        });
    }
}
```


