<h1>Internationalization (I18n) and Localization (L10n)</h1>

<h2>Learning Objectives:</h2>
<ul>
  <li>Learn how to parametrize Flask templates to display different languages</li>
  <li>Learn how to infer the correct locale based on URL parameters, user settings or request headers</li>
  <li>Learn how to localize timestamps</li>
</ul>

<h3>0. Basic Flask app</h3>
<p>First you will setup a basic Flask app in <code>0-app.py</code>. Create a single <code>/</code> route and an <code>index.html</code> template that simply outputs “Welcome to Holberton” as page title (<code>&lt;title&gt;</code>) and “Hello world” as header (<code>&lt;h1&gt;</code>).</p>

<h3>1. Basic Babel setup</h3>
<p>Install the Babel Flask extension:</p>
<pre><code>$ pip3 install flask_babel
</code></pre>
<p>Then instantiate the <code>Babel</code> object in your app. Store it in a module-level variable named <code>babel</code>.</p>
<p>In order to configure available languages in our app, you will create a <code>Config</code> class that has a <code>LANGUAGES</code> class attribute equal to <code>["en", "fr"]</code>.</p>
<p>Use <code>Config</code> to set Babel’s default locale (<code>"en"</code>) and timezone (<code>"UTC"</code>).</p>
<p>Use that class as config for your Flask app.</p>

<h3>2. Get locale from request</h3>
<p>Create a <code>get_locale</code> function with the <code>babel.localeselector</code> decorator. Use <code>request.accept_languages</code> to determine the best match with our supported languages.</p>

<h3>3. Parametrize templates</h3>
<p>Use the <code>_</code> or <code>gettext</code> function to parametrize your templates. Use the message IDs <code>home_title</code> and <code>home_header</code>.</p>
<p>Create a <code>babel.cfg</code> file containing</p>
<pre><code>[python: **.py]
[jinja2: **/templates/**.html]extensions=jinja2.ext.autoescape,jinja2.ext.with_
</code></pre>
<p>Then initialize your translations with</p>
<pre><code>$ pybabel extract -F babel.cfg -o messages.pot .
</code></pre>
<p>and your two dictionaries with</p>
<pre><code>$ pybabel init -i messages.pot -d translations -l en$ pybabel init -i messages.pot -d translations -l fr
</code></pre>
<p>Then edit files <code>translations/[en|fr]/LC_MESSAGES/messages.po</code> to provide the correct value for each message ID for each language. Use the following translations:</p>
<table>
  <tr>
    <th><code>msgid</code></th>
    <th><b>English</b></th>
    <th><b>French</b></th>
  </tr>
  <tr>
    <td><code>home_title</code></td>
    <td><code>"Welcome to Holberton"</code></td>
    <td><code>"Bienvenue chez Holberton"</code></td>
  </tr>
  <tr>
    <td><code>home_header</code></td>
    <td><code>"Hello world!"</code></td>
    <td><code>"Bonjour monde!"</code></td>
  </tr>
</table>
<p>Then compile your dictionaries with</p>
<pre><code>$ pybabel compile -d translations
</code></pre>
<p>Reload the home page of your app and make sure that the correct messages show up.</p>

<h3>4. Force locale with URL parameter</h3>
<p>In this task, you will implement a way to force a particular locale by passing the <code>locale=fr</code> parameter to your app’s URLs.</p>
<p>In your <code>get_locale</code> function, detect if the incoming request contains locale argument and ifs value is a supported locale, return it. If not or if the parameter is not present, resort to the previous default behavior.</p>
<p>Now you should be able to test different translations by visiting <a href="http://127.0.0.1:5000?locale=[fr|en]">http://127.0.0.1:5000?locale=[fr|en]</a>.</p>

<h3>5. Mock logging in</h3>
<p>Creating a user login system is outside the scope of this project. To emulate a similar behavior, copy the following user table in <code>5-app.py</code>.</p>
<pre><code>users = {
    1: {"name": "Balou", "locale": "fr", "timezone": "Europe/Paris"},
    2: {"name": "Beyonce", "locale": "en", "timezone": "US/Central"},
    3: {"name": "Spock", "locale": "kg", "timezone": "Vulcan"},
    4: {"name": "Teletubby", "locale": None, "timezone": "Europe/London"},
}
</code></pre>
<p>This will mock a database user table. Logging in will be mocked by passing <code>login_as</code> URL parameter containing the user ID to log in as.</p>
<p>Define a <code>get_user</code> function that returns a user dictionary or <code>None</code> if the ID cannot be found or if <code>login_as</code> was not passed.</p>
<p>Define a <code>before_request</code> function and use the <code>app.before_request</code> decorator to make it be executed before all other functions. <code>before_request</code> should use <code>get_user</code> to find a user if any, and set it as a global on <code>flask.g.user</code>.</p>
<p>In your HTML template, if a user is logged in, in a paragraph tag, display a welcome message otherwise display a default message as shown in the table below.</p>
<table>
  <tr>
    <th><code>msgid</code></th>
    <th><b>English</b></th>
    <th><b>French</b></th>
  </tr>
  <tr>
    <td><code>logged_in_as</code></td>
    <td><code>"You are logged in as %(username)s."</code></td>
    <td><code>"Vous êtes connecté en tant que %(username)s."</code></td>
  </tr>
  <tr>
    <td><code>not_logged_in</code></td>
    <td><code>"You are not logged in."</code></td>
    <td><code>"Vous n'êtes pas connecté."</code></td>
  </tr>
</table>

<h3>6. Use user locale</h3>
<p>Change your <code>get_locale</code> function to use a user’s preferred local if it is supported.</p>
<p>The order of priority should be</p>
<ol>
  <li>Locale from URL parameters</li>
  <li>Locale from user settings</li>
  <li>Locale from request header</li>
  <li>Default locale</li>
</ol>
<p>Test by logging in as different users</p>

<h3>7. Infer appropriate time zone</h3>
<p>Define a <code>get_timezone</code> function and use the <code>babel.timezoneselector</code> decorator.</p>
<p>The logic should be the same as <code>get_locale</code>:</p>
<ol>
  <li>Find <code>timezone</code> parameter in URL parameters</li>
  <li>Find time zone from user settings</li>
  <li>Default to UTC</li>
</ol>
<p>Before returning a URL-provided or user time zone, you must validate that it is a valid time zone. To that, use <code>pytz.timezone</code> and catch the <code>pytz.exceptions.UnknownTimeZoneError</code> exception.</p>

<h3>8. Display the current time</h3>
<p>Based on the inferred time zone, display the current time on the home page in the default format. For example:</p>
<blockquote>Jan 21, 2020, 5:55:39 AM</blockquote>
<p>or</p>
<blockquote>21 janv. 2020 à 05:56:28</blockquote>
<p>Use the following translations:</p>
<table>
  <tr>
    <th><code>msgid</code></th>
    <th><b>English</b></th>
    <th><b>French</b></th>
  </tr>
  <tr>
    <td><code>current_time_is</code></td>
    <td><code>"The current time is %(current_time)s."</code></td>
    <td><code>"Nous sommes le %(current_time)s."</code></td>
  </tr>
</table>