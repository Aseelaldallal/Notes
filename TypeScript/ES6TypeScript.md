---


---

<h1 id="es6-and-typescript">ES6 and TypeScript</h1>
<p>TypeScript gives you a lot of access to most ES6 features.</p>
<h2 id="let-and-const">Let and Const</h2>
<p>Let and Const create a block scope variable.<br>
The var keyword creates a global scope variable.</p>
<h2 id="arrow-functions">Arrow Functions</h2>
<p><strong>Regular Function</strong></p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> <span class="token function-variable function">addNumbers</span> <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span>number1<span class="token punctuation">:</span> number<span class="token punctuation">,</span> number2<span class="token punctuation">:</span> number<span class="token punctuation">)</span> <span class="token punctuation">:</span> number <span class="token punctuation">{</span>
	<span class="token keyword">return</span> number1 <span class="token operator">+</span> number2<span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token function">addNumbers</span><span class="token punctuation">(</span><span class="token number">10</span><span class="token punctuation">,</span><span class="token number">21</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>Arrow Function</strong></p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> <span class="token function-variable function">multiplyNumbers</span> <span class="token operator">=</span> <span class="token punctuation">(</span>number1<span class="token punctuation">:</span> number<span class="token punctuation">,</span> number2<span class="token punctuation">:</span> number<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> number1\\<span class="token operator">*</span>number2<span class="token punctuation">;</span>
</code></pre>
<h2 id="default-parameters">Default Parameters</h2>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> countDown <span class="token operator">=</span> <span class="token punctuation">(</span>start<span class="token punctuation">:</span> number<span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token keyword">void</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span> 
	<span class="token keyword">while</span><span class="token punctuation">(</span>start <span class="token operator">&gt;</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	    start<span class="token operator">--</span><span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"DONE: "</span><span class="token punctuation">,</span> start<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token function">countDown</span><span class="token punctuation">(</span><span class="token number">10</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

</code></pre>
<p>But what if countDown is called without Parameters?</p>
<p>We can set a default parameter.</p>
<pre><code>const countDown = (start: number = 10) : void =&gt; {
    while(start &gt; 0) {
	    start--;
    }
    console.log("DONE: ", start);
}
</code></pre>
<p>Now <code>countDown()</code> works. If you pass in 20, it’ll use 20 rather than the default 10.</p>
<h2 id="rest-and-spread-operators">Rest and Spread Operators</h2>
<p>They allow you to work with arrays and lists of data.</p>
<p><strong>Spread Operator</strong></p>
<pre><code>let numbers = \[1,10,9,11\];
console.log(Math.max(1,10,9,11));
</code></pre>
<p>We cant do Math.max(numbers);</p>
<p>Solution: <em>Use Spread Operator</em></p>
<pre><code>console.log(Math.max(...numbers));
</code></pre>
<p><strong>Rest Operator</strong></p>
<pre><code>function makeArray(arg1: number, arg2: number) {
    return [arg1,arg2]
}
</code></pre>
<p>What if you wanted an array with more values, and you didn’t know how many?</p>
<p>Solution: <em>Use Rest Operator</em></p>
<pre><code>function makeArray(...args: number[] {
    return args;
}
</code></pre>
<p>…args will take all parameters and turn them into array. Opposite of spread operator</p>
<p>You can now call makeArray with an arbitrary number of numbers.</p>
<pre><code>console.log(makeArray(1,2,4));
</code></pre>
<h2 id="destructuring">Destructuring</h2>
<pre><code>const myHobbies = ["Cooking", "Sports"];
const hobby1 = myHobbies[0];
const hobby2 = myHobbies[1];
console.log(hobby1, hobby2);
</code></pre>
<p>With destructuring:</p>
<pre><code>const [hobby1, hobby2] = myhobbies;
console.log(hobby1, hobby2);
</code></pre>
<p>You could also destructure with objects.</p>
<pre><code>const userData = {
    username: "hi",
    age: 22
}

const age = userData.age;
const username = userData.username;
console.log(username, age);
</code></pre>
<p>Shorter syntax with Desctructuring:</p>
<pre><code>const {username, age} = userData;
console.log(username, age);
</code></pre>
<p>The name here has to match the field in the object .If you want to use different names for your constants, you can do something like this:</p>
<pre><code>const {username: myName, age: myAge} = userData;
console.log(myName, myAge);
</code></pre>
<p>We used aliases - this is optional.</p>

