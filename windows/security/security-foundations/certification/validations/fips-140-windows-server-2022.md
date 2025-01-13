---
title: FIPS 140 validated modules for Windows Server 2022
description: This topic lists the completed FIPS 140 cryptographic module validations for Windows Server 2022.
ms.date: 11/13/2024
ms.topic: reference
---

# FIPS 140 validated modules in Windows Server 2022

The following tables list the completed FIPS 140 validations of cryptographic modules used in Windows Server 2022, organized by major release of the operating system. The linked Security Policy document for each module provides details on the module capabilities and the policies the operator must follow to use the module in its FIPS approved mode of operation. For information on using the overall operating system in its FIPS approved mode, see [Use Windows in a FIPS approved mode of operation](../fips-140-validation.md#use-windows-in-a-fips-approved-mode-of-operation). For details on the FIPS approved algorithms used by each module, see its linked Security Policy document or module certificate.

## Windows Server 2022

Build: 10.0.20348. Validated Editions: Standard, Datacenter, and Datacenter: Azure.

|Cryptographic Module (linked to Security Policy document)|CMVP Certificate #|Validated Algorithms|
|--- |--- |--- |
|[Cryptographic Primitives Library][sp-4825]|[#4825][certificate-4825]|FIPS Approved: AES, CKG, CVL, DRBG, DSA, ECDSA, ENT (P), HMAC, KAS, KAS-SSC, KBKDF, KTS, PBKDF, RSA, SHS, and Triple-DES|
|[Kernel Mode Cryptographic Primitives Library][sp-4766]|[#4766][certificate-4766]|FIPS Approved: AES, CKG, CVL, DRBG, DSA, ECDSA, ENT (P), HMAC, KAS, KAS-SSC, KBKDF, KTS, PBKDF, RSA, SHS, and Triple-DES|

---

<!-- Links -->

<!-- CMVP Certificates -->

[certificate-4766]: https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/4766
[certificate-4825]: https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/4825

<!-- Security Policies -->

[sp-4766]: https://csrc.nist.gov/CSRC/media/projects/cryptographic-module-validation-program/documents/security-policies/140sp4766.pdf
[sp-4825]: https://csrc.nist.gov/CSRC/media/projects/cryptographic-module-validation-program/documents/security-policies/140sp4825.pdf
