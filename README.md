# Social proof plugins

## Recent Supporter List

## Options

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

### Example

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
<td>token</td>
<td></td>
<td><strong>Mandatory</strong>. Your special API token provided by e-Activist. Enables access to the e-Activist data API.</td>
</tr>
<tr>
<td>campaignId</td>
<td></td>
<td><strong>Mandatory.</strong> A single campaign ID or list of campaign IDs for which data should be retrieved (and aggregated, if relevant). The campaign ID can be found in the URL for each campaign e.g <a href="http://e-activist.com/ea-action/action?ea.client.id=xx&amp;ea.campaign.id=">http://e-activist.com/ea-action/action?ea.client.id=xx&amp;ea.campaign.id=</a><strong>xxxxx</strong></td>
</tr>
<tr>
<td>target</td>
<td>0</td>
<td>e-Activist’s does not request to know your target number of supporters. To create a thermometer plotting progress therefore requires you to manually specify this target number, using this option. If you have a campaign where your target number is 40,000, you’d specify <code class="inline-code">target: 40000 </code>(without commas to donate thousands).</td>
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
<td>By default the plugin will pull data directly from e-Activist's API URL, but you may wish to have it pull from an alternate URL. The format of the data is expect to be exactly the same as e-Activist's output.</td>
</tr>
</tbody>
</table>

### Markup

The contents of the element you choose with your jQuery selector should include the following classes. The types of elements you add these classes to is up to you, but obviously the markup must be conducive to the general concept of a thermometer which has a body and a "level" within that body.

<table style="width: 100%;" border="0" cellpadding="5">
<thead>
<tr>
<th>CLASS</th>
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

### Example

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