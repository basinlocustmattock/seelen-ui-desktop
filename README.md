<div align="center">

# Seelen UI Desktop Environment

**A fully customizable desktop environment for Windows 10 and Windows 11.**

</div>

## 🖥️ Overview

Seelen UI is a desktop environment for Windows 10 and Windows 11 focused on customization. The project is described as a fully customizable desktop environment, intended for users who want a more adaptable Windows desktop experience.

The available documentation in this repository focuses on self-signed certificates used for development builds, especially nightly MSIX packages. These certificates can be trusted locally so that development packages signed with them can be installed and tested in a Windows environment.

## ✨ Key Focus

- Customizable desktop environment for Windows 10/11
- Development support for nightly MSIX package testing
- Self-signed certificate workflow for trusting development builds
- PowerShell-based certificate import instructions

## 🧾 Self-Signed Certificates

This repository documents the use of self-signed certificates for development purposes.

The certificate described in the original documentation is named `Seelen.pfx` and is intended to be imported into the local machine root certificate store so Windows can trust nightly MSIX packages signed with it.

> **Note:** Self-signed certificates are intended for development and testing workflows. They should be handled carefully and replaced when expired.

## 🔐 Certificate Creation

The documented certificate creation command uses `msixherocli.exe`:

```pwsh
msixherocli.exe newcert --directory .\.cert --name Seelen --password Seelen --subject CN=7E60225C-94CB-4B2E-B17F-0159A11074CB --validUntil "14/12/2026 6:31:10 pm"
```

This command creates a development certificate with the name `Seelen`, using the provided subject and expiration date.

## 🛠️ Trusting the Development Certificate

To trust nightly MSIX packages signed with the development certificate, the certificate can be imported into the local machine root certificate store.

Documented workflow:

1. Obtain `Seelen.pfx`.
2. Open PowerShell as Administrator.
3. Navigate to the directory containing the certificate.
4. Run:

```pwsh
$password = ConvertTo-SecureString -String Seelen -Force -AsPlainText
Import-PfxCertificate -FilePath .\Seelen.pfx -CertStoreLocation Cert:\LocalMachine\root -Password $password
```

This imports the certificate into:

```text
Cert:\LocalMachine\root
```

Administrator privileges are required because the certificate is added to the local machine trust store.

## 💻 System Requirements

Based on the project description, Seelen UI targets:

- Windows 10
- Windows 11

No additional hardware, runtime, or installation requirements are specified in the provided documentation.

## ⚠️ Certificate Expiration

The documented certificate workflow includes an important note:

> These files expire each year and should be replaced with new ones.

If a development certificate expires, packages signed with it may no longer be trusted as expected. A new certificate should be generated and installed when needed.

## ❓ FAQ

### What is Seelen UI?

Seelen UI is described as a fully customizable desktop environment for Windows 10 and Windows 11.

### What is the certificate used for?

The self-signed certificate is used in the development environment to trust nightly MSIX packages.

### Do I need administrator permissions to import the certificate?

Yes. The documented import command installs the certificate into the local machine root certificate store, which requires an elevated PowerShell session.

### Is the certificate permanent?

No. The documentation notes that these certificate files expire each year and should be replaced with new ones.

### Is this certificate intended for production use?

The provided documentation describes it as part of the development environment, specifically for trusting nightly MSIX packages. It should be treated as a development certificate.

## 📌 Keywords

Seelen UI, Windows desktop environment, customizable desktop environment, Windows 10 desktop customization, Windows 11 desktop customization, MSIX development certificate, self-signed certificate, PowerShell certificate import.
