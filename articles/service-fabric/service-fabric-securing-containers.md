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
# <a name="container-security"></a><span data-ttu-id="62cb7-103">Kontener zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="62cb7-103">Container security</span></span>

<span data-ttu-id="62cb7-104">Sieć szkieletowa usług udostępnia mechanizm dla usług wewnątrz kontenera można uzyskać dostępu do certyfikatu, który jest zainstalowany na węzłach w klastrze systemu Windows lub Linux (w wersji 5.7 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="62cb7-104">Service Fabric provides a mechanism for services inside a container to access a certificate that is installed on the nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="62cb7-105">Ponadto sieci szkieletowej usług również obsługuje gMSA (kont usług zarządzanych grupy) dla systemu Windows kontenerów.</span><span class="sxs-lookup"><span data-stu-id="62cb7-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="62cb7-106">Zarządzanie certyfikatami dla kontenerów</span><span class="sxs-lookup"><span data-stu-id="62cb7-106">Certificate management for containers</span></span>

<span data-ttu-id="62cb7-107">Określając certyfikatu, można zabezpieczyć swoje usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="62cb7-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="62cb7-108">Certyfikat należy zainstalować na węzłach klastra.</span><span class="sxs-lookup"><span data-stu-id="62cb7-108">The certificate must be installed on the nodes of the cluster.</span></span> <span data-ttu-id="62cb7-109">Informacje o certyfikacie znajduje się w manifeście aplikacji w obszarze `ContainerHostPolicies` tagu w formie poniższy fragment kodu przedstawia:</span><span class="sxs-lookup"><span data-stu-id="62cb7-109">The certificate information is provided in the application manifest under the `ContainerHostPolicies` tag as the following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="62cb7-110">Podczas uruchamiania aplikacji, środowisko uruchomieniowe odczytuje certyfikaty i generuje plik PFX oraz hasła dla każdego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="62cb7-110">When starting the application, the runtime reads the certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="62cb7-111">Ten plik PFX oraz hasła są dostępne w kontenerze, za pomocą następujących zmiennych środowiskowych:</span><span class="sxs-lookup"><span data-stu-id="62cb7-111">This PFX file and password are accessible inside the container using the following environment variables:</span></span> 

* <span data-ttu-id="62cb7-112">**_PFX _ [CertName] Certificate_ [CodePackageName]**</span><span class="sxs-lookup"><span data-stu-id="62cb7-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="62cb7-113">**_Hasło _ [CertName] Certificate_ [CodePackageName]**</span><span class="sxs-lookup"><span data-stu-id="62cb7-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="62cb7-114">Usługa kontenera lub proces jest odpowiedzialny za zaimportować plik PFX do kontenera.</span><span class="sxs-lookup"><span data-stu-id="62cb7-114">The container service or process is responsible for importing the PFX file into the container.</span></span> <span data-ttu-id="62cb7-115">Aby zaimportować certyfikat, można użyć `setupentrypoint.sh` skrypty lub wykonania kodu niestandardowego, w ramach procesu kontenera.</span><span class="sxs-lookup"><span data-stu-id="62cb7-115">To import the certificate, you can use `setupentrypoint.sh` scripts or executed custom code within the container process.</span></span> <span data-ttu-id="62cb7-116">Następujący przykładowy kod w języku C# do importowania plików PFX:</span><span class="sxs-lookup"><span data-stu-id="62cb7-116">Sample code in C# for importing the PFX file follows:</span></span>

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
<span data-ttu-id="62cb7-117">Ten certyfikat PFX mogą służyć do uwierzytelniania aplikacji lub usługi lub bezpiecznego commmunication z innymi usługami.</span><span class="sxs-lookup"><span data-stu-id="62cb7-117">This PFX certificate can be used for authenticate the application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="62cb7-118">Skonfiguruj grupę dla kontenerów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="62cb7-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="62cb7-119">Aby skonfigurować usługi zarządzane przez grupę (grupa zarządzanych kont usług), plik specyfikacji poświadczeń (`credspec`) znajduje się we wszystkich węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="62cb7-119">To set up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in the cluster.</span></span> <span data-ttu-id="62cb7-120">We wszystkich węzłach za pomocą rozszerzenia maszyny Wirtualnej można skopiować pliku.</span><span class="sxs-lookup"><span data-stu-id="62cb7-120">The file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="62cb7-121">`credspec` Plik musi zawierać informacje o koncie gMSA.</span><span class="sxs-lookup"><span data-stu-id="62cb7-121">The `credspec` file must contain the gMSA account information.</span></span> <span data-ttu-id="62cb7-122">Aby uzyskać więcej informacji na temat `credspec` plików, zobacz [kont usług](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="62cb7-122">For more information on the `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="62cb7-123">Specyfikacja poświadczeń i `Hostname` tag są określone w manifeście aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62cb7-123">The credential specification and the `Hostname` tag are specified in the application manifest.</span></span> <span data-ttu-id="62cb7-124">`Hostname` Tag musi odpowiadać nazwie konta gMSA działającą w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="62cb7-124">The `Hostname` tag must match the gMSA account name that the container runs under.</span></span>  <span data-ttu-id="62cb7-125">`Hostname` Tagu umożliwia kontenera do samodzielnego uwierzytelnienia w innych usługach w domenie przy użyciu uwierzytelniania Kerberos.</span><span class="sxs-lookup"><span data-stu-id="62cb7-125">The `Hostname` tag allows the container to authenticate itself to other services in the domain using Kerberos authentication.</span></span>  <span data-ttu-id="62cb7-126">Przykładowy służący do określania `Hostname` i `credspec` w aplikacji manifestu jest wyświetlany w następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="62cb7-126">A sample for specifying the `Hostname` and the `credspec` in the application manifest is shown in the following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="62cb7-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62cb7-127">Next steps</span></span>

* [<span data-ttu-id="62cb7-128">Wdrażanie kontenera systemu Windows w sieci szkieletowej usług w systemie Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="62cb7-128">Deploy a Windows container to Service Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="62cb7-129">Wdrażanie kontenera Docker sieci szkieletowej usług w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="62cb7-129">Deploy a Docker container to Service Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
