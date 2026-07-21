# Packages and Data Kits | Get Started with Data 360 Development | Data 360 Developer Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dev/guide/packages-data-kits.html

---

A package is a container to which you can add metadata components. It holds the set of related features, customizations, and schema that comprise your app. When packaging Data 360 metadata, you must add the metadata to a data kit, and then add the data kit to the package. Data kits streamline the package creation and installation process.

For Data 360, the metadata represents the definition of Data 360 components in the Data 360 org and not the data. For example, the metadata can represent the definitions of calculated insights, profiles, and data streams.

If you’re packaging both Data 360 metadata and Salesforce Platform metadata, create two separate packages: one for Data 360 metadata and one for all other metadata. Starting in Winter ‘25, including both Data 360 metadata, and non-Data 360 metadata in a single package isn’t allowed.

To package Data 360 metadata components, first add the components to a data kit. Then add the data kit to a package. The package is then used to install the Data 360 components in a different org. A package can contain one or more data kits.

If you’re packaging both Data 360 metadata and Salesforce Platform metadata, create two separate packages: one for Data 360 metadata and one for all other metadata. Starting in Winter ‘25, including both Data 360 metadata and non-Data 360 metadata in a single package isn’t allowed. You can’t add Data 360 metadata in an unlocked package.

Customer developers, that is, developers doing in-house development for their own Data 360 instance, use data kits with unmanaged packages to deploy metadata from a test org to a production org.

Salesforce partners who build apps and distribute them on AppExchange use managed packages to do both. Salesforce partners can develop apps for Data 360 customers. For managed packages, make sure that the namespace is enabled for your organization. For more information, see Create and Register Your Namespace

All Data 360 feature metadata in a managed package is locked. As a package owner, you can control and protect the data kit metadata from unauthorized changes. After you install a package and deploy the data kit components, the components are locked. Susbcribers can add entities but can’t modify or delete any deployed mappings or entities. If modifications are made to the deployed metadata entities, they’re overwritten when the data kit is redeployed.

To find out which Data 360 components are packageable, see Data 360 Extensibility Readiness Matrix.

For Data 360 components that aren’t available in data kits, you can add them to a package. To find out which components are available in packages, see Metadata Components for Data 360 Cheat Sheet. Also, check the Metadata Coverage Report.

See Also

Trailhead: Packaging and Data Kits in Data Cloud
Help: Build and Share Data 360 Functionality
Help: Packaging in Data Cloud
