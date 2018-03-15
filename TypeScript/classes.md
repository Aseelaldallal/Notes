---


---

<h1 id="classes-in-typescript">Classes in TypeScript</h1>
<h2 id="basic-classes">Basic Classes</h2>
<pre><code>class  Person {

    public  name:  string;
    private  type:  string  =  "human";	    
    protected  age:  number  =  27;
    
    constructor(name:  string, public  username:  string) {	    
	    this.name  =  name;	    
    }
    
    printAge() {  
	    console.log(this.age);	    
	    this.setType("old guy");	    
    }
    
    private  setType(type:  string) {    
	    this.type  =  type;	    
	    console.log(this.type);    
    }
    
}
</code></pre>
<p><strong>Note: Private vs Protected</strong></p>
<p>Private accessible only within Person Object<br>
Protected properties are also accessible in objects that inherit from Person</p>
<p><strong>Note: Shortcut for Creating Property</strong></p>
<pre><code> constructor(name : string, public  username:  string) {...}
</code></pre>
<p>Automatically create a public property called username, and assign the second argument to username</p>
<pre><code>const person = new Person("Aseel", "aseel");    
console.log(person);    
person.printAge();
</code></pre>
<h2 id="inheritance">Inheritance</h2>
<p>Classes can also inherit from each other. This is an ES6 and TypeScript feature.</p>
<pre><code>class  Aseel  extends  Person {
	constructor(username:  string) {
		super("Aseel", username);
		this.age  =  20; // you can do this because age is a protected variable in Person
		//Accessing this.type gives an error, since it's private
	}
}

const  asool  =  new  Aseel("asoola");
console.log(asool);
</code></pre>
<h2 id="getters-and-setters">Getters and Setters</h2>
<pre><code>class  Plant {
    private  _species:  string  =  "Default"; 
    
    // This will be the property name accessible from outside. It will NOT be called like a method, it'll be called like a property
    set species(value:  string) {
    	if (value.length  &gt;  3) {
    		this._species  =  value;
    	}
    }
    
    // So the reason we have _species is that we'll actually get a variable called species
    
    get species() {
    	return  this._species;
    }   
}
</code></pre>
<p><strong>Creating Plant</strong></p>
<pre><code>let  plant  =  new  Plant();
</code></pre>
<p><strong>Getting Species</strong></p>
<pre><code>console.log(plant.species); // note how we're not calling it like a function
</code></pre>
<p><strong>Setting Species</strong></p>
<pre><code>plant.species  =  "Green plant";
console.log(plant.species);
</code></pre>
<h2 id="static-properties-and-methods">Static Properties and Methods</h2>
<p><strong>Normal Classes</strong></p>
<pre><code>class  Helpers {
    PI:  number  =  3.14;
}
</code></pre>
<p>The only way I can access this is by instantiating Helper.</p>
<p><strong>Static Keyword</strong></p>
<p>I can make the PI property accessible outside the class without needing to instantiate Helper.</p>
<pre><code>class  Helper {
	static  PI:  number  =  3.14;
	static  calcCircumference(diameter:  number):  number {
	return (this.PI  =  diameter);
	}
}
console.log(2  *  Helper.PI);
console.log(Helper.calcCircumference(8));
</code></pre>
<p>Mostly use static variables and methods for helper classes.</p>
<h2 id="abstract-classes">ABSTRACT CLASSES</h2>
<p>Abstract classes can’t be instantiated directly. You have to inherit from them. Why do this? Because maybe this class doesn’t need to be instantiated, just needs to provide basic setup</p>
<pre><code>abstract  class  Project {

    protected  projectName:  string  =  "Default";   
    budget:  number  =  200;

    calcBudget() {	    
	    return  this.budget  *  2;	    
    }
    
	// abstract function
    abstract changeName(name:  string):  void;
}
</code></pre>
<p><strong>Abstract Functions</strong></p>
<p>We ONLY define how the function should like like. Abstract on a function means that when you extend the class you MUST IMPLEMENT the abstract method, otherwise you get an error. Notice: No Curly braces.</p>
<pre><code>class  ITProject  extends  Project {
    changeName(name:  string) {    
	    this.projectName  =  name;    
    }
}
let  newProj  =  new  ITProject();
console.log(newProj);    
newProj.changeName("SUPERPRO");    
console.log(newProj);
</code></pre>
<h2 id="singleton-class">SINGLETON CLASS</h2>
<p>Only one instance during runtime. This is useful if you want to have a SINGLE instance of a class. By making constructor private, you can force class to be only used a single time. So you can’t instantiate class from outside.</p>
<pre><code>class  OnlyOne {

private  static  instance:  OnlyOne;    
    private constructor(public  name:  string) {}   
    static getInstance() {   
	    if (!OnlyOne.instance) {   
		    OnlyOne.instance  =  new  OnlyOne("The Only One");    
	    }    
	    return  OnlyOne.instance;    
    }    
}

let right  =  OnlyOne.getInstance();
</code></pre>
<p>You can’t do</p>
<pre><code>	let wrong = new OnlyOne("hello");
</code></pre>
<p>because the constructor is private.</p>
<h2 id="read-only-properties">Read-Only Properties</h2>
<p>*Continuing from above…</p>
<pre><code>console.log(right.name); // this works
</code></pre>
<p>we can also do this</p>
<pre><code>right.name  =  "Something Else";
</code></pre>
<p>What if we want to make sure that we can only set name in the constructor.</p>
<p>Two methods:</p>
<ol>
<li>Specify a getter without setter – result: readonly</li>
<li>Shorter method: use word readonly</li>
</ol>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">class</span>  <span class="token class-name">OnlyOne</span> <span class="token punctuation">{</span>
    <span class="token keyword">private</span>  <span class="token keyword">static</span>  instance<span class="token punctuation">:</span>  OnlyOne<span class="token punctuation">;</span>
    <span class="token keyword">private</span>  <span class="token function">constructor</span><span class="token punctuation">(</span><span class="token keyword">public</span>  readonly  name<span class="token punctuation">:</span>  string<span class="token punctuation">)</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
    <span class="token keyword">static</span>  <span class="token function">getInstance</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>OnlyOne2<span class="token punctuation">.</span>instance<span class="token punctuation">)</span> <span class="token punctuation">{</span>
		    OnlyOne2<span class="token punctuation">.</span>instance  <span class="token operator">=</span>  <span class="token keyword">new</span>  <span class="token class-name">OnlyOne2</span><span class="token punctuation">(</span><span class="token string">"The Only One"</span><span class="token punctuation">)</span><span class="token punctuation">;</span> 
	    <span class="token punctuation">}</span>
	    <span class="token keyword">return</span>  OnlyOne2<span class="token punctuation">.</span>instance<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>

