!SLIDE center subsection blue

# Custom DPK Modules

!SLIDE bullets incremental transition=fade

# Custom DPK Modules

1. Fill in DPK gaps
1. Started by Eric Bolinger (CU)
1. Make it your system, not a Demo environment
1. Open Source - https://github.com/psadmin-io
1. Windows and Linux support

!SLIDE bullets

# io_weblogic

WebLogic Domain Configuration

1. Certificates
1. Java Options
1. `pskey`
1. JCE

!SLIDE bullets

# io_portwar

Website Configuration

1. `configuration.properties`
1. Cookie Name
1. Index Redirect
1. `text.properties`
1. Custom Signon

!SLIDE bullets incremental transition=fade

# Install Modules

1. `git clone https://github.com/psadmin-io/psadminio-io_portalwar`
1. `puppet module install psadminio_io_portal` (future)
1. Enable Data Bindings

        @@@ yaml
        puppet.conf
        # data_binding_terminus=none

!SLIDE center subsection blue

# Demo

~~~SECTION:notes~~~

Show off current state:

1. Show WL default page at root of web server
1. Open `text.properties`
1. Open `webLogic.xml` (cookie name)

Clone and update `psft_customizations.yaml`

1. `cd C:\psft\dpk\puppet\production\modules`
1. `git clone https://github.com/psadmin-io/psadminio-io_portalwar.git io_portalwar`
1. `puppet module install puppetlabs-inifile --confdir=c:\psft\dpk\puppet`
1. Enable Data Bindings
1. Update `psft_customizations.yaml`
 
        @@@ yaml
        # ############
        # io_portalwar
        # ############

        io_portalwar::text_properties:
          "%{hiera('pia_domain_name')}":
            '138':  'Hello UMRUG'

        io_portalwar::pia_cookie_name: "%{hiera('db_name')}-PORTAL-PSJSESSIONID"

        io_portalwar::index_redirect: true
        io_portalwar::redirect_target: "./%{hiera('pia_site_name')}/signon.html"

1. Run `puppet apply --confdir=c:\psft\dpk\puppet -d -e "contain ::io_portalwar"`
1. `get-service -name *PIA* | restart-service`

~~~ENDSECTION~~~

!SLIDE bullets

# Configure io_portalwar

    @@@ yaml
    io_portalwar::config_properties:
      "%{hiera('pia_domain_name')}":
        WebProfile: EXTERNAL

!SLIDE bullets

# Configure io_portalwar

    @@@ yaml
    io_portalwar::pia_cookie_name: "%{hiera('db_name')}-PORTAL-PSJSESSIONID"

!SLIDE bullets

# Configure io_portwar

    @@@ yaml
    io_portalwar::text_properties:
      "%{hiera('pia_domain_name')}":
        '138':  'Hello OOW17'

!SLIDE bullets

# Configure io_portalwar

    @@@ yaml
    io_portalwar::index_redirect: true
    io_portalwar::redirect_target: "./%{hiera('pia_site_name')}/signon.html"

!SLIDE bullets

# Configure io_weblogic

    @@@ yaml
    io_weblogic::java_options:
      "%{hiera('pia_domain_name')}":
        -Xms:                              '1024m'
        -Xmx:                              '1024m'
        -Dweblogic.threadpool.MinPoolSize: '=100'
        -Dhttps.protocols:                 '=TLSv1,TLSv1.1,TLSv1.2'

!SLIDE bullets

# Configure io_weblogic

    @@@ yaml
    io_weblogic::install_jce: true

!SLIDE center subsection blue

# Demo