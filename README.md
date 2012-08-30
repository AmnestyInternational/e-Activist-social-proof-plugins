# Engaging Networks Social Proof jQuery plugins

Engaging Networks predomininantly provide web applications to the charity sector for campaigning/fundraising purposes. Two of their products, E-Activist and Net Donor, create interfaces to capture supporter data, stored in a database accessible via an API. The web applications' purpose is to provide a WYSIWYG-style interface through which donation and campaigning forms can be generated by the charity, which their supporters can then use to support a cause.

The apps focus mainly on the creation of these forms and the storage of supporter data for the charities, they're less focussed on providing tools to increase social engagement of the campaigns themselves. 

These plugins try to bridge that gap somewhat by providing [Social Proof](http://en.wikipedia.org/wiki/Social_proof) widgets, which can be used on any website, which show the campaigns in action. 

These plugins are for use with jQuery and are used to access Engaging Network's API and generate stylable widgets for use on a charity's website.

3 plugins currently exist

#### [Recent supporter list](#recent-supporter-list-1)
A dynamic list of the supporters who have recently used any given campaigning form or forms. 

(Uses EN's EaDataCapture service.)

#### [Thermometer](#thermometer-1)
A "We have raised this much to rebuild the church roof" style thermometer to indicate the overall success of a campaign, relative to the campaign's goal. This can be used to indicate total donations or total registrations/engagements. 

(Uses EN's EaEmailAOTarget or NetDonor services.)

#### [RollCall](#rollcall-1)
Similar to 'Supporter list' shown above but with the option of fundraising donation amounts from the NetDonor system (e.g. Bob just gave £10). This plugin requires less processing than 'Supporter list' but doesn't include information about how recently an action was taken. 

(Uses EN's two new services, RollCall and FundraisingRollCall, which appear to be intended for use by systems like the Recent Supporter List, but limited in the fields it returns.)


## Global options

All plugins require these options defining as a bear minimum and are essential to working with the Engaging Networks data API.

<table style="width: 100%;" border="0" cellpadding="5">
<thead>
<tr>
<th>Option</th>
<th>Default</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>token</td>
<td></td>
<td><strong>Mandatory</strong>. Your special API token provided by e-Activist. Enables access to the e-Activist data API.</td>
</tr>
<tr>
<td>campaignId</td>
<td></td>
<td><strong>Mandatory.</strong> A single campaign ID or list of campaign IDs for which data should  be retrieved (and aggregated, if relevant). The campaign ID can be  found in the URL for each campaign e.g  <a href="http://e-activist.com/ea-action/action?ea.client.id=xx&amp;ea.campaign.id=">http://e-activist.com/ea-action/action?ea.client.id=xx&amp;ea.campaign.id=</a><strong>xxxxx</strong></td>
</tr>
</table>



## Recent supporter List

### Options

<table style="width: 100%;" border="0" cellpadding="5">
<thead>
<tr>
<th>Option</th>
<th>Default</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>count</td>
<td>5</td>
<td>The number of recent supporters you want listed. Supporters will be listed most recent first.</td>
</tr>
<tr>
<td>format</td>
<td>{forename} from {town}, {datetime} {ago}</td>
<td>
<p>The exact formatting of the output of each row of information. This can include HTML. The {placeholders} are used to retrieve specific fields from e-Activist's API.</p>
<p>One placeholder not related to e-Activist's fields is <span class="geshifilter"><code class="text geshifilter-text">{ago}</code></span>. This is used to output the data of the action in relative time format e.g "2 mins ago". The "2 mins " comes from the <span class="geshifilter"><code class="text geshifilter-text">{datetime}</code></span> but depending on the language of your page <span class="geshifilter"><code class="text geshifilter-text">{ago}</code></span> may have to come before or after "2 mins " so is provided as a separate placeholder to the <span class="geshifilter"><code class="text geshifilter-text">{datetime}</code></span>.</p>
</td>
</tr>
<tr>
<td>agoFormat</td>
<td>datetime</td>
<td>The name of the field containing the date to be formatted into the relative “2 mins ago” time. For almost all situations this does not need to be changed.</td>
</tr>
<tr>
<td>agoText</td>
<td>ago</td>
<td>The literal word "ago" or its translation into another language, used to generate the relative time phrase "2 mins ago"</td>
</tr>
<tr>
<td>agoFormatLabelsSingular</td>
<td>['year', 'month', 'week', 'day', 'hour', 'minute', 'second']</td>
<td>An array of labels for each of the key time periods used to output the relative time format. Singular versions of the nouns only.</td>
</tr>
<tr>
<td>agoFormatLabelsPlural</td>
<td>['years', 'months', 'weeks', 'days', 'hours', 'minutes', 'seconds']</td>
<td>An array of labels for each of the key time periods used to output the relative time format. Plural versions of the nouns only.</td>
</tr>
<tr>
<td>dataUrl</td>
<td>&nbsp;</td>
<td>By default the plugin will pull data directly from e-Activist's API URL,  but you may wish to have it pull from an alternate URL. The format of  the data is expect to be exactly the same as e-Activist's output.</td>
</tr>
</tbody>
</table>

### Usage example

```html
<script src="jquery.eactivist-supporterlist.js"></script>
<script>
  $(function(){
		$('.supporterlist').eActivistSupporterlist({
			token: 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx',
			campaignId: 'xxxxx,xxxxx,xxxxx',
			format: '<span class="name">{vorname}</span> de {land} <span class="time">{ago} {datetime}</span>',
			agoText: 'Hace',
			agoFormatLabelsSingular: ['ano', 'mes', 'semanas', 'dia', 'hora', 'minutos', 'segundo'],
			agoFormatLabelsPlural: ['ano', 'mes', 'semanas', 'dia', 'hora', 'minutos', 'segundo'],
			count:5
		})
	});
</script>
<div class="supporterlist">
	<h3>People taking action</h3>
</div>
```

In the somewhat implausible example above, the relative time format has been configured for Spanish (note `{ago}` goes before the `{datetime}`) but the fields being pulled from the data API are `{vorname}` and `{land}` and evidently coming from a German database.
It would output something like

```html
<div class="supporterlist">
  <h3>People taking action</h3>
	<ul>
		<li><span class="name">David</span> de England <span class="time">Hace 2 minutos</span></li>
		<li><span class="name">Luke</span> de Tatooine <span class="time">Hace 10 minutos</span></li>
		<li><span class="name">Darth</span> de Tatooine <span class="time">Hace 1 hora</span></li>
		<li><span class="name">Leia</span> de Alderaan <span class="time">Hace 5 hora</span></li>
		<li><span class="name">Han</span> de Corellia <span class="time">Hace 1 dia</span></li>
	</ul>
</div>
```


## Thermometer

### Options

<table style="width: 100%;" border="0" cellpadding="5">
<thead>
<tr>
<th>Option</th>
<th>Default</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>target</td>
<td>0</td>
<td>Engaging Networks have no knowledge of your campaign targets so to create a thermometer plotting progress towards that target requires you to manually provide the target number, using this option. If you have a campaign where your target number is 40,000, you’d specify <code class="inline-code">target: 40000 </code>(without commas to denote thousands).</td>
</tr>
<tr>
<td>initialValue</td>
<td>0</td>
<td>You may wish the thermometer's level to include data from outside the e-Activist system. <code class="inline-code">initialValue</code> allows you to specify a number which will be added to the count that comes from the e-Activist data API, prior to plotting the thermometer progress. If for example you have received 200 supporters via a street campaign, and 1000 supporters via e-Activist, you would specify <code class="inline-code">initialValue: 200</code>. A total of 1200 would display on the<br />thermometer.</td>
</tr>
<tr>
<td>duration</td>
<td>2000</td>
<td>The duration of the animation which increases the thermometer's level to the point representing progress so far. If set to 0 no animation will occur.</td>
</tr>
<tr>
<td>dataUrl</td>
<td>&nbsp;</td>
<td>By default the plugin will pull data directly from e-Activist's API URL, but you may wish to have it pull from an alternate URL. The format of the data is expected to be exactly the same as e-Activist's output.</td>
</tr>
<tr>
<td>service</td>
<td>EaEmailAOTarget</td>
<td>Accepts 'EaEmailAOTarget' or 'NetDonor'. <strong>'EaEmailAOTarget'</strong> is for use with e-activist campaigns. <strong>'NetDonor'</strong> is for use with NetDonor fundraising campaigns.</td>
</tr>
<tr>
<td>currencySymbol</td>
<td><em>empty string</em></td>
<td>Only relevant for NetDonor fundraising campaigns. Prepends a character to the numeric values output by the plugin (t_target and t_current). &amp;#163; is the HTML code for &#163;. </td>
</tr>
</tbody>
</table>

### CSS

The contents of the element you choose with your jQuery selector should include the following classes. The types of elements you add these classes to is up to you, but obviously the markup must be conducive to the general concept of a thermometer which has a body and a "level" within that body.

<table style="width: 100%;" border="0" cellpadding="5">
<thead>
<tr>
<th>Class</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>t_body</td>
<td><strong>Mandatory</strong>. This element must wrap one with t_level applied. t_body is the main body of the thermometer - the part which "fills" with the progress bar.</td>
</tr>
<tr>
<td>t_level</td>
<td><strong>Mandatory.</strong> The themometer's "level" indicator. An element which is expanded/contracted to indicate the progress of the campaign towards its target.</td>
</tr>
<tr>
<td>t_current</td>
<td>Any element with t_current applied to it will be populated with the value of the total current number of actions on the campaign (or totalled across multiple campaign IDs, if specified).</td>
</tr>
<tr>
<td>t_target</td>
<td>Any element with t_target will be populated with the value entered in the <code class="inline-code">target</code> plugin option. Useful for generating messages like "X people have signed up, help us get to Y".</td>
</tr>
</tbody>
</table>

### Usage example

```html
<script src="jquery.eactivist-thermometer.js"></script>
<script>
  $(function(){ 
		$('.thermometer').eActivistThermometer({
			token:'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx', 
			campaignId:xxxxx, 
			target:50000
		});
	});
</script>
<div class="thermometer">
	<div class="t_body">
		<div class="t_level"></div><span class="t_current"></span>
	</div>
	<span class="t_current"></span>have signed up. Help us get to <span class="t_target"></span>
</div>
```




## Rollcall

### Options

<table style="width: 100%;" border="0" cellpadding="5">
<thead>
<tr>
<th>Option</th>
<th>Default</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<td>dataUrl</td>
<td>&nbsp;</td>
<td>By default the plugin will pull data directly from e-Activist's API URL, but you may wish to have it pull from an alternate URL. The format of the data is expected to be exactly the same as e-Activist's output.</td>
</tr>
<tr>
<td>format</td>
<td>{firstName} from {country}{city} gave {currency}{amount}</td>
<td>
<p>The exact formatting of the output of each row of information. This can include HTML. The {placeholders} are used to retrieve specific fields from e-Activist's API.</p>
</td>
</tr>
<tr>
<td>dataSet</td>
<td>1</td>
<td>
<p>This is an option from the Engaging Networks API. dataSet=1 returns first name and <strong>country</strong>. dataSet=2 returns first name and <strong>city</strong></p>
</td>
</tr>
<tr>
<td>count</td>
<td>5</td>
<td>
<p>The number of results you want to see.</p>
</td>
</tr>
<tr>
<td>service</td>
<td>RollCall</td>
<td>
<p>Accepts 'RollCall' or 'FundraisingRollCall'. <strong>RollCall</strong> is for use with an e-activist campaign. <strong>FundraisingRollCall</strong> is for use with a NetDonor campaign.</p>
</td>
</tr>
<tr>
<td>titleCaseFields</td>
<td>['firstname', 'city', 'country']</td>
<td>
<p>Preformats the specified fields into Title Case (data from API isn't sanitised). Enter the <strong>lower-case</strong> titles of the API fields you would like to format. 'ford from GUILDford' would become 'Ford from Guildford'. Could also be done manually with CSS text-transform:capitalize.</p>
</td>
</tr>
<tr>
<td>currencySymbolReplacements</td>
<td>{ 'GBP':'&#163;', 'EUR': '&#8364;'}</td>
<td>
<p>Only required for FundraisingRollCall. Converts the currency data as stored in the database (e.g. GBP) into an HTML encoded character for display on the page.</p>
</td>
</tr>
</tbody>
</table>


### Usage example

```html
<script src="jquery.eactivist-rollcall.js" type="text/javascript"></script>
  <script type="text/javascript">
  // <![CDATA[
  $(function(){          
        $('#fundraising_rollcall').eActivistRollcall({
            token:'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx',
            campaignId:'xxxxx,xxxxx,xxxxx',
            count:3,
            dataSet:2,
            format:'<span class="name">{firstName}<\/span> from {country}{city} gave {currency}{amount} ',
            service: 'FundraisingRollCall'              
        })
  });  
  // ]]>
</script>

<div id="fundraising_rollcall">
<h3>Latest donations</h3>
</div>
```