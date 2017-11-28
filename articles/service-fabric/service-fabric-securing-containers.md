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
# <a name="container-security"></a><span data-ttu-id="e084f-103">Kontener zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e084f-103">Container security</span></span>

<span data-ttu-id="e084f-104">Sieć szkieletowa usług udostępnia mechanizm dla usług wewnątrz tooaccess kontenera certyfikatu zainstalowanego na powitania węzłów w klastrze systemu Windows lub Linux (w wersji 5.7 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="e084f-104">Service Fabric provides a mechanism for services inside a container tooaccess a certificate that is installed on hello nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="e084f-105">Ponadto sieci szkieletowej usług również obsługuje gMSA (kont usług zarządzanych grupy) dla systemu Windows kontenerów.</span><span class="sxs-lookup"><span data-stu-id="e084f-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="e084f-106">Zarządzanie certyfikatami dla kontenerów</span><span class="sxs-lookup"><span data-stu-id="e084f-106">Certificate management for containers</span></span>

<span data-ttu-id="e084f-107">Określając certyfikatu, można zabezpieczyć swoje usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="e084f-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="e084f-108">Witaj certyfikat należy zainstalować na węzłach hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e084f-108">hello certificate must be installed on hello nodes of hello cluster.</span></span> <span data-ttu-id="e084f-109">Hello informacji o certyfikatach znajduje się w manifeście aplikacji hello w obszarze hello `ContainerHostPolicies` tagu w formie hello fragment kodu przedstawia następujące:</span><span class="sxs-lookup"><span data-stu-id="e084f-109">hello certificate information is provided in hello application manifest under hello `ContainerHostPolicies` tag as hello following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="e084f-110">Przy uruchamianiu aplikacji hello środowiska uruchomieniowego hello odczytuje hello certyfikatów i generuje plik PFX oraz hasła dla każdego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e084f-110">When starting hello application, hello runtime reads hello certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="e084f-111">Ten plik PFX oraz hasła są dostępne w kontenerze hello przy użyciu hello następujące zmienne środowiskowe:</span><span class="sxs-lookup"><span data-stu-id="e084f-111">This PFX file and password are accessible inside hello container using hello following environment variables:</span></span> 

* <span data-ttu-id="e084f-112">**_PFX _ [CertName] Certificate_ [CodePackageName]**</span><span class="sxs-lookup"><span data-stu-id="e084f-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="e084f-113">**_Hasło _ [CertName] Certificate_ [CodePackageName]**</span><span class="sxs-lookup"><span data-stu-id="e084f-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="e084f-114">Usługa kontenera Hello lub proces jest odpowiedzialny za importowanie plików PFX hello hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="e084f-114">hello container service or process is responsible for importing hello PFX file into hello container.</span></span> <span data-ttu-id="e084f-115">tooimport hello certyfikatu, można użyć `setupentrypoint.sh` skrypty lub wykonania kodu niestandardowego, w ramach procesu kontenera hello.</span><span class="sxs-lookup"><span data-stu-id="e084f-115">tooimport hello certificate, you can use `setupentrypoint.sh` scripts or executed custom code within hello container process.</span></span> <span data-ttu-id="e084f-116">Następujący przykładowy kod w języku C# do importowania plików PFX hello:</span><span class="sxs-lookup"><span data-stu-id="e084f-116">Sample code in C# for importing hello PFX file follows:</span></span>

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
<span data-ttu-id="e084f-117">Ten certyfikat PFX można uwierzytelnić hello aplikacji lub usługi lub bezpiecznego commmunication z innymi usługami.</span><span class="sxs-lookup"><span data-stu-id="e084f-117">This PFX certificate can be used for authenticate hello application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="e084f-118">Skonfiguruj grupę dla kontenerów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e084f-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="e084f-119">tooset się przez grupę (grupa zarządzanych kont usług), plik specyfikacji poświadczeń (`credspec`) znajduje się we wszystkich węzłach w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="e084f-119">tooset up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in hello cluster.</span></span> <span data-ttu-id="e084f-120">można skopiować pliku Hello we wszystkich węzłach za pomocą rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e084f-120">hello file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="e084f-121">Witaj `credspec` plik musi zawierać informacje o koncie gMSA hello.</span><span class="sxs-lookup"><span data-stu-id="e084f-121">hello `credspec` file must contain hello gMSA account information.</span></span> <span data-ttu-id="e084f-122">Aby uzyskać więcej informacji na temat hello `credspec` plików, zobacz [kont usług](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="e084f-122">For more information on hello `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="e084f-123">Specyfikacja poświadczeń Hello i hello `Hostname` tag są określone w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e084f-123">hello credential specification and hello `Hostname` tag are specified in hello application manifest.</span></span> <span data-ttu-id="e084f-124">Witaj `Hostname` tag musi odpowiadać nazwie konta gMSA hello, który hello kontenera działa pod.</span><span class="sxs-lookup"><span data-stu-id="e084f-124">hello `Hostname` tag must match hello gMSA account name that hello container runs under.</span></span>  <span data-ttu-id="e084f-125">Witaj `Hostname` tag temu tooauthenticate kontenera hello, samej usługi tooother w domenie hello za pomocą uwierzytelniania Kerberos.</span><span class="sxs-lookup"><span data-stu-id="e084f-125">hello `Hostname` tag allows hello container tooauthenticate itself tooother services in hello domain using Kerberos authentication.</span></span>  <span data-ttu-id="e084f-126">Przykładowy służący do określania hello `Hostname` i hello `credspec` w hello manifest aplikacji jest wyświetlana po fragment hello:</span><span class="sxs-lookup"><span data-stu-id="e084f-126">A sample for specifying hello `Hostname` and hello `credspec` in hello application manifest is shown in hello following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="e084f-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e084f-127">Next steps</span></span>

* [<span data-ttu-id="e084f-128">Wdrażanie systemu Windows tooService kontenera sieci szkieletowej w systemie Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e084f-128">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="e084f-129">Wdrażanie tooService kontenera Docker sieci szkieletowej w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e084f-129">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
