---
title: "Zabezpieczeń kontenera sieci szkieletowej usług platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się teraz w celu zabezpieczenia usługi kontenerów."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 75faca1e827a0eca6b97adcb2e1c6ca72b3364d6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="container-security"></a>Kontener zabezpieczeń

Sieć szkieletowa usług udostępnia mechanizm dla usług wewnątrz kontenera można uzyskać dostępu do certyfikatu, który jest zainstalowany na węzłach w klastrze systemu Windows lub Linux (w wersji 5.7 lub nowszej). Ponadto sieci szkieletowej usług również obsługuje gMSA (kont usług zarządzanych grupy) dla systemu Windows kontenerów. 

## <a name="certificate-management-for-containers"></a>Zarządzanie certyfikatami dla kontenerów

Określając certyfikatu, można zabezpieczyć swoje usługi kontenera. Certyfikat należy zainstalować na węzłach klastra. Informacje o certyfikacie znajduje się w manifeście aplikacji w obszarze `ContainerHostPolicies` tagu w formie poniższy fragment kodu przedstawia:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Podczas uruchamiania aplikacji, środowisko uruchomieniowe odczytuje certyfikaty i generuje plik PFX oraz hasła dla każdego certyfikatu. Ten plik PFX oraz hasła są dostępne w kontenerze, za pomocą następujących zmiennych środowiskowych: 

* **_PFX _ [CertName] Certificate_ [CodePackageName]**
* **_Hasło _ [CertName] Certificate_ [CodePackageName]**

Usługa kontenera lub proces jest odpowiedzialny za zaimportować plik PFX do kontenera. Aby zaimportować certyfikat, można użyć `setupentrypoint.sh` skrypty lub wykonania kodu niestandardowego, w ramach procesu kontenera. Następujący przykładowy kod w języku C# do importowania plików PFX:

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
Ten certyfikat PFX mogą służyć do uwierzytelniania aplikacji lub usługi lub bezpiecznego commmunication z innymi usługami.


## <a name="set-up-gmsa-for-windows-containers"></a>Skonfiguruj grupę dla kontenerów systemu Windows

Aby skonfigurować usługi zarządzane przez grupę (grupa zarządzanych kont usług), plik specyfikacji poświadczeń (`credspec`) znajduje się we wszystkich węzłach w klastrze. We wszystkich węzłach za pomocą rozszerzenia maszyny Wirtualnej można skopiować pliku.  `credspec` Plik musi zawierać informacje o koncie gMSA. Aby uzyskać więcej informacji na temat `credspec` plików, zobacz [kont usług](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). Specyfikacja poświadczeń i `Hostname` tag są określone w manifeście aplikacji. `Hostname` Tag musi odpowiadać nazwie konta gMSA działającą w kontenerze.  `Hostname` Tagu umożliwia kontenera do samodzielnego uwierzytelnienia w innych usługach w domenie przy użyciu uwierzytelniania Kerberos.  Przykładowy służący do określania `Hostname` i `credspec` w aplikacji manifestu jest wyświetlany w następujący fragment kodu:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Następne kroki

* [Wdrażanie kontenera systemu Windows w sieci szkieletowej usług w systemie Windows Server 2016](service-fabric-get-started-containers.md)
* [Wdrażanie kontenera Docker sieci szkieletowej usług w systemie Linux](service-fabric-get-started-containers-linux.md)
