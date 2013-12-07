--- 
layout: post
title: "Titanium : DB Synchronization"
comments: true
categories:
- db
- iPhone
- iPhone/iPad
- sync
- Titanium
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
<strong>Header Notes:</strong>
1. Static data should be released with app, just don't do db synchronization.
2. Just embed sync background when ppl looking at some instructions/tips etc.
3. Don't update db all the time.

App Start:
<em><strong>app.js</strong></em>
<code lang='javascript'>
// Localization libs
Ti.include('l10n/l10n.js');
Ti.include('l10n/l10n_dialog.js');
Ti.include('l10n/l10n_format.js');

var db = Titanium.Database.install('eq31formulas.db', 'eq31formulas');

// Ti.include('content/tab_formula.js')

// this sets the background color of the master UIView (when there are no windows/tab groups on it)
Titanium.UI.setBackgroundColor('#000');

// create tab group
var tabGroup = Titanium.UI.createTabGroup();

//
// create tab for tips
//
Ti.include('content/tab_tips.js');

//
// create tab for weibo
//
Ti.include('content/tab_weibo.js');

//
// create tab for formulas
//
Ti.include('content/tab_formulas.js');

// create tab for lang settings
var win_setting = Ti.UI.createWindow({
    title:_('tab_settings')
});

var tab_setting = Ti.UI.createTab({  
    icon:'images/nav_icon_setting.png',
    title:_('tab_settings'),
    window:win_setting
});

var data = [];
var ACTION_LANGUAGE = 0;

var row = Ti.UI.createTableViewRow({
  title: _('language'),
  hasChild: true,
  action: ACTION_LANGUAGE,
  className: 'control'
});

var label_lang = Ti.UI.createLabel({
  textAlign: 'right',
  right: 10,
  width: 175,
  color: '#385487',
  font: {fontSize: 16},
  text: L10N.getLanguageDisplayName()
});

row.add(label_lang);

data.push(row);

// create table view

var tableview = Ti.UI.createTableView({
  data:data,
  style:Ti.UI.iPhone.TableViewStyle.GROUPED
});

// add table click listener

tableview.addEventListener('click', function(e) {
  var rowdata = e.rowData;
  if (rowdata.action == ACTION_LANGUAGE) {

    // show language selection dialog

    L10N.showLanguageSelectionDialog();
  }
});

win_setting.add(tableview);

//
//  add tabs
//
tabGroup.addTab(tab_formulas);  
tabGroup.addTab(tab_tips);  
tabGroup.addTab(tab_weibo);
tabGroup.addTab(tab_setting);  

var omodes = [
	Titanium.UI.PORTRAIT,
	Titanium.UI.UPSIDE_PORTRAIT,
	Titanium.UI.LANDSCAPE_LEFT,
	Titanium.UI.LANDSCAPE_RIGHT
];

win_formulas.orientationModes = omodes;
win_tips.orientationModes = omodes;
win_weibo.orientationModes = omodes;

Titanium.Analytics.featureEvent('app.feature.blah',{product:'killer'});

tabGroup.addEventListener('open',function()
{
	Titanium.UI.setBackgroundColor('#fff');
});

tabGroup.setActiveTab(0);
tabGroup.open({
	transition:Titanium.UI.iPhone.AnimationStyle.FLIP_FROM_LEFT
});

// add top level introduction of 31 formulas
Ti.include("introduction.js");

// synchronize db
Ti.include("synchronize.js");

</code>

Prepare data while launching the app:
<em><strong>synchronize.js</strong></em>
<code lang="javascript">
(function(){
	var db = Titanium.Database.open('eq31formulas');
	
        // JS test
	var currentTime = new Date();
	var month = currentTime.getMonth() + 1;
	var day = currentTime.getDate();
	var year = currentTime.getFullYear();
	
	Titanium.API.info('JS TIME:' + currentTime);
	// lesson = db.execute('SELECT * FROM LESSONS ORDER BY ID LIMIT 1')
	
	if (Titanium.Network.online == true)
	{
		Titanium.API.info('Online--update lessons!');
		var src = 'http://www.veecue.com/eq31formulas/data_service/lessons';
		c = Titanium.Network.createHTTPClient();

		c.onload = function()
		{	
			var json_data = JSON.parse(this.responseText);
			
			Titanium.API.info('lesson count:' + json_data.length);
			
			for(var i=0; i<json_data.length; i++)
			{
				Titanium.API.info("updating lesson:" + i);
				var record = json_data[i].lesson;
				// add different control for UPDATE or INSERTION here
				db.execute('CREATE TABLE IF NOT EXISTS LESSONS (ID INTEGER, TITLE TEXT, AIMS TEXT, ANSWER_ORDER TEXT, LANG_STEP TEXT, MODEL_ANSWER TEXT)');
				db.execute('DELETE FROM LESSONS');
				db.execute("INSERT INTO LESSONS (ID, TITLE, AIMS, ANSWER_ORDER, LANG_STEP, MODEL_ANSWER) VALUES(?,?,?,?,?,?)", record.id, record.title, record.aims, record.answer_order, record.lang_step, record.model_answer);	
			}
		};
 
		// open the client
		c.open('GET', src);
		
		// send the data
		c.send();
	}
	else
	{
		Titanium.API.info('Offline--');
		return;
	}  	
})();
</code>
