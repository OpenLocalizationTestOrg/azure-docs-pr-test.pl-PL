---
title: "Tworzenie kolekcji hybrydowej usługi RemoteApp aaaTroubleshoot | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak błędy tworzenia kolekcji tootroubleshoot RemoteApp hybrydowego"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="8884e-103">Rozwiązywanie problemów związanych z tworzeniem kolekcji hybrydowych Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8884e-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8884e-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8884e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8884e-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="8884e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8884e-106">Kolekcja hybrydowa znajduje się w i przechowuje dane w hello chmury Azure, ale również umożliwia użytkownikom dostęp do danych i zasobów przechowywanych w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="8884e-106">A hybrid collection is hosted in and stores data in hello Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="8884e-107">Użytkownicy mogą uzyskiwać dostęp do aplikacji, logując się przy użyciu poświadczeń firmowych synchronizowanych lub sfederowanych z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8884e-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="8884e-108">Można wdrażać kolekcję hybrydową, który korzysta z istniejącej sieci wirtualnej Azure, lub można utworzyć nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8884e-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="8884e-109">Zaleca się tworzenia lub za pomocą podsieci sieci wirtualnej wystarczająco duży zakres CIDR oczekiwany przyszły wzrost usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8884e-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="8884e-110">Nie utworzono jeszcze kolekcji?</span><span class="sxs-lookup"><span data-stu-id="8884e-110">Haven't created your collection yet?</span></span> <span data-ttu-id="8884e-111">Zobacz [tworzenie kolekcji hybrydowej](remoteapp-create-hybrid-deployment.md) hello czynności.</span><span class="sxs-lookup"><span data-stu-id="8884e-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for hello steps.</span></span>

