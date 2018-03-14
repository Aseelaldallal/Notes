---


---

<h1 id="setup">SETUP</h1>
<ol>
<li>Node must be installed.</li>
<li>Run <code>npm -g install typescript</code></li>
<li>Open project folder, run <code>npm init</code></li>
<li>Run <code>tsc --init</code> . This will put the folder under control of typescript. It’ll create a tsconfig.json file which tells typescript that this folder is a typescript project and by running tsc, compile all .ts files.</li>
<li>In index.html, add<br>
<code>&lt;script src="./app.js"&gt;&lt;/script&gt;</code></li>
</ol>
<h2 id="lite-server">LITE-SERVER</h2>
<pre><code>npm install lite-server --save-dev
</code></pre>
<p>Will host index.html file, update it automatically when .js file changes. After installing, type npm start, and you’ll be directed to localhost:3000</p>

