---


---

<h1 id="typescript-compiler">TypeScript Compiler</h1>
<h3 id="basics">BASICS</h3>
<p>When you run the command ‘tsc’, the .ts files are compiled into .js files.</p>
<pre><code>let myName : string = "Max"
</code></pre>
<p>gets compiled to</p>
<pre><code>var myName = "Max";
</code></pre>
<hr>
<h3 id="tsconfig.json">TSCONFIG.JSON</h3>
<h5 id="noemitonerror">NOEMITONERROR</h5>
<p>Even if you get a compilation error, you do get a JavaScript File.<br>
But you can suppress this behavior by going to tscconfig.json:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">compileOptions target <span class="token punctuation">{</span>
	    <span class="token string">"compilerOptions"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
		    <span class="token string">"module"</span><span class="token punctuation">:</span> <span class="token string">"commonjs"</span><span class="token punctuation">,</span>
		    <span class="token string">"target"</span><span class="token punctuation">:</span> <span class="token string">"es5"</span><span class="token punctuation">,</span> 
		    <span class="token string">"noImplicitAny"</span><span class="token punctuation">:</span> <span class="token string">"false"</span><span class="token punctuation">,</span>
		    <span class="token string">"sourceMap"</span><span class="token punctuation">:</span> <span class="token boolean">false</span>
	    <span class="token punctuation">}</span><span class="token punctuation">,</span>
	    <span class="token string">"exclude"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
		    <span class="token string">"node_modules"</span> 
	    <span class="token punctuation">}</span>   
	<span class="token punctuation">}</span>
</code></pre>
<p>Under compiler options, you can add:</p>
<pre><code>"noEmitOnError": true // default is false
</code></pre>
<p>Now you shouldn’t get a .js file if the tsc file detects an error.</p>
<h5 id="sourcemap">SOURCEMAP</h5>
<pre><code>"sourceMap": true // default: false
</code></pre>
<p>When you compile, you get a .map file.</p>
<p>Whats the advantage of this source map?</p>
<p>Click on sources in chrome dev tools. You’ll actually see the app.js file AND app.ts file. You can click into it, and set a breakpoint in it. Thus, with this true, we can debug a .ts file directly in the browser.</p>
<h5 id="noimplicitany">NOIMPLICITANY</h5>
<pre><code>"noImplicitAny": true // default: false
</code></pre>
<p>Don’t allow for implicit anys.</p>
<pre><code>let anything;
anything = 12;
</code></pre>
<p>Anything is of type any because we didn’t set it. You don’t get an error, unless noImplicitAny is true.</p>
<p>Note if you set it to true, you could still do</p>
<pre><code>anything : any = 12
</code></pre>
<p>because this isn’t an implicit any.</p>
<h5 id="strictnullchecks">STRICTNULLCHECKS</h5>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">function</span> <span class="token function">controlMe</span><span class="token punctuation">(</span>isTrue<span class="token punctuation">:</span> boolean<span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">let</span> result<span class="token punctuation">:</span> number<span class="token punctuation">;</span>
	<span class="token keyword">if</span><span class="token punctuation">(</span>isTrue<span class="token punctuation">)</span> <span class="token punctuation">{</span>
		result <span class="token operator">=</span> <span class="token number">12</span><span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
	<span class="token keyword">return</span> result<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>If not isTrue, then result is null, which could lead to problems in your code.</p>
<pre><code>"strictNullChecks": true
</code></pre>
<p>Now, the compiler analyzes which part of your code you can reach and will fail because result could possibly be null</p>
<h5 id="nounusedparameters">NOUNUSEDPARAMETERS</h5>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">function</span> <span class="token function">controlMe</span><span class="token punctuation">(</span>isTrue<span class="token punctuation">:</span> boolean<span class="token punctuation">,</span> somethingElse<span class="token punctuation">:</span> boolean<span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">let</span> result<span class="token punctuation">:</span> number<span class="token punctuation">;</span>
	<span class="token keyword">if</span><span class="token punctuation">(</span>isTrue<span class="token punctuation">)</span> <span class="token punctuation">{</span>
		result <span class="token operator">=</span> <span class="token number">12</span><span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
	<span class="token keyword">return</span> result<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>Setting</p>
<pre><code>"noUnusedParameters": true // default false
</code></pre>
<p>will result in an error because somethingElse is never used</p>
<hr>
<p><strong>Info on TypeScript tsconfig.json</strong><br>
<a href="http://www.typescriptlang.org/docs/handbook/tsconfig-json.html">http://www.typescriptlang.org/docs/handbook/tsconfig-json.html</a></p>
<p><strong>Info on tsc compiler options:</strong><br>
<a href="http://www.typescriptlang.org/docs/handbook/compiler-options.html">http://www.typescriptlang.org/docs/handbook/compiler-options.html</a></p>

