---
title: Windows 11 security book - Secure supply chain
description: Security foundation chapter - Secure supply chain.
ms.topic: overview
ms.date: 11/18/2024
---

# Secure supply chain

:::image type="content" source="images/security-foundation.png" alt-text="Diagram containing a list of security features." lightbox="images/security-foundation.png" border="false":::

The end-to-end Windows 11 supply chain is complex. It extends from the entire development process, to components such as chips, firmware, drivers, operating system, and apps from other organizations, manufacturing, and security updates. Microsoft invests significantly in Windows 11 supply chain security, and the security of features and components. In 2021, the United States issued an executive order on enhancing the nation's cybersecurity. The executive order, along with various attacks like SolarWinds and WannaCry, elevated the urgency and importance of ensuring a secure supply chain.

Microsoft requires the Windows 11 supply chain to comply with controls including:

- Identity management and user access control
  - Access control
  - Principles of least privilege
  - Role-based access control (role-based access control)
  - Segregation of duties
  - MFAs
  - Account management
  - Physical access control
- Information security
  - Information handling
  - Cryptography
  - Vulnerability scanning
  - Encryption
  - Integrity and attestation
  - Confidentiality
- Operational controls
  - Code of repo ownership
  - Config & change management
  - Asset ownership
  - Manufacturing standards
- Security monitoring & event logging
  - Network
  - Host
  - Application
  - Services
  - DevOps
  - Manufacturing security
  - Physical security monitoring
- Supplier security control
  - Supplier Security and Privacy Assurance (SSPA)
  - Supplier screening
  - Supplier inventory
- Logistics security control
  - Receiving
  - Shipping
  - Warehouse & storage
  - Logistics management

## Software bill of materials (SBOM)

In the Windows ecosystem, ensuring the integrity and authenticity of software components is paramount. To achieve this, we utilize Software Bill of Materials (SBOMs) and COSE (CBOR Object Signing and Encryption) sign all evidence. SBOMs provide a comprehensive inventory of software components, including their dependencies and associated metadata. Transparency is crucial for vulnerability management and compliance with security standards.

The COSE signing process enhances the trustworthiness of SBOMs by providing cryptographic signatures that verify the integrity and authenticity of the SBOM content. The CoseSignTool, a platform-agnostic command line application, is employed to apply and verify these digital signatures. This tool ensures that all SBOMs and other build evidence are signed and validated, maintaining a high level of security within the software supply chain.

By integrating SBOMs and COSE signing evidence, we offer stakeholders visibility into the components they use, ensuring that all software artifacts are trustworthy and secure. This approach aligns with our commitment to end-to-end supply chain security, providing a robust framework for managing and verifying software components across the Windows ecosystem.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [SBOM tool](https://github.com/microsoft/sbom-tool)
- [Code Sign Tool](https://github.com/microsoft/CoseSignTool)

## Windows Software Development Kit (SDK)

Developers can design highly secure applications that benefit from the latest Windows 11 safeguards using the Windows SDK. The SDK provides a unified set of APIs and tools for developing secure desktop apps for Windows 11 and Windows 10. To help create apps that are up to date and protected, the SDK follows the same security standards, protocols, and compliance as the core Windows operating system.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Windows application development - best practices](/windows/apps/get-started/best-practices)
- [Windows SDK samples on GitHub](https://github.com/microsoft/WindowsAppSDK-Samples)