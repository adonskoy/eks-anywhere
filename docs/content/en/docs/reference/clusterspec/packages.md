---
title: "Packages configuration"
linkTitle: "Packages configuration"
weight: 40
description: >
  Full EKS Anywhere configuration reference for curated packages.
---

This is a generic template with detailed descriptions below for reference. To generate your own package configuration, follow instructions from [Package Management]({{< relref "../../tasks/packages" >}}) section and modify it using descriptions below.

```yaml
apiVersion: anywhere.eks.amazonaws.com/v1alpha1
kind: PackageBundleController
metadata:
  name: eksa-packages-bundle-controller
  namespace: eksa-packages
spec:
  activeBundle: "v1-21-1001"
  logLevel: 4
  privateRegistry: public.ecr.aws/eks-anywhere
  source:
    registry: public.ecr.aws/eks-anywhere
    repository: eks-anywhere-packages-bundles
  upgradeCheckInterval: "24h"
  upgradeCheckShortInterval: "5h"

---
apiVersion: packages.eks.amazonaws.com/v1alpha1
kind: PackageBundle
metadata:
  name: package-bundle
  namespace: eksa-packages
spec:
  packages:
  - name: hello-eks-anywhere
    source:
      registry: public.ecr.aws/eks-anywhere
      repository: hello-eks-anywhere
      versions:
      - digest: sha256:da25f5fdff88c259bb2ce7c0f1e9edddaf102dc4fb9cf5159ad6b902b5194e66
        name: v0.0
        images:
        - digest: sha256:da25f5fdff88c259bb2ce7c0f1e9edddaf102dc4fb9cf5159ad6b902b5194e66
          repository: public.ecr.aws/eks-anywhere

---
apiVersion: packages.eks.amazonaws.com/v1alpha1
kind: Package
metadata:
  name: my-hello-eks-anywhere
  namespace: eksa-packages
spec:
  packageName: hello-eks-anywhere
  packageVersion: v0.0.0-f47374093e8a9c48aca8c7a7f06ae185eb7506f3-helm
  targetNamespace: eksa-packages

```

## PackageBundleController Fields
### PackageBundleController
PackageBundleController is the Schema for the packagebundlecontroller API.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
      <td><b>apiVersion</b></td>
      <td>string</td>
      <td>packages.eks.amazonaws.com/v1alpha1</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b>kind</b></td>
      <td>string</td>
      <td>PackageBundleController</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b><a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.20/#objectmeta-v1-meta">metadata</a></b></td>
      <td>object</td>
      <td>Refer to the Kubernetes API documentation for the fields of the `metadata` field.</td>
      <td>true</td>
      </tr><tr>
        <td><b><a href="#packagebundlecontrollerspec">spec</a></b></td>
        <td>object</td>
        <td>
          PackageBundleControllerSpec defines the desired state of PackageBundleController.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#packagebundlecontrollerstatus">status</a></b></td>
        <td>object</td>
        <td>
          PackageBundleControllerStatus defines the observed state of PackageBundleController.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### PackageBundleController.spec
