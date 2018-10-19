# Manifest

The Evaneos manifest to describe services of its Information System.


## The file
The file must be named `MANIFEST.json` and be put under the project root.

If your project has its own repository, it must be at the root of the repository.

If your project shares a repository with other projects (like in `evaneos-ng`), put it under the directory containing your source (same level as your `composer.json` or `package.json`).

##The format
It is a `json` file, so it must respect the `json` format.
Furthermore, there's a `Json Schema` describing it, allowing you to validate your manifest against it (and having autocomplete).

To do that, you'll need to declare the schema to use for your file:

```json
{
    "$schema": "https://raw.githubusercontent.com/Evaneos/json-schemas/master/MANIFEST/MANIFEST-v1.0.0.schema.json",
    ...
}
```

### Languages
In the `languages` section, you'll have to list the languages used by your application, alongside the main frameworks it uses.

You don't have to be over-descriptive here, as some information will be retrieved from the `composer.json` or `package.json` later on.

### Services
In the `services` section, you'll have to describe every service your application needs to work.

This includes `databases`, `message queues`, other `applications` or any other `third-party` service.

Be careful when naming your services. It has to have the same name in other `MANIFEST.json` files if that's a shared service (`shared-database` for example).

### Domains
In the `domains` section, you'll have to list the domains hosted by your application.

Only list the domains directly embedded in your code. If it's imported through a bundle, the manifest of the bundle will describe it.

### Infrastructure
In the `infrastructure` section, you'll have to list the `http hosts` your application responds to.

### Deploy
In the `deploy` section, you'll describe which method is used to deploy your code to production, and where it's deployed at.

### Messages
This section is divided in 2: the `outbound` and `inbound` messages.

For now, this section will only contain messages that are `Domain events`.

#### Outbound Messages
In the `outbound` section, you'll find the `events` section.

In it, you'll be able to describe all the events your application produces. Please name it as it is named in your application.

For now, we'll only describe events produced by a `business domain`. So you'll have to specify the `domain` it's from (use the same name as describe a little earlier in the `domains` section).

If your event is dispatched, as it should be, you'll have two cases to specify.

If it's dispatched internally, you'll have to specify for which use.

If it's dispatched to a message queue, you'll have to specify to which one (name the `service` by using the name specified in the `services` section) and the exchange it's dispatched to (the normalization of an `exchange` name is `[<vhost>]<name of your exchange>`).

It can be dispatched both locally and to a message queue (or multiple messages queues).

#### Inbound Messages

In the `inbound` section, you'll find the `events` section.

In it, you'll be able to describe all the events your application consumes. Please name it as it is named in your application.

For now, we'll only describe events produced by a `business domain`. So you'll have to specify the `domain` it's from (use the same name as describe a little earlier in the `domains` section).

If your event is dispatched from a message queue, you'll have to specify from which one (name the `service` by using the name specified in the `services` section) and the queue it's consumed from (the normalization of a `queue` name is `[<vhost>]<name of your queue>`).


## Example

You can find different examples in `evaneos-ng`.

Look at the one for `www.evaneos.com` which contains all cases.