# About

Portage GT (short for "Portage using Gentoo") is a replacement Package Provider for Puppet. It was written by [Whatbox Inc.](http://whatbox.ca/) to improve server management, and released as on Open Source project under the MIT, BSD & GPL licenses. Patches and bug reports are welcome, please see our [CLA](http://whatbox.ca/policies/contributions).

I will also warn you that this module is not completely compatible with the existing Portage Provider. Rather than making assumptions, this provider will throw errors in the event of ambiguity, preferring developer clarification over the possibility of performing an unintended action.


# Dependencies
The following packages are necessary for this module.

* `app-admin/puppet`
* `sys-apps/portage`
* `app-portage/eix`
* `dev-ruby/xml-simple`


# Environment
The following things are assumed:

* `/etc/portage/package.use` is a directory
* `/etc/portage/package.keywords` is a directory
* Both of the above are free for modification by puppet
* __WARNING:__ Folders contained within either of these will be automatically removed by this plugin


# Research Needed
## Puppet

* We require a provider shutdown function to compliment self.prefetch, that will only be executed once, after all packages have been run
* Ability to add newparam()'s to Puppet Providers and overwrite existing ones, without overwriting the entire type
    * __NOTE:__ this should be done in a flattened manner, not using install_options like the MSI Provider.
* Way to create proper resources for self.prefetch when passed from Rspec tests. We currently don't test this thoroughly enough.


# Roadmap

* Remove package type overwrite (see Research Needed > Puppet)
* "repository" option, to specify the exact overlay to be used


# Roadmap (Undecided)

* Use an external config file
    * __Pro:__ No editing the code
    * __Pro:__ The current most likely don't update when puppet is daemonized
    * __Con:__ Assuming file is managed by puppet, it will take two runs for changes to take effect
* `revdep-rebuild` implemented via shutdown function (see Research Needed > Puppet)


# Features Omitted
These are features we're not implementing at this time

* package mask
    * using puppet `ensure => :held`
* package unmask
* `CONFIG[:useChange]` does not trigger a recompile if global use flags defined in `/etc/make.conf` change.
