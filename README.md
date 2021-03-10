# GitHub AS NugetServer
Using Github as Private Nuget Package Server and Share Your Packages

## Before
I spent hours of searching and trying to get my NuGet packages on a private package server so I could use it on several computers and share them with colleagues. In this tip, I show you how easy it is - within 10 minutes, you have it done with a few simple steps.

<h3>Why</h3>

<ul>
	<li>You have class projects and create Nuget packages of them.</li>
	<li>Public sharing is no option.</li>
	<li>You want to share between computers and have it available centrally.</li>
	<li>Perfect, simple, easy to do.</li>
</ul>

<p>This article describes:</p>

<ol>
	<li>Personal</li>
	<li>Organization</li>
</ol>

<h2>1. Personal Private Packages on Github Package</h2>

<h3>Step 1</h3>

<ul>
	<li>Go to Github account &gt;&gt; Open Setting &gt;&gt; Developer setting &gt;&gt; Personal access tokens</li>
	<li>Get personal token &lt;Api-Key&gt;</li>
	<li>Get Github username &lt;Github username&gt;</li>
</ul>

<h3>Step 2</h3>

<p>For sample, just create a new class project with .NET core or newer like at the command prompt as administrator.</p>

<pre lang="text">
dotnet new console --name OctocatApp</pre>

<h3>Step 3</h3>

<p>In the project file, add in the tag propertygroup.</p>

<pre lang="xml">
&lt;RepositoryUrl&gt;https://github.com/&lt;Github username&gt;/&lt;ApplicationName&gt;/&lt;/RepositoryUrl&gt;
&lt;GeneratePackageOnBuild&gt;true&lt;/GeneratePackageOnBuild&gt;&lt;code&gt;</pre>

<ul>
	<li>Replace &lt;Github username&gt;</li>
	<li>Replace &lt;ApplicationName&gt; (example: <code>OctocatApp)</code></li>
</ul>

<h3>Step 4</h3>

<p>In the project root, create <code>NuGet.Config</code> and copy the code below:</p>

<pre lang="xml">
&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
&lt;configuration&gt;
  &lt;packageSources&gt;
    &lt;clear/&gt;
    &lt;add key=&quot;github&quot; value=&quot;https://nuget.pkg.github.com/&lt;Github username&gt;/index.json&quot;/&gt;
  &lt;/packageSources&gt;
  &lt;packageSourceCredentials&gt;
    &lt;github&gt;
      &lt;add key=&quot;Username&quot; value=&quot;&lt;Github username&gt;&quot;/&gt;
      &lt;add key=&quot;ClearTextPassword&quot; value=&quot;&lt;API-Key&gt;&quot;/&gt;
    &lt;/github&gt;
  &lt;/packageSourceCredentials&gt;
&lt;/configuration&gt;</pre>

<ul>
	<li>Replace 2 x &lt;Github username&gt;</li>
	<li>Replace &lt;API-Key&gt;</li>
</ul>

<h4>Note</h4>

<p>Version-number must be unique and unused. Change it in the project file or with project options.</p>

<h3>Step 5</h3>

<p>Push the application to GitHub (create a repo, or let VS do it for you).</p>

<h3>Step 6</h3>

<p>Open a command prompt as administrator in the project folder and type:</p>

<pre lang="text">
dotnet nuget push &quot;bin/Release/&lt;ApplicationName&gt;.1.0.0.nupkg&quot;  --source &quot;github&quot; --api-key <Api key></pre>

<ul>
	<li>Replace &lt;applicationName&gt;</li>
	<li>Update version-number</li>
	<li>Replace &lt;api key&gt;</li>
</ul>

<h2>Finished</h2>

<p>Check in Github packages and see your package.</p>

<h2>Getting It</h2>

<p>Add in VS a package source with <em>https://nuget.pkg.github.com/&lt;Github username&gt;/index.json</em> as source.</p>

<p>The first time, Github asks you the username/password.</p>

<h2>2. Organization Private Packages on Github Packages</h2>

<p>The project needs to be an organization project with members.</p>

<h3>Step 1</h3>

<ul>
	<li>Go to Github account &gt;&gt; Open Setting &gt;&gt; Developer setting &gt;&gt; Personal access tokens</li>
	<li>Get personal token &lt;Api-Key&gt;</li>
	<li>Get Github username &lt;Github username&gt;</li>
	<li>Get OrganizationName &lt;OrganizationName &gt;</li>
</ul>

<h3>Step 2</h3>

<p>For sample, just create a new class project with .NET core or newer like at the command prompt as administrator:</p>

<pre lang="text">
dotnet new console --name OctocatApp</pre>

<h3>Step 3</h3>
<p>In the project file, add in the tag propertygroup.<p/>

<pre lang="xml">
&lt;RepositoryUrl&gt;https://github.com/&lt;OrganizationName&gt;/&lt;ApplicationName&gt;/&lt;/RepositoryUrl&gt;
&lt;GeneratePackageOnBuild&gt;true&lt;/GeneratePackageOnBuild&gt;</pre>

<ul>
	<li>Replace &lt;OrganizationName &gt;</li>
	<li>Replace &lt;ApplicationName&gt; (example: <code>OctocatApp)</code></li>
</ul>

<h3>Step 4</h3>

<p>In the project root, create <code>NuGet.Config</code> and copy the code below:</p>

<pre lang="xml">
&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
&lt;configuration&gt;
  &lt;packageSources&gt;
    &lt;clear/&gt;
    &lt;add key=&quot;github&quot; value=&quot;https://nuget.pkg.github.com/&lt;OrganizationName&gt;/index.json&quot;/&gt;
  &lt;/packageSources&gt;
  &lt;packageSourceCredentials&gt;
    &lt;github&gt;
      &lt;add key=&quot;Username&quot; value=&quot;&lt;Github username&gt;&quot;/&gt;
      &lt;add key=&quot;ClearTextPassword&quot; value=&quot;&lt;API-Key&gt;&quot;/&gt;
    &lt;/github&gt;
  &lt;/packageSourceCredentials&gt;
&lt;/configuration&gt;</pre>

<ul>
	<li>Replace &lt;Github username&gt;</li>
	<li>Replace &lt;OrganizationName &gt;</li>
	<li>Replace &lt;API-Key&gt;</li>
</ul>

<h4>Note</h4>

<p>Version-number must be unique and unused. Change it in the project file or with project options.</p>

<h3>Step 5</h3>

<p>Push the application to GitHub (create a repo, or let VS do it for you).</p>

<h3>Step 6</h3>

<p>Open a command prompt as administrator in the project folder and type:</p>

<pre lang="text">
dotnet nuget push &quot;bin/Release/&lt;ApplicationName&gt;.1.0.0.nupkg&quot;  --source &quot;github&quot;</pre>

<ul>
	<li>Replace &lt;applicationName&gt;</li>
	<li>Replace version-number</li>
</ul>

<h2>Finished</h2>

<p>Check in Github packages and see your package.</p>

<h2>Getting It</h2>

<p>Add in VS a package source with <em>https://nuget.pkg.github.com/&lt;Github username&gt;/index.json</em> as source.</p>

<p>The first time, Github asks you the username/password.</p>

<p>Happy coding!</p>
