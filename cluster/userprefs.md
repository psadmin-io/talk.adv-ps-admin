!SLIDE center subsection blue

# User Preferences

!SLIDE bullets

# User Preferences

* TODO

~~~SECTION:notes~~~

158 - Federated User Preferences

~~~ENDSECTION~~~

!SLIDE bullets

# New Framework

* TODO

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# Custom Preferences

* TODO

~~~SECTION:notes~~~

~~~ENDSECTION~~~

# Federated User Preferences

* TODO

~~~SECTION:notes~~~

Federated User Preferences @ 20:00
	• PeopleBooks
	• Clustering
		○ https://docs.oracle.com/cd/E99483_01/pt857pbr1/eng/pt/tsec/concept_UnderstandingTheMyPreferencesUserInterface.html#ufc5aa618-62bd-4b78-afba-68cce300a9ef
		○ The My Preferences link is cluster-aware. As a result, when you click the link it always shows the gateway system’s My Preferences component.
		○ Changes made to the General Settings preferences are synchronized to all systems in the same cluster automatically.
		○ The My Preferences page displays preference items from all systems in the same cluster and allows users to change settings in those systems from within the same My Preferences page.
	• Dev Custom My Pref Personalization Items
		○ https://goo.gl/j6w3Lc
	• Sync Message
		○ PTUN_USER_PREFERENCES - Unified User Preferences
		○ Fires at My Pref page load and save
		○ Appears to look at node network, regardless of Active Routing
			▪ I saw Errors going back to 8.54 Nodes I didn't know were in network
	• Questions
		○ How do we handle PT mixed cluster?
		○ Are all apps using this new framework? 
		○ What are some good use cases for custom items?
			▪ Branding options?
			▪ Enable/Disable breadcrumbs 🙂

Custom My Preferences @ 35:00

~~~ENDSECTION~~~

!SLIDE center subsection grey

# Demo

~~~SECTION:notes~~~

https://docs.oracle.com/cd/E92519_01/pt856pbr2/eng/pt/tsec/concept_UnderstandingTheMyPreferencesUserInterface.html

My Preferences in Clustered Environments, Press Enter to collapse

Service Operation: PTUN_USER_PREFERENCES

Handler: PTGP_GUIDED_PROCESS:IBHandlers:UnifiedUserPreferenceHandler.OnRequest

~~~ENDSECTION~~~