<span data-ttu-id="8884e-112">Jeśli występują problemy podczas tworzenia kolekcji, lub jeśli hello kolekcji nie działa, sposób hello podejrzewasz, że należy, zapoznaj się z następujących informacji hello.</span><span class="sxs-lookup"><span data-stu-id="8884e-112">If you are having trouble creating your collection, or if hello collection isn't working hello way you think it should, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="8884e-113">Obraz jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="8884e-113">Your image is invalid</span></span>
<span data-ttu-id="8884e-114">Jeśli zostanie wyświetlony komunikat, takie jak "GoldImageInvalid" podczas oczekiwania dla usługi Azure tooprovision kolekcji, oznacza to, że obraz szablonu nie spełnia wymagań hello [określone wymagania dotyczące obrazu](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="8884e-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="8884e-115">Tak, przejdź do odczytu tych [wymagania](remoteapp-imagereqs.md), Usuń obraz i spróbuj toocreate kolekcji ponownie.</span><span class="sxs-lookup"><span data-stu-id="8884e-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="8884e-116">SIECI wirtualnej ma zdefiniowane grup zabezpieczeń sieci?</span><span class="sxs-lookup"><span data-stu-id="8884e-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="8884e-117">Jeśli masz zdefiniowane w podsieci hello używasz kolekcji grup zabezpieczeń sieci, upewnij się, te [adresów URL i portów](remoteapp-ports.md) jest dostępny w obrębie podsieci.</span><span class="sxs-lookup"><span data-stu-id="8884e-117">If you have network security groups defined on hello subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="8884e-118">Możesz dodać dodatkowe sieci zabezpieczeń grupy toohello maszyn wirtualnych wdrożonych przez użytkownika w podsieci hello zwiększenie poziomu kontrolki.</span><span class="sxs-lookup"><span data-stu-id="8884e-118">You can add additional network security groups toohello VMs deployed by you in hello subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="8884e-119">Używasz serwery DNS?</span><span class="sxs-lookup"><span data-stu-id="8884e-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="8884e-120">I są one dostępne z podsieć sieci Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="8884e-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="8884e-121">Masz toomake powitalne się, że serwery DNS w sieci wirtualnej są zawsze włączone i zawsze możliwe tooresolve maszyn wirtualnych dla hello hostowanych w hello sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8884e-121">You have toomake sure hello DNS servers in your VNET are always up and always able tooresolve hello virtual machines hosted in hello VNET.</span></span> <span data-ttu-id="8884e-122">Nie należy używać w tym Google DNS.</span><span class="sxs-lookup"><span data-stu-id="8884e-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="8884e-123">Dla kolekcji hybrydowych należy używać serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="8884e-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="8884e-124">Możesz je określić w schemat konfiguracji sieci lub za pośrednictwem portalu zarządzania powitania po utworzeniu sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8884e-124">You specify them in your network configuration schema or through hello management portal when you create your virtual network.</span></span> <span data-ttu-id="8884e-125">Serwery DNS używane w kolejności hello, że są one określone w czasie pracy awaryjnej (jak działania okrężnego min. tooround).</span><span class="sxs-lookup"><span data-stu-id="8884e-125">DNS servers are used in hello order that they are specified in a failover manner (as opposed tooround robin).</span></span>  
<span data-ttu-id="8884e-126">Zobacz zbyt[rozpoznawanie nazwy dla maszyn wirtualnych i wystąpień roli](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake się, że serwery DNS są skonfigurowane correcly.</span><span class="sxs-lookup"><span data-stu-id="8884e-126">Please refer too[Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="8884e-127">Upewnij się, że serwery DNS hello kolekcji są dostępne z podsiecią sieci Wirtualnej hello, określone dla tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="8884e-127">Make sure hello DNS servers for your collection are accessible and available from hello VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="8884e-128">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="8884e-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Zdefiniuj serwery DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="8884e-130">W kolekcji jest używany kontroler domeny usługi Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8884e-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="8884e-131">Obecnie tylko do jednej domeny usługi Active Directory może być skojarzony z usługą Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8884e-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="8884e-132">Kolekcja hybrydowa Hello obsługuje tylko konta usługi Azure Active Directory, które zostały zsynchronizowane przy użyciu narzędzia DirSync z wdrożenia usługi Active Directory systemu Windows Server; w szczególności albo zsynchronizowane z opcją synchronizacji haseł hello synchronizowane ze skonfigurowaną Federacją usług federacyjnych Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="8884e-132">hello hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with hello Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="8884e-133">Należy toocreate domeny niestandardowej, która odpowiada hello sufiks domeny nazwy UPN w domenie lokalnej i konfigurowania integracji katalogu.</span><span class="sxs-lookup"><span data-stu-id="8884e-133">You need toocreate a custom domain that matches hello UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="8884e-134">Zobacz [Konfigurowanie usługi Active Directory dla usługi Azure RemoteApp](remoteapp-ad.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="8884e-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="8884e-135">Upewnij się, podane szczegóły domeny hello są prawidłowe i hello kontroler domeny jest dostępny z powitalne maszyny Wirtualnej utworzonej w hello podsieć używana na potrzeby usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8884e-135">Make sure hello domain details provided are valid and hello domain controller is reachable from hello VM created in hello subnet used for Azure Remote App.</span></span> <span data-ttu-id="8884e-136">Upewnij się, że konto usługi hello się, że podane poświadczenia mają uprawnienia tooadd komputery toohello pod warunkiem domeny i że hello nazwa usługi AD, pod warunkiem, mogą zostać rozwiązane z hello DNS podany w hello sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8884e-136">Also make sure hello service account credentials supplied have permissions tooadd computers toohello provided domain and that hello AD name provided can be resolved from hello DNS provided in hello VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="8884e-137">Jakie nazwy domeny czy określono podczas tworzenia Twojej kolekcji?</span><span class="sxs-lookup"><span data-stu-id="8884e-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="8884e-138">Nazwa domeny Hello utworzone lub dodane musi być nazwą domeny wewnętrznej (nie nazwę domeny usługi Azure AD) i musi być w rozpoznawalnym formacie DNS (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="8884e-138">hello domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="8884e-139">Na przykład masz wewnętrzna nazwa usługi Active Directory (contoso.local) i Active Directory głównej nazwy użytkownika (contoso.com) - masz toouse hello wewnętrzna nazwa podczas tworzenia Twojej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="8884e-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have toouse hello internal name when you create your collection.</span></span>