<sup><sup>[↩ Parent](#packagebundlecontroller)</sup></sup>



PackageBundleControllerSpec defines the desired state of PackageBundleController.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#packagebundlecontrollerspecsource">source</a></b></td>
        <td>object</td>
        <td>
          Source of the bundle.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>activeBundle</b></td>
        <td>string</td>
        <td>
          ActiveBundle is name of the bundle from which packages should be sourced.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>logLevel</b></td>
        <td>integer</td>
        <td>
          LogLevel controls the verbosity of logging in the controller.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>privateRegistry</b></td>
        <td>string</td>
        <td>
          PrivateRegistry is the registry being used for all images, charts and bundles<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>upgradeCheckInterval</b></td>
        <td>string</td>
        <td>
          UpgradeCheckInterval is the time between upgrade checks. 
 The format is that of time's ParseDuration.<br/>
          <br/>
            <i>Default</i>: 1d<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>upgradeCheckShortInterval</b></td>
        <td>string</td>
        <td>
          UpgradeCheckShortInterval time between upgrade checks if there is a problem. 
 The format is that of time's ParseDuration.<br/>
          <br/>
            <i>Default</i>: 1h<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### PackageBundleController.spec.source
<sup><sup>[↩ Parent](#packagebundlecontrollerspec)</sup></sup>



Source of the bundle.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>registry</b></td>
        <td>string</td>
        <td>
          Registry portion of an OCI address to the bundle<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>repository</b></td>
        <td>string</td>
        <td>
          Repository portion of an OCI address to the bundle<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


#### PackageBundleController.status
<sup><sup>[↩ Parent](#packagebundlecontroller)</sup></sup>



PackageBundleControllerStatus defines the observed state of PackageBundleController.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>detail</b></td>
        <td>string</td>
        <td>
          Detail of the state.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>state</b></td>
        <td>enum</td>
        <td>
          State of the bundle controller.<br/>
          <br/>
            <i>Enum</i>: ignored, active, disconnected<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


## PackageBundle Fields
### PackageBundle
PackageBundle is the Schema for the packagebundle API.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
      <td><b>apiVersion</b></td>
      <td>string</td>
      <td>packages.eks.amazonaws.com/v1alpha1</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b>kind</b></td>
      <td>string</td>
      <td>PackageBundle</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b><a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.20/#objectmeta-v1-meta">metadata</a></b></td>
      <td>object</td>
      <td>Refer to the Kubernetes API documentation for the fields of the `metadata` field.</td>
      <td>true</td>
      </tr><tr>
        <td><b><a href="#packagebundlespec">spec</a></b></td>
        <td>object</td>
        <td>
          PackageBundleSpec defines the desired state of PackageBundle.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#packagebundlestatus">status</a></b></td>
        <td>object</td>
        <td>
          PackageBundleStatus defines the observed state of PackageBundle.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### PackageBundle.spec
<sup><sup>[↩ Parent](#packagebundle)</sup></sup>



PackageBundleSpec defines the desired state of PackageBundle.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#packagebundlespecpackagesindex">packages</a></b></td>
        <td>[]object</td>
        <td>
          Packages supported by this bundle.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


#### PackageBundle.spec.packages[index]
<sup><sup>[↩ Parent](#packagebundlespec)</sup></sup>



BundlePackage specifies a package within a bundle.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#packagebundlespecpackagesindexsource">source</a></b></td>
        <td>object</td>
        <td>
          Source location for the package (probably a helm chart).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the package.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### PackageBundle.spec.packages[index].source
<sup><sup>[↩ Parent](#packagebundlespecpackagesindex)</sup></sup>



Source location for the package (probably a helm chart).

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>repository</b></td>
        <td>string</td>
        <td>
          Repository within the Registry where the package is found.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#packagebundlespecpackagesindexsourceversionsindex">versions</a></b></td>
        <td>[]object</td>
        <td>
          Versions of the package supported by this bundle.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>registry</b></td>
        <td>string</td>
        <td>
          Registry in which the package is found.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### PackageBundle.spec.packages[index].source.versions[index]
<sup><sup>[↩ Parent](#packagebundlespecpackagesindexsource)</sup></sup>



SourceVersion describes a version of a package within a repository.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>digest</b></td>
        <td>string</td>
        <td>
          Digest is a checksum value identifying the version of the package and its contents.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is a human-friendly description of the version, e.g. "v1.0".<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#packagebundlespecpackagesindexsourceversionsindeximagesindex">images</a></b></td>
        <td>[]object</td>
        <td>
          Images is a list of images used by this version of the package.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>schema</b></td>
        <td>string</td>
        <td>
          Schema is a base64 encoded, gzipped json schema used to validate package configurations.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### PackageBundle.spec.packages[index].source.versions[index].images[index]
<sup><sup>[↩ Parent](#packagebundlespecpackagesindexsourceversionsindex)</sup></sup>



VersionImages is an image used by a version of a package.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>digest</b></td>
        <td>string</td>
        <td>
          Digest is a checksum value identifying the version of the package and its contents.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>repository</b></td>
        <td>string</td>
        <td>
          Repository within the Registry where the package is found.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


#### PackageBundle.status
<sup><sup>[↩ Parent](#packagebundle)</sup></sup>



PackageBundleStatus defines the observed state of PackageBundle.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>state</b></td>
        <td>enum</td>
        <td>
          PackageBundleStateEnum defines the observed state of PackageBundle.<br/>
          <br/>
            <i>Enum</i>: available, ignored, invalid<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#packagebundlestatusspec">spec</a></b></td>
        <td>object</td>
        <td>
          PackageBundleSpec defines the desired state of PackageBundle.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### PackageBundle.status.spec
<sup><sup>[↩ Parent](#packagebundlestatus)</sup></sup>



PackageBundleSpec defines the desired state of PackageBundle.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#packagebundlestatusspecpackagesindex">packages</a></b></td>
        <td>[]object</td>
        <td>
          Packages supported by this bundle.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


#### PackageBundle.status.spec.packages[index]
<sup><sup>[↩ Parent](#packagebundlestatusspec)</sup></sup>



BundlePackage specifies a package within a bundle.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#packagebundlestatusspecpackagesindexsource">source</a></b></td>
        <td>object</td>
        <td>
          Source location for the package (probably a helm chart).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the package.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### PackageBundle.status.spec.packages[index].source
<sup><sup>[↩ Parent](#packagebundlestatusspecpackagesindex)</sup></sup>



Source location for the package (probably a helm chart).

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>repository</b></td>
        <td>string</td>
        <td>
          Repository within the Registry where the package is found.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#packagebundlestatusspecpackagesindexsourceversionsindex">versions</a></b></td>
        <td>[]object</td>
        <td>
          Versions of the package supported by this bundle.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>registry</b></td>
        <td>string</td>
        <td>
          Registry in which the package is found.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### PackageBundle.status.spec.packages[index].source.versions[index]
<sup><sup>[↩ Parent](#packagebundlestatusspecpackagesindexsource)</sup></sup>



SourceVersion describes a version of a package within a repository.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>digest</b></td>
        <td>string</td>
        <td>
          Digest is a checksum value identifying the version of the package and its contents.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is a human-friendly description of the version, e.g. "v1.0".<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#packagebundlestatusspecpackagesindexsourceversionsindeximagesindex">images</a></b></td>
        <td>[]object</td>
        <td>
          Images is a list of images used by this version of the package.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>schema</b></td>
        <td>string</td>
        <td>
          Schema is a base64 encoded, gzipped json schema used to validate package configurations.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### PackageBundle.status.spec.packages[index].source.versions[index].images[index]
<sup><sup>[↩ Parent](#packagebundlestatusspecpackagesindexsourceversionsindex)</sup></sup>



VersionImages is an image used by a version of a package.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>digest</b></td>
        <td>string</td>
        <td>
          Digest is a checksum value identifying the version of the package and its contents.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>repository</b></td>
        <td>string</td>
        <td>
          Repository within the Registry where the package is found.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


## Package Fields
### Package
Package is the Schema for the package API.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
      <td><b>apiVersion</b></td>
      <td>string</td>
      <td>packages.eks.amazonaws.com/v1alpha1</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b>kind</b></td>
      <td>string</td>
      <td>Package</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b><a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.20/#objectmeta-v1-meta">metadata</a></b></td>
      <td>object</td>
      <td>Refer to the Kubernetes API documentation for the fields of the `metadata` field.</td>
      <td>true</td>
      </tr><tr>
        <td><b><a href="#packagespec">spec</a></b></td>
        <td>object</td>
        <td>
          PackageSpec defines the desired state of an package.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#packagestatus">status</a></b></td>
        <td>object</td>
        <td>
          PackageStatus defines the observed state of Package.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### Package.spec
<sup><sup>[↩ Parent](#package)</sup></sup>



PackageSpec defines the desired state of an package.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>packageName</b></td>
        <td>string</td>
        <td>
          PackageName is the name of the package as specified in the bundle.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>config</b></td>
        <td>string</td>
        <td>
          Config for the package.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>packageVersion</b></td>
        <td>string</td>
        <td>
          PackageVersion is a human-friendly version name or sha256 checksum for the package, as specified in the bundle.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>targetNamespace</b></td>
        <td>string</td>
        <td>
          TargetNamespace defines where package resources will be deployed.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### Package.status
<sup><sup>[↩ Parent](#package)</sup></sup>



PackageStatus defines the observed state of Package.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>currentVersion</b></td>
        <td>string</td>
        <td>
          Version currently installed.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#packagestatussource">source</a></b></td>
        <td>object</td>
        <td>
          Source associated with the installation.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>detail</b></td>
        <td>string</td>
        <td>
          Detail of the state.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>state</b></td>
        <td>enum</td>
        <td>
          State of the installation.<br/>
          <br/>
            <i>Enum</i>: initializing, installing, installed, updating, uninstalling, unknown<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>targetVersion</b></td>
        <td>string</td>
        <td>
          Version to be installed.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#packagestatusupgradesavailableindex">upgradesAvailable</a></b></td>
        <td>[]object</td>
        <td>
          UpgradesAvailable indicates upgraded versions in the bundle.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


#### Package.status.source
<sup><sup>[↩ Parent](#packagestatus)</sup></sup>



Source associated with the installation.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>digest</b></td>
        <td>string</td>
        <td>
          Digest is a checksum value identifying the version of the package and its contents.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>registry</b></td>
        <td>string</td>
        <td>
          Registry in which the package is found.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>repository</b></td>
        <td>string</td>
        <td>
          Repository within the Registry where the package is found.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>version</b></td>
        <td>string</td>
        <td>
          Versions of the package supported.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


#### Package.status.upgradesAvailable[index]
<sup><sup>[↩ Parent](#packagestatus)</sup></sup>



PackageAvailableUpgrade details the package's available upgrade versions.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>tag</b></td>
        <td>string</td>
        <td>
          Tag is a specific version number or sha256 checksum for the package upgrade.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>version</b></td>
        <td>string</td>
        <td>
          Version is a human-friendly version name for the package upgrade.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>