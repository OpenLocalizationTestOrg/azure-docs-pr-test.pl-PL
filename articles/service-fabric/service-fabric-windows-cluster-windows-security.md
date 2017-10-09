---
title: "aaaSecure a klastra z systemem Windows przy użyciu zabezpieczeń systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure węzła do węzła i węzeł klient zabezpieczeń w autonomicznym klastra z systemem w systemie Windows przy użyciu zabezpieczeń systemu Windows."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="da014-103">Zabezpieczanie klastra autonomicznego w systemie Windows przy użyciu zabezpieczeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="da014-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="da014-104">tooprevent nieautoryzowany klastra usługi sieć szkieletowa tooa dostępu, należy zabezpieczyć hello klastra.</span><span class="sxs-lookup"><span data-stu-id="da014-104">tooprevent unauthorized access tooa Service Fabric cluster, you must secure hello cluster.</span></span> <span data-ttu-id="da014-105">Bezpieczeństwa jest szczególnie ważne, uruchomienie klastra hello obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="da014-105">Security is especially important when hello cluster runs production workloads.</span></span> <span data-ttu-id="da014-106">W tym artykule opisano sposób tooconfigure węzła do węzła i węzeł klient zabezpieczeń przy użyciu zabezpieczeń systemu Windows w hello *pliku ClusterConfig.JSON* pliku.</span><span class="sxs-lookup"><span data-stu-id="da014-106">This article describes how tooconfigure node-to-node and client-to-node security by using Windows security in hello *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="da014-107">proces Hello odpowiada toohello skonfigurować zabezpieczenia krok [tworzenia autonomicznych klastra z systemem Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="da014-107">hello process corresponds toohello configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="da014-108">Aby uzyskać więcej informacji o używaniu sieci szkieletowej usług zabezpieczeń systemu Windows, temacie [klastra scenariusze zabezpieczeń](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="da014-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="da014-109">Należy zastanów wybór hello zabezpieczeń węzła do węzła, ponieważ nie istnieje żadne Uaktualnianie klastra z jednym tooanother wybór zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="da014-109">You should consider hello selection of node-to-node security carefully because there is no cluster upgrade from one security choice tooanother.</span></span> <span data-ttu-id="da014-110">Wybór zabezpieczeń hello toochange, masz toorebuild hello pełne klastra.</span><span class="sxs-lookup"><span data-stu-id="da014-110">toochange hello security selection, you have toorebuild hello full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="da014-111">Konfigurowanie zabezpieczeń systemu Windows przy użyciu usługi zarządzane przez grupę</span><span class="sxs-lookup"><span data-stu-id="da014-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="da014-112">przykład Witaj *ClusterConfig.gMSA.Windows.MultiMachine.JSON* pliku konfiguracji są pobierane z hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) pakiet klastra autonomiczny zawiera szablon do konfigurowania systemu Windows zabezpieczeń za pomocą [konta usług zarządzanych grupy (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="da014-112">hello sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| <span data-ttu-id="da014-113">**Ustawienie konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="da014-113">**Configuration Setting**</span></span> | <span data-ttu-id="da014-114">**Opis**</span><span class="sxs-lookup"><span data-stu-id="da014-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="da014-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="da014-115">WindowsIdentities</span></span> |<span data-ttu-id="da014-116">Zawiera hello tożsamości klastra i klienta.</span><span class="sxs-lookup"><span data-stu-id="da014-116">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="da014-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="da014-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="da014-118">Konfiguruje zabezpieczeń węzła do węzła.</span><span class="sxs-lookup"><span data-stu-id="da014-118">Configures node-to-node security.</span></span> <span data-ttu-id="da014-119">Konto usługi zarządzane przez grupę.</span><span class="sxs-lookup"><span data-stu-id="da014-119">A group managed service account.</span></span> |  
| <span data-ttu-id="da014-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="da014-120">ClusterSPN</span></span> |<span data-ttu-id="da014-121">Pełni kwalifikowaną nazwę SPN konta gMSA</span><span class="sxs-lookup"><span data-stu-id="da014-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="da014-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="da014-122">ClientIdentities</span></span> |<span data-ttu-id="da014-123">Konfiguruje zabezpieczeń węzeł klienta.</span><span class="sxs-lookup"><span data-stu-id="da014-123">Configures client-to-node security.</span></span> <span data-ttu-id="da014-124">Tablica konta użytkownika klienta.</span><span class="sxs-lookup"><span data-stu-id="da014-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="da014-125">Tożsamość</span><span class="sxs-lookup"><span data-stu-id="da014-125">Identity</span></span> |<span data-ttu-id="da014-126">powitania klienta tożsamości, użytkownika domeny.</span><span class="sxs-lookup"><span data-stu-id="da014-126">hello client identity, a domain user.</span></span> |  
| <span data-ttu-id="da014-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="da014-127">IsAdmin</span></span> |<span data-ttu-id="da014-128">Wartość TRUE oznacza hello domeny, które użytkownik ma uprawnienia dostępu administratora klienta, wartość false dla dostępu klientów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="da014-128">True specifies that hello domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="da014-129">[Węzeł toonode zabezpieczeń](service-fabric-cluster-security.md#node-to-node-security) skonfigurowano ustawienie **ClustergMSAIdentity** gdy sieć szkieletowa usług musi toorun mocy przez grupę.</span><span class="sxs-lookup"><span data-stu-id="da014-129">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs toorun under gMSA.</span></span> <span data-ttu-id="da014-130">W kolejności toobuild relacje zaufania między węzłami ich należy pamiętać o sobie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="da014-130">In order toobuild trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="da014-131">Można to zrobić na dwa sposoby: można określić konta usługi zarządzanego grupy obejmującą wszystkie węzły w klastrze hello hello lub hello domeny grupy na komputerze, który zawiera wszystkie węzły w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="da014-131">This can be accomplished in two different ways: Specify hello Group Managed Service Account that includes all nodes in hello cluster or Specify hello domain machine group that includes all nodes in hello cluster.</span></span> <span data-ttu-id="da014-132">Zdecydowanie zaleca się używanie hello [konta usług zarządzanych grupy (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) podejście, szczególnie w przypadku dużych klastrów (więcej niż 10 węzłów) lub klastrów, które są prawdopodobnie toogrow lub zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="da014-132">We strongly recommend using hello [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely toogrow or shrink.</span></span>  
<span data-ttu-id="da014-133">To rozwiązanie nie wymaga hello tworzenia grupy domeny, dla której administratorzy klastra przyznano tooadd prawa dostępu i Usuń członków.</span><span class="sxs-lookup"><span data-stu-id="da014-133">This approach does not require hello creation of a domain group for which cluster administrators have been granted access rights tooadd and remove members.</span></span> <span data-ttu-id="da014-134">Te konta są również przydatne w przypadku automatyczne zarządzanie hasłami.</span><span class="sxs-lookup"><span data-stu-id="da014-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="da014-135">Aby uzyskać więcej informacji, zobacz [wprowadzenie do kont usług zarządzanych grupy](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="da014-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="da014-136">[Klient toonode zabezpieczeń](service-fabric-cluster-security.md#client-to-node-security) jest konfigurowana przy użyciu **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="da014-136">[Client toonode security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="da014-137">W kolejności tooestablish relacji zaufania między klienta i hello klastra należy skonfigurować tooknow klastra hello które tożsamości klienta, które on zaufany.</span><span class="sxs-lookup"><span data-stu-id="da014-137">In order tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow which client identities that it can trust.</span></span> <span data-ttu-id="da014-138">Można to zrobić na dwa sposoby: Określ hello domeny grupy użytkowników, którzy się połączyć lub określ hello użytkownicy węzeł domeny, które mogą nawiązywać połączenia.</span><span class="sxs-lookup"><span data-stu-id="da014-138">This can be done in two different ways: Specify hello domain group users that can connect or specify hello domain node users that can connect.</span></span> <span data-ttu-id="da014-139">Sieć szkieletowa usług obsługuje dwa typy kontroli różny dostęp dla klientów, które są połączone tooa klastra sieci szkieletowej usług: administratora i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="da014-139">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="da014-140">Kontrola dostępu umożliwia określenie hello dla hello typy toolimit administratora klastra toocertain dostępu do operacji klastra dla różnych grup użytkowników, co klaster hello bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="da014-140">Access control provides hello ability for hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, making hello cluster more secure.</span></span>  <span data-ttu-id="da014-141">Administratorzy mają pełny dostęp toomanagement możliwości (w tym możliwości odczytu/zapisu).</span><span class="sxs-lookup"><span data-stu-id="da014-141">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="da014-142">Użytkownicy mają domyślnie tylko możliwości toomanagement dostęp do odczytu (na przykład możliwość wykonywania kwerend), a hello możliwości tooresolve aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="da014-142">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span> <span data-ttu-id="da014-143">Aby uzyskać więcej informacji dotyczących kontroli dostępu, zobacz [kontrola dostępu oparta na rolach dla klientów usługi sieć szkieletowa](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="da014-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="da014-144">Witaj następujący przykład **zabezpieczeń** sekcji konfiguruje zabezpieczenia systemu Windows przy użyciu usługi zarządzane przez grupę i określa, że hello maszyn w *ServiceFabric.clusterA.contoso.com* gMSA są częścią klastra hello oraz że *CONTOSO\usera* ma dostęp klient administratora:</span><span class="sxs-lookup"><span data-stu-id="da014-144">hello following example **security** section configures Windows security using gMSA and specifies that hello machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of hello cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="da014-145">Konfigurowanie zabezpieczeń systemu Windows przy użyciu grupy na komputerze</span><span class="sxs-lookup"><span data-stu-id="da014-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="da014-146">przykład Witaj *ClusterConfig.Windows.MultiMachine.JSON* pliku konfiguracji są pobierane z hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) pakiet klastra autonomiczny zawiera szablon do konfigurowania zabezpieczeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="da014-146">hello sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="da014-147">Zabezpieczenia systemu Windows jest skonfigurowany w hello **właściwości** sekcji:</span><span class="sxs-lookup"><span data-stu-id="da014-147">Windows security is configured in hello **Properties** section:</span></span> 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| <span data-ttu-id="da014-148">**Ustawienie konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="da014-148">**Configuration setting**</span></span> | <span data-ttu-id="da014-149">**Opis**</span><span class="sxs-lookup"><span data-stu-id="da014-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="da014-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="da014-150">ClusterCredentialType</span></span> |<span data-ttu-id="da014-151">**ClusterCredentialType** ustawiono zbyt*Windows* Jeśli ClusterIdentity określa nazwa grupy komputera usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da014-151">**ClusterCredentialType** is set too*Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="da014-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="da014-152">ServerCredentialType</span></span> |<span data-ttu-id="da014-153">Ustaw zbyt*Windows* tooenable zabezpieczenia systemu Windows dla klientów.</span><span class="sxs-lookup"><span data-stu-id="da014-153">Set too*Windows* tooenable Windows security for clients.</span></span><br /><br /><span data-ttu-id="da014-154">Oznacza to, że klienci hello hello klastra i hello samego klastra są uruchomione w ramach domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da014-154">This indicates that hello clients of hello cluster and hello cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="da014-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="da014-155">WindowsIdentities</span></span> |<span data-ttu-id="da014-156">Zawiera hello tożsamości klastra i klienta.</span><span class="sxs-lookup"><span data-stu-id="da014-156">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="da014-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="da014-157">ClusterIdentity</span></span> |<span data-ttu-id="da014-158">Użyj nazwy grupy komputera, domain\machinegroup, tooconfigure zabezpieczeń węzła do węzła.</span><span class="sxs-lookup"><span data-stu-id="da014-158">Use a machine group name, domain\machinegroup, tooconfigure node-to-node security.</span></span> |  
| <span data-ttu-id="da014-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="da014-159">ClientIdentities</span></span> |<span data-ttu-id="da014-160">Konfiguruje zabezpieczeń węzeł klienta.</span><span class="sxs-lookup"><span data-stu-id="da014-160">Configures client-to-node security.</span></span> <span data-ttu-id="da014-161">Tablica konta użytkownika klienta.</span><span class="sxs-lookup"><span data-stu-id="da014-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="da014-162">Tożsamość</span><span class="sxs-lookup"><span data-stu-id="da014-162">Identity</span></span> |<span data-ttu-id="da014-163">Dodaj hello domeny użytkownika, domena azwa_użytkownika powitania klienta tożsamości.</span><span class="sxs-lookup"><span data-stu-id="da014-163">Add hello domain user, domain\username, for hello client identity.</span></span> |  
| <span data-ttu-id="da014-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="da014-164">IsAdmin</span></span> |<span data-ttu-id="da014-165">Toospecify tootrue zestawu, który hello użytkownika domeny ma dostęp administratora klienta lub false dla dostępu klientów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="da014-165">Set tootrue toospecify that hello domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="da014-166">[Węzeł zabezpieczenia toonode](service-fabric-cluster-security.md#node-to-node-security) jest konfigurowana przy użyciu ustawienia **ClusterIdentity** Jeśli chcesz toouse grupy na komputerze w ramach domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da014-166">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want toouse a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="da014-167">Aby uzyskać więcej informacji, zobacz [Utwórz grupę maszyny w usłudze Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span><span class="sxs-lookup"><span data-stu-id="da014-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="da014-168">[Węzeł Klient zabezpieczeń](service-fabric-cluster-security.md#client-to-node-security) jest konfigurowana przy użyciu **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="da014-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="da014-169">tooestablish zaufania między klastrem klienta i hello, musisz skonfigurować hello klastra tooknow powitania klienta tożsamości, które hello klastra można ufać.</span><span class="sxs-lookup"><span data-stu-id="da014-169">tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow hello client identities that hello cluster can trust.</span></span> <span data-ttu-id="da014-170">Można ustanowić relacji zaufania na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="da014-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="da014-171">Określ hello domeny grupy użytkowników, które mogą nawiązywać połączenia.</span><span class="sxs-lookup"><span data-stu-id="da014-171">Specify hello domain group users that can connect.</span></span>
- <span data-ttu-id="da014-172">Określ hello domeny węzła Użytkownicy mogą łączyć.</span><span class="sxs-lookup"><span data-stu-id="da014-172">Specify hello domain node users that can connect.</span></span>

<span data-ttu-id="da014-173">Sieć szkieletowa usług obsługuje dwa typy kontroli różny dostęp dla klientów, które są połączone tooa klastra sieci szkieletowej usług: administratora i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="da014-173">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="da014-174">Kontrola dostępu umożliwia hello klastra administrator toolimit toocertain typy dostępu operacji klastra dla różnych grup użytkowników, co czyni klastra hello bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="da014-174">Access control enables hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, which makes hello cluster more secure.</span></span>  <span data-ttu-id="da014-175">Administratorzy mają pełny dostęp toomanagement możliwości (w tym możliwości odczytu/zapisu).</span><span class="sxs-lookup"><span data-stu-id="da014-175">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="da014-176">Użytkownicy mają domyślnie tylko możliwości toomanagement dostęp do odczytu (na przykład możliwość wykonywania kwerend), a hello możliwości tooresolve aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="da014-176">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span>  

<span data-ttu-id="da014-177">Witaj następujący przykład **zabezpieczeń** konfiguruje zabezpieczenia systemu Windows, określa, że hello maszyn w sekcji *ServiceFabric/clusterA.contoso.com* są częścią klastra hello i określa, że  *CONTOSO\usera* ma dostęp klient administratora:</span><span class="sxs-lookup"><span data-stu-id="da014-177">hello following example **security** section configures Windows security, specifies that hello machines in *ServiceFabric/clusterA.contoso.com* are part of hello cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> <span data-ttu-id="da014-178">Sieć szkieletowa usług nie powinny zostać wdrożone na kontrolerze domeny.</span><span class="sxs-lookup"><span data-stu-id="da014-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="da014-179">Upewnij się, że pliku ClusterConfig.json nie zawierają hello adres IP kontrolera domeny hello, korzystając z grupy na komputerze lub konta grupy usługi zarządzanej (gMSA).</span><span class="sxs-lookup"><span data-stu-id="da014-179">Make sure that ClusterConfig.json does not include hello IP address of hello domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="da014-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da014-180">Next steps</span></span>
<span data-ttu-id="da014-181">Po skonfigurowaniu zabezpieczeń systemu Windows w hello *pliku ClusterConfig.JSON* plików, wznowić hello procesu tworzenia klastra w [tworzenia autonomicznych klastra z systemem Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="da014-181">After configuring Windows security in hello *ClusterConfig.JSON* file, resume hello cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="da014-182">Aby uzyskać więcej informacji na temat sposobu węzeł węzeł zabezpieczeń, węzeł klient zabezpieczeń i kontroli dostępu opartej na rolach, zobacz [klastra scenariusze zabezpieczeń](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="da014-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="da014-183">Zobacz [klastra bezpiecznego połączenia tooa](service-fabric-connect-to-secure-cluster.md) przykłady połączenie przy użyciu programu PowerShell lub klienta fabricclient z rolą.</span><span class="sxs-lookup"><span data-stu-id="da014-183">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
