---
layout: post
title: ! 'JS: select all checkbox and submit form via js'
categories:
- Tech Notes
tags:
- checkbox
- form
- js
- tips
published: true
comments: true
---
<p><strong>TIPS:</strong></p>

<p><code lang="js">
<script type="text/javascript">
  function SetAllCheckBoxes(FormName, FieldName, CheckValue)<br>
  {<br>
    if(!document.forms[FormName])<br>
      return;<br>
    var objCheckBoxes = document.forms[FormName].elements[FieldName];<br>
    if(!objCheckBoxes)<br>
      return;<br>
    var countCheckBoxes = objCheckBoxes.length;<br>
    if(!countCheckBoxes)<br>
      objCheckBoxes.checked = CheckValue;<br>
    else<br>
    // set the check value for all check boxes<br>
      for(var i = 0; i < countCheckBoxes; i++)<br>
        objCheckBoxes[i].checked = CheckValue;<br>
  }</p>

<p>  function SendForm(FormName, ActionName)<br>
  {<br>
    if(!document.forms[FormName])<br>
      return;<br>
    if(ActionName == 'unread')<br>
      document.forms[FormName].action = '<%= batch_update_notifications_path(:type => "unread") %>';<br>
    if(ActionName == 'remove')<br>
      document.forms[FormName].action = '<%= batch_update_notifications_path(:type => "remove") %>';<br>
    document.forms[FormName].submit();<br>
  }
</script>
</code></p>
