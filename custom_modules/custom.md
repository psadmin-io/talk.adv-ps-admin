!SLIDE center subsection blue

# Custom DPK Modules

!SLIDE bullets

# Custom DPK Modules

1. Fill in DPK gaps
1. Make it your system, not a Demo environment
1. Open Source (github.com/psadmin-io)
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

!SLIDE bullets

# Install Modules

1. `git clone https://github.com/psadmin-io/psadminio-io_portalwar`
1. `puppet module install psadminio_io_weblogic` (future)

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