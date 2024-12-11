---
layout: default
built_from_commit: a0909f4eae7490d52cb1e7dc81010592ba607679
title: 'Man Page: puppet module'
canonical: "/puppet/latest/man/module.html"
---

# Man Page: puppet module

> **NOTE:** This page was generated from the Puppet source code on 2024-11-04 23:37:39 +0000

## NAME
**puppet-module** - Creates, installs and searches for modules on the
Puppet Forge.

## SYNOPSIS
puppet module *action* \[\--environment production \] \[\--modulepath \]

## DESCRIPTION
This subcommand can find, install, and manage modules from the Puppet
Forge, a repository of user-contributed Puppet code. It can also
generate empty modules, and prepare locally developed modules for
release on the Forge.

## OPTIONS
Note that any setting that\'s valid in the configuration file is also a
valid long argument, although it may or may not be relevant to the
present action. For example, **server** and **run_mode** are valid
settings, so you can specify **\--server \<servername\>**, or
**\--run_mode \<runmode\>** as an argument.

See the configuration file documentation at
*https://puppet.com/docs/puppet/latest/configuration.html* for the full
list of acceptable parameters. A commented list of all configuration
options can also be generated by running puppet with **\--genconfig**.

\--render-as FORMAT

:   The format in which to render output. The most common formats are
    **json**, **s** (string), **yaml**, and **console**, but other
    options such as **dot** are sometimes available.

\--verbose

:   Whether to log verbosely.

\--debug

:   Whether to log debug information.

\--environment production

:   The environment in which Puppet is running. For clients, such as
    **puppet agent**, this determines the environment itself, which
    Puppet uses to find modules and much more. For servers, such as
    **puppet server**, this provides the default environment for nodes
    that Puppet knows nothing about.

    When defining an environment in the **\[agent\]** section, this
    refers to the environment that the agent requests from the primary
    server. The environment doesn\'t have to exist on the local
    filesystem because the agent fetches it from the primary server.
    This definition is used when running **puppet agent**.

    When defined in the **\[user\]** section, the environment refers to
    the path that Puppet uses to search for code and modules related to
    its execution. This requires the environment to exist locally on the
    filesystem where puppet is being executed. Puppet subcommands,
    including **puppet module** and **puppet apply**, use this
    definition.

    Given that the context and effects vary depending on the config
    section
    *https://puppet.com/docs/puppet/latest/config_file_main.html##config-sections*    in which the **environment** setting is defined, do not set it
    globally.

\--modulepath

