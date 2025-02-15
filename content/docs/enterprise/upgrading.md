---
title: Upgrading
description: This page contains the list of deprecations and important or breaking changes for Pomerium Enterprise. Please read it carefully.
---

#  Upgrading Pomerium Enterprise

When new version of Pomerium Enterprise are released, check back to this page before you upgrade.

## 0.18.0

## Before You Upgrade

- When using [`external-data`](/docs/enterprise/external-data) the Databroker backend for Pomerium should be switched from Redis to [Postgres](/docs/topics/data-storage#postgres).

## 0.17.0

## Before You Upgrade

- The new `license-key`  option is required for starting Pomerium Enterprise. Please contact your account team if you have not been issued one yet.

## 0.16.0

## Before You Upgrade

- The [`signing-key`](/docs/enterprise/reference/config#signing-key) has been replaced with [`authenticate-service-url`](/docs/enterprise/reference/config#authenticate-service-url). Instead of manually setting the signing key in the Enterprise Console to match the Authenticate Service, we specify the trusted URL of the Authenticate Service to pull the signing key from.

  The `signing-key` key will continue to work for existing configurations, but [device enrollment](/docs/enterprise/reference/manage#new-enrollment) will not work until it is replaced by `authenticate-service-url`.

## 0.15.0

### Before You Upgrade

- `signing-key` is now a required option to improve request security from Pomerium Core. The value should match the one set in Pomerium Core. See the [signing key] reference page for more information on generating a key.
- `audience` is now a required option to improve request security from Pomerium Core. The value should match the Enterprise Console's external URL hostname, as defined in the [`from`](/docs/reference/routes) field in the Routes entry (not including the protocol).

[signing key]: /docs/reference/signing-key

### Helm Installations

- As of v0.15.0, All Helm charts have been consolidated to a single repository. Remove the `pomerium-enterprise` repo and upgrade from `pomerium`:

   ```bash
   helm repo remove pomerium-enterprise
   helm upgrade --install pomerium-console pomerium/pomerium-console --values=pomerium-console-values.yaml
   ```

- As noted above, `signing-key` must be shared between Pomerium and Enterprise. See the [Update Pomerium](/docs/enterprise/install/helm#update-pomerium) section of [Install Pomerium Enterprise in Helm](/docs/enterprise/install/helm) for more information.
