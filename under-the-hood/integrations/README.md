---
icon: code-merge
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
  metadata:
    visible: false
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
tags:
  - integration
---

# Integrations

## What is an Integration?

COZY is just one piece of a much larger project that you are developing. Because of that, COZY tries to follow two core principles:

1. Be self contained
2. Support the development using third-party plugins

While this principle means designing COZY in a way that makes it easy to work with both via API documentation, etc., we can do even better. An **Integration** is our way of directly supporting a third party package that you may be using in your project.&#x20;

### How Integrations are Handled

Integrations in COZY are handled completely under the hood as opposed to the modular workflow used in COZY 3. This means that when adding a supported package to your Unity project, everything will automatically connect to COZY directly without any additional work needed.

## Working with Integrations

### The Integrations Window

To view the status of all of your integrations, open the Integrations window. You can find this either in the COZY Weather component inspector or the menu at  `Tools/COZY: Weather 4/Integrations`

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Once the window is open, you can see all of the available integrations for your project. If an integration is grayed out, it is not detected in your project. Otherwise, it will be labelled as "In Project". The "In Project" check is done via conditional compilers that will occasionally change as they are managed by third parties. If this occurs, you can generally remove the conditional compilation statements from the integration script or add the compiler that the script is looking for and it will be recognized as included in your project.

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
If the integration relies on certain things being setup in the scene (for example, the Zephyr integration requires an instance of Zephyr to be in your scene) and the requirements are not met, you will see a warning icon or error icon in the header for the integration. Integrations with a **warning** will still run, but the warning should be addressed. Integrations with an **error** will not run.
{% endhint %}

### Integration Properties

Each integration is composed of a header and a foldout that contains properties. Unfurling the header allows you to see any properties that are exposed for the integration. These properties are _**project-wide**_ and will not be limited to the active scene.

### Integration Types

#### Logic

Logic integrations run logic to hook COZY's systems up to another system.

#### Installable

Installable integrations do not run logic but rather make permanent changes to your project by installing a change. Normally, these are reserved for shaders or installable .unitypackages.

#### Other

Some integrations do neither of these operations and are handled exclusively by the third party.&#x20;

## Developing Custom Integrations

While we strive to support most of the popular packages on the Unity Asset Store, there are plenty of reasons to want to develop your own integration if you are creating your own asset or working with custom systems. See the guide on creating your own integrations here: [build-an-integration.md](../../extending-cozy/build-an-integration.md "mention")
