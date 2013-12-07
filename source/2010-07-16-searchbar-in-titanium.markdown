--- 
layout: post
title: SearchBar in Titanium
comments: true
categories:
- iPhone
- iPhone/iPad
- searchbar
- tableview
- Titanium
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
In this post, I will guide you to use SearchBar in TableView when your development is based on Titanium.

<strong>Keywords</strong>: <em>Titanium, TableView, TableViewRow, SearchBar</em>

<strong>Step 1</strong>: Create a table view row datas for your content list.
<code lang="javascript">
// create the rest of the rows
var data = [];
for (var c=0;c<rowCount;c++)
{
	var row = Ti.UI.createTableViewRow();
	row.backgroundImage = '../images/row_bg.png';
	row.selectedBackgroundImage = '../images/row_bg_selected.png';
	row.height = 90;
	row.url = "formulas_show.js";
	row.id = id;
	row.className = 'datarow';
	row.filter = "the data you want to search";  // here you will set the filter content which will be searched.
	row.clickName = 'row';

	data.push(row);
}
</code>

<strong>Step 2</strong>: Create a search bar.
<code lang="javascript">
// CREATE SEARCH BAR
var search = Titanium.UI.createSearchBar({
	barColor:'#385292', 
	showCancel:false
});

search.addEventListener('change', function(e)
{
   e.value; // search string as user types
});
search.addEventListener('return', function(e)
{
   search.blur();
});
search.addEventListener('cancel', function(e)
{
   search.blur();
});
</code>

<strong>Step 3</strong>: Create a table view for your content list.
<code lang="javascript">
// create table view 
tableView = Titanium.UI.createTableView({
	data:data, // here will be the data array
	search:search, //here will set search bar
	filterAttribute:'filter', //here is the search filter which appears in TableViewRow as an attribute(you can define it in other name)
	backgroundColor:'white'
});
</code>

Ok, now you can add search bar for table view content list. as a reminder, you should add event listener for the table view object, but the click event should be bundled with the "row", so that you can search and click the search result linking to target window.