:   The search path for modules, as a list of directories separated by
    the system path separator character. (The POSIX path separator is
    \':\', and the Windows path separator is \';\'.)

    Setting a global value for **modulepath** in puppet.conf is not
    allowed (but it can be overridden from the commandline). Please use
    directory environments instead. If you need to use something other
    than the default modulepath of **\<ACTIVE ENVIRONMENT\'S MODULES
    DIR\>:\$basemodulepath**, you can set **modulepath** in
    environment.conf. For more info, see
    *https://puppet.com/docs/puppet/latest/environments_about.html*

## ACTIONS
**changes** - Show modified files of an installed module.

:   **SYNOPSIS**

    puppet module changes *path*

    **DESCRIPTION**

    Shows any files in a module that have been modified since it was
    installed. This action compares the files on disk to the md5
    checksums included in the module\'s checksums.json or, if that is
    missing, in metadata.json.

    **RETURNS**

    Array of strings representing paths of modified files.

**install** - Install a module from the Puppet Forge or a release archive.

:   **SYNOPSIS**

    puppet module install \[\--force \| -f\] \[\--target-dir DIR \| -i
    DIR\] \[\--ignore-dependencies\] \[\--version VER \| -v VER\] *name*

    **DESCRIPTION**

    Installs a module from the Puppet Forge or from a release archive
    file. Note: Module install uses MD5 checksums, which are prohibited
    on FIPS enabled systems.

    The specified module will be installed into the directory specified
    with the **\--target-dir** option, which defaults to the first
    directory in the modulepath.

    **OPTIONS** *\--force* \| *-f* - Force overwrite of existing module,
    if any. Implies \--ignore-dependencies.

    *\--ignore-dependencies* - Do not attempt to install dependencies.
    Implied by \--force.

    *\--target-dir DIR* \| *-i DIR* - The directory into which modules
    are installed; defaults to the first directory in the modulepath.

    Specifying this option will change the installation directory, and
    will use the existing modulepath when checking for dependencies. If
    you wish to check a different set of directories for dependencies,
    you must also use the **\--environment** or **\--modulepath**
    options.

    *\--version VER* \| *-v VER* - Module version to install; can be an
    exact version or a requirement string, eg \'\>= 1.0.3\'. Defaults to
    latest version.

    **RETURNS**

    Pathname object representing the path to the installed module.

**list** - List installed modules

:   **SYNOPSIS**

    puppet module list \[\--tree\]

    **DESCRIPTION**

    Lists the installed puppet modules. By default, this action scans
    the modulepath from puppet.conf\'s **\[main\]** block; use the
    \--modulepath option to change which directories are scanned.

    The output of this action includes information from the module\'s
    metadata, including version numbers and unmet module dependencies.

    **OPTIONS** *\--tree* - Whether to show dependencies as a tree view

    **RETURNS**

    hash of paths to module objects

**uninstall** - Uninstall a puppet module.

:   **SYNOPSIS**

    puppet module uninstall \[\--force \| -f\] \[\--ignore-changes \|
    -c\] \[\--version=\] *name*

    **DESCRIPTION**

    Uninstalls a puppet module from the modulepath (or a specific target
    directory). Note: Module uninstall uses MD5 checksums, which are
    prohibited on FIPS enabled systems.

    **OPTIONS** *\--force* \| *-f* - Force the uninstall of an installed
    module even if there are local changes or the possibility of causing
    broken dependencies.

    *\--ignore-changes* \| *-c* - Uninstall an installed module even if
    there are local changes to it. (Implied by \--force.)

    *\--version=* - The version of the module to uninstall. When using
    this option, a module matching the specified version must be
    installed or else an error is raised.

    **RETURNS**

    Hash of module objects representing uninstalled modules and related
    errors.

**upgrade** - Upgrade a puppet module.

:   **SYNOPSIS**

    puppet module upgrade \[\--force \| -f\] \[\--ignore-dependencies\]
    \[\--ignore-changes \| -c\] \[\--version=\] *name*

    **DESCRIPTION**

    Upgrades a puppet module. Note: Module upgrade uses MD5 checksums,
    which are prohibited on FIPS enabled systems.

    **OPTIONS** *\--force* \| *-f* - Force the upgrade of an installed
    module even if there are local changes or the possibility of causing
    broken dependencies. Implies \--ignore-dependencies.

    *\--ignore-changes* \| *-c* - Upgrade an installed module even if
    there are local changes to it. (Implied by \--force.)

    *\--ignore-dependencies* - Do not attempt to install dependencies.
    Implied by \--force.

    *\--version=* - The version of the module to upgrade to.

    **RETURNS**

    Hash

## EXAMPLES
**changes**

Show modified files of an installed module:

\$ puppet module changes /etc/puppetlabs/code/modules/vcsrepo/ warning:
1 files modified lib/puppet/provider/vcsrepo.rb

**install**

Install a module:

\$ puppet module install puppetlabs-vcsrepo Preparing to install into
/etc/puppetlabs/code/modules \... Downloading from
https://forgeapi.puppet.com \... Installing \-- do not interrupt \...
/etc/puppetlabs/code/modules └── puppetlabs-vcsrepo (v0.0.4)

Install a module to a specific environment:

\$ puppet module install puppetlabs-vcsrepo \--environment development
Preparing to install into
/etc/puppetlabs/code/environments/development/modules \... Downloading
from https://forgeapi.puppet.com \... Installing \-- do not interrupt
\... /etc/puppetlabs/code/environments/development/modules └──
puppetlabs-vcsrepo (v0.0.4)

Install a specific module version:

\$ puppet module install puppetlabs-vcsrepo -v 0.0.4 Preparing to
install into /etc/puppetlabs/modules \... Downloading from
https://forgeapi.puppet.com \... Installing \-- do not interrupt \...
/etc/puppetlabs/code/modules └── puppetlabs-vcsrepo (v0.0.4)

Install a module into a specific directory:

\$ puppet module install puppetlabs-vcsrepo
\--target-dir=/opt/puppetlabs/puppet/modules Preparing to install into
/opt/puppetlabs/puppet/modules \... Downloading from
https://forgeapi.puppet.com \... Installing \-- do not interrupt \...
/opt/puppetlabs/puppet/modules └── puppetlabs-vcsrepo (v0.0.4)

Install a module into a specific directory and check for dependencies in
other directories:

\$ puppet module install puppetlabs-vcsrepo
\--target-dir=/opt/puppetlabs/puppet/modules \--modulepath
/etc/puppetlabs/code/modules Preparing to install into
/opt/puppetlabs/puppet/modules \... Downloading from
https://forgeapi.puppet.com \... Installing \-- do not interrupt \...
/opt/puppetlabs/puppet/modules └── puppetlabs-vcsrepo (v0.0.4)

Install a module from a release archive:

\$ puppet module install puppetlabs-vcsrepo-0.0.4.tar.gz Preparing to
install into /etc/puppetlabs/code/modules \... Downloading from
https://forgeapi.puppet.com \... Installing \-- do not interrupt \...
/etc/puppetlabs/code/modules └── puppetlabs-vcsrepo (v0.0.4)

Install a module from a release archive and ignore dependencies:

\$ puppet module install puppetlabs-vcsrepo-0.0.4.tar.gz
\--ignore-dependencies Preparing to install into
/etc/puppetlabs/code/modules \... Installing \-- do not interrupt \...
/etc/puppetlabs/code/modules └── puppetlabs-vcsrepo (v0.0.4)

**list**

List installed modules:

\$ puppet module list /etc/puppetlabs/code/modules ├──
bodepd-create_resources (v0.0.1) ├── puppetlabs-bacula (v0.0.2) ├──
puppetlabs-mysql (v0.0.1) ├── puppetlabs-sqlite (v0.0.1) └──
puppetlabs-stdlib (v2.2.1) /opt/puppetlabs/puppet/modules (no modules
installed)

List installed modules in a tree view:

\$ puppet module list \--tree /etc/puppetlabs/code/modules └─┬
puppetlabs-bacula (v0.0.2) ├── puppetlabs-stdlib (v2.2.1) ├─┬
puppetlabs-mysql (v0.0.1) │ └── bodepd-create_resources (v0.0.1) └──
puppetlabs-sqlite (v0.0.1) /opt/puppetlabs/puppet/modules (no modules
installed)

List installed modules from a specified environment:

\$ puppet module list \--environment production
/etc/puppetlabs/code/modules ├── bodepd-create_resources (v0.0.1) ├──
puppetlabs-bacula (v0.0.2) ├── puppetlabs-mysql (v0.0.1) ├──
puppetlabs-sqlite (v0.0.1) └── puppetlabs-stdlib (v2.2.1)
/opt/puppetlabs/puppet/modules (no modules installed)

List installed modules from a specified modulepath:

\$ puppet module list \--modulepath /opt/puppetlabs/puppet/modules
/opt/puppetlabs/puppet/modules (no modules installed)

**uninstall**

Uninstall a module:

\$ puppet module uninstall puppetlabs-ssh Removed
/etc/puppetlabs/code/modules/ssh (v1.0.0)

Uninstall a module from a specific directory:

\$ puppet module uninstall puppetlabs-ssh \--modulepath
/opt/puppetlabs/puppet/modules Removed
/opt/puppetlabs/puppet/modules/ssh (v1.0.0)

Uninstall a module from a specific environment:

\$ puppet module uninstall puppetlabs-ssh \--environment development
Removed /etc/puppetlabs/code/environments/development/modules/ssh
(v1.0.0)

Uninstall a specific version of a module:

\$ puppet module uninstall puppetlabs-ssh \--version 2.0.0 Removed
/etc/puppetlabs/code/modules/ssh (v2.0.0)

**upgrade**

upgrade an installed module to the latest version

\$ puppet module upgrade puppetlabs-apache
/etc/puppetlabs/puppet/modules └── puppetlabs-apache (v1.0.0 -\> v2.4.0)

upgrade an installed module to a specific version

\$ puppet module upgrade puppetlabs-apache \--version 2.1.0
/etc/puppetlabs/puppet/modules └── puppetlabs-apache (v1.0.0 -\> v2.1.0)

upgrade an installed module for a specific environment

\$ puppet module upgrade puppetlabs-apache \--environment test
/etc/puppetlabs/code/environments/test/modules └── puppetlabs-apache
(v1.0.0 -\> v2.4.0)

## COPYRIGHT AND LICENSE
Copyright 2012 by Puppet Inc. Apache 2 license; see COPYING