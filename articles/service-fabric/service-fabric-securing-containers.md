---
title: "aaaAzure zabezpieczeń kontenera sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Dowiedz się teraz toosecure kontenera usług."
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
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a>Kontener zabezpieczeń

Sieć szkieletowa usług udostępnia mechanizm dla usług wewnątrz tooaccess kontenera certyfikatu zainstalowanego na powitania węzłów w klastrze systemu Windows lub Linux (w wersji 5.7 lub nowszej). Ponadto sieci szkieletowej usług również obsługuje gMSA (kont usług zarządzanych grupy) dla systemu Windows kontenerów. 

## <a name="certificate-management-for-containers"></a>Zarządzanie certyfikatami dla kontenerów

Określając certyfikatu, można zabezpieczyć swoje usługi kontenera. Witaj certyfikat należy zainstalować na węzłach hello hello klastra. Hello informacji o certyfikatach znajduje się w manifeście aplikacji hello w obszarze hello `ContainerHostPolicies` tagu w formie hello fragment kodu przedstawia następujące:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Przy uruchamianiu aplikacji hello środowiska uruchomieniowego hello odczytuje hello certyfikatów i generuje plik PFX oraz hasła dla każdego certyfikatu. Ten plik PFX oraz hasła są dostępne w kontenerze hello przy użyciu hello następujące zmienne środowiskowe: 

* **_PFX _ [CertName] Certificate_ [CodePackageName]**
* **_Hasło _ [CertName] Certificate_ [CodePackageName]**

Usługa kontenera Hello lub proces jest odpowiedzialny za importowanie plików PFX hello hello kontenera. tooimport hello certyfikatu, można użyć `setupentrypoint.sh` skrypty lub wykonania kodu niestandardowego, w ramach procesu kontenera hello. Następujący przykładowy kod w języku C# do importowania plików PFX hello:

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
Ten certyfikat PFX można uwierzytelnić hello aplikacji lub usługi lub bezpiecznego commmunication z innymi usługami.


## <a name="set-up-gmsa-for-windows-containers"></a>Skonfiguruj grupę dla kontenerów systemu Windows

tooset się przez grupę (grupa zarządzanych kont usług), plik specyfikacji poświadczeń (`credspec`) znajduje się we wszystkich węzłach w klastrze hello. można skopiować pliku Hello we wszystkich węzłach za pomocą rozszerzenia maszyny Wirtualnej.  Witaj `credspec` plik musi zawierać informacje o koncie gMSA hello. Aby uzyskać więcej informacji na temat hello `credspec` plików, zobacz [kont usług](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). Specyfikacja poświadczeń Hello i hello `Hostname` tag są określone w manifeście aplikacji hello. Witaj `Hostname` tag musi odpowiadać nazwie konta gMSA hello, który hello kontenera działa pod.  Witaj `Hostname` tag temu tooauthenticate kontenera hello, samej usługi tooother w domenie hello za pomocą uwierzytelniania Kerberos.  Przykładowy służący do określania hello `Hostname` i hello `credspec` w hello manifest aplikacji jest wyświetlana po fragment hello:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Następne kroki

* [Wdrażanie systemu Windows tooService kontenera sieci szkieletowej w systemie Windows Server 2016](service-fabric-get-started-containers.md)
* [Wdrażanie tooService kontenera Docker sieci szkieletowej w systemie Linux](service-fabric-get-started-containers-linux.md)
