!SLIDE center subsection blue

# User Preferences

!SLIDE bullets

# User Preferences

* My Preferences are cluster-aware
* Always shows the gateway system’s My Preferences component
* General Settings preferences are synchronized 
* Displays preference items from all systems in cluster

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# New Framework

* Delivered by Applications
* Custom Personalizations
    * Add to General Settings  
    * Create other custom preference item categories
        * Creating Fluid components 
        * Define content references in the My Preferences folder
    * Order controlled by SEQNBR on CREF

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# Service Operation

* Sync Message
    * PTUN_USER_PREFERENCES - Unified User Preferences
        * Handler: PTGP_GUIDED_PROCESS:IBHandlers:UnifiedUserPreferenceHandler
	* Fires at My Pref page load and save
	* Appears to look at node network, regardless of Active Routing

!SLIDE bullets

# References

* Clustering
    * https://docs.oracle.com/cd/E99483_01/pt857pbr1/eng/pt/tsec/concept_UnderstandingTheMyPreferencesUserInterface.html#ufc5aa618-62bd-4b78-afba-68cce300a9ef
* Dev Custom My Pref Personalization Items
    * https://goo.gl/j6w3Lc

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE center subsection grey

# Demo

![Demo](../_images/pref.jpg)

!SLIDE supplemental guide

# User Preferences Demo

* User Pref page - FN and HR content
    * Payroll and GL
* General updates sync gateway to others - test time change
* Service PTUN_USER_PREFERENCES
