!SLIDE center subsection blue

# Back Button

!SLIDE bullets incremental

# Back Button

* Button that takes you back
* Works in mysterious ways

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# Tips and Tricks

* Multi Tools version
* Component settings
* Nav Collections 

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# How it works

* JavaScript
    * PT_COMMON > PT_HISTORY
    * var pt_history = getHistoryObject();

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE center subsection grey

# Demo

![Demo](../_images/exam.jpg)

!SLIDE supplemental guide

# Back Button Demo

## JavaScript Location

1. PT_COMMON > PT_HISTORY

## Create the back button HTML

1. backNavigation.classicBackButton.create();

## Add to History

1. AddToHistory(label, keyData, userData, pageName, stateNum, elemNum, classicURL, dashboard, appBcData, nPost, userQueryString, bReturnToLastPage) 
1. AddToHistory("Testing", "", "", "", 0, 0, "http://google.com", 0, "","","",true);

## Examples

1. var pt_history = getHistoryObject();
1. pt_history.nodes();
1. Populate stack
    1. Service Ops, Service Config
1. _AddToHistory("psadmin.io 1", "", "", "", 0, 0, "https://psadmin.io", 1, "","","",true);
1. _AddToHistory("psadmin.io 2", "", "", "", 0, 0, "https://psadmin.io", 1, "","","",true);
1. var pt_history = getHistoryObject();
1. pt_history.nodes();
1. Try back button 
