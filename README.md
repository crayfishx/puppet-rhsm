# rhsm

## Description

A puppet module to manage Redhat subscriptions using the subscription-manager


## Module Description

This module provides the `rh_subscription` type that can be used to add and remove subscriptions

## Usage

Use Puppet to add or remove a subscription based on it's pool ID

    rh_subscription { '8e8e7f7a77554a776277ac6dca654':
      ensure => present,
    }

## Hiera

The rhsm class also provides a helper using `create_resources()` to configure any subscriptions in hiera

    ---
    rhsm::subscriptions:
      8e8e7f7a77554a776277ac6dca654: {}
      8e8e7f7a77554a776277e63d13ca4: {}
     
Puppet will automatically configure these subscriptions when the rhsm class is declared.

    class { '::rhsm': }

The module also provides a way to store pool IDs with corresponding readable names and refer to those in your manifests

    ---
    rhsm::pool_names:
      rhel_extras:  8e8e7f7a77554a776277ac6dca654
      oracle_stuff: 8e8e7f7a77554a776277e63d13ca4

You can then declare these subscriptions from hiera....

    ---
    rhsm::named_subscriptions:
      rhel_extras: {}
      oracle_stuff: {}

Or use the `rhsm::named_subscription` defined resource type directly

    class { '::rhsm': }

    rhsm::named_subscription { 'oracle_stuff':
      ensure => present,
    }

## Credits

* Written and maintained by Craig Dunn <craig@craigdunn.org>
* Sponsered by Baloise Group [http://baloise.github.io](http://baloise.github.io)
