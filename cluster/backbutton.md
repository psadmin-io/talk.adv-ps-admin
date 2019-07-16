!SLIDE center subsection blue

# Back Button

!SLIDE bullets

# Back Button

* TODO: image of back button

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# Tips and Tricks

* Multi Tools version
    * 8.54.21? and up?
* Component settings
* Nav Collections TODO

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# How it works

* JavaScript
    * PT_COMMON > PT_HISTORY
* TODO - call out details
    * backNavigation.classicBackButton.create();
    * var pt_history = getHistoryObject();

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE center subsection grey

# Demo

!SLIDE supplemental guide

# JavaScript Location

* PT_COMMON > PT_HISTORY

# Create the back button HTML

* backNavigation.classicBackButton.create();

# Add to History

* AddToHistory(label, keyData, userData, pageName, stateNum, elemNum, classicURL, dashboard, appBcData, nPost, userQueryString, bReturnToLastPage) 
* AddToHistory("Testing", "", "", "", 0, 0, "http://google.com", 0, "","","",true);

# Examples

* var pt_history = getHistoryObject();
* pt_history.pop();
* pt_history.save();
* getHistoryObject().nodes
