!SLIDE center subsection blue

# Approches to DPKs

!SLIDE bullets incremental transition=fade

# Approches

1. DPK tools, Manual domain
1. DPK tools and domains, Manual config
1. DPK and Custom modules
1. Customized DPK

!SLIDE bullets incremental transition=fade

# Managing Custom DPK

1. Push files from network share
1. Symlink to dpkfiles in git repo
1. Manual git repo
1. Puppet server

!SLIDE bullets incremental transition=fade

# Makefile for dpkfiles

1. Similar approach to dotfiles
1. Create a git repo containing all custom dpkfiles
1. Include a `make` file, which creates symlinks
1. Example: `make link TYPE=prd_portal`

!SLIDE bullets

# Makefile for dpkfiles

    @@@ make
    $PUPPET_CONFIG_DIR/
        data/
            psft_customization.yaml -> $DPKFILES_DIR/data/prd_portal.psft_customization.yaml
        manifests/
            site.pp -> $DPKFILES_DIR/manifests/prd_portal.site.pp
        modules/
            io_roles -> $DPKFILES_DIR/modules/io_roles
            io_profiles -> $DPKFILES_DIR/modules/io_profiles
            io_config -> $DPKFILES_DIR/modules/io_config
