!SLIDE center subsection blue

# psadmin-plus

!SLIDE bullets

# psadmin-plus

* psadmin-plus, or  `psa`, is a psadmin helper script
* Great for completing multiple tasks in one command
* [github.com/psadmin-io/psadmin-plus](https://github.com/psadmin-io/psadmin-plus)

!SLIDE bullets

# psa help

    @@@console
    $ psa help
    Usage: psa [command] <type> <domain>

    Commands:
        help           display this help message
        list           list domains
        summary        PS_CFG_HOME summary, no type or domain needed
        status         status of the domain
        start          pooladd, if enabled, then start the domain
        stop           poolrm, if enabled, stop the domain
        ...
    Types:
        app            act on application domains
        prcs           act on process scheduler domains
        web            act on web domains
        all,<blank>    act on all types of domains
    Domains:
        dom            act on specific domains
        all,<blank>    act on all domains

!SLIDE bullets

# psa examples

* `psa help`           - help menu
* `psa start`          - start all domains on server
* `psa start web`      - start all web domains on server
* `psa start web hdev` - start hdev web domain on server
* `psa bounce`         - stop, cache, IPC, configure, start all domains

!SLIDE bullets

# psa versions

* ruby - Linux, Windows
* old branches
    * bash
    * powershell
    * old multiple domain support

!SLIDE bullets

# psa install

* Install Ruby, RubyGems...or use Puppet's
    * `export PATH=/opt/puppetlabs/puppet/bin:$PATH`
    * `$env:PATH += ";C:\Program Files\Puppet Labs\Puppet\sys\ruby\bin"`
* `gem install psadmin_plus`

*NOTE: For Windows, you will need to [update the RubyGemsRootCA.pem](https://gist.github.com/iversond/772e73257c4ca59a9e6137baa7288788), since the DPK ships an outdated version.*

!SLIDE center subsection grey

# Demo
