---
title: "Azure Active Directory Domain Services: Aktualizowanie ustawień DNS na potrzeby sieci wirtualnej platformy Azure | Microsoft Docs"
description: "Wprowadzenie do usługi Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 8bee2a25f196d645b27f30f21305b1550e44e07a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="f8241-103">Aktualizowanie ustawień DNS dla sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f8241-103">Update DNS settings for the Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="f8241-104">Zadanie 4. Aktualizowanie ustawień DNS dla sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f8241-104">Task 4: Update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="f8241-105">W poprzednich zadaniach konfiguracji pomyślnie włączono usługi Azure Active Directory Domain Services dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="f8241-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="f8241-106">Następnym krokiem jest zapewnienie komputerom w sieci wirtualnej możliwości łączenia się z tymi usługami i korzystania z nich.</span><span class="sxs-lookup"><span data-stu-id="f8241-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="f8241-107">W tym artykule zaktualizujesz ustawienia serwera DNS dla sieci wirtualnej, wskazując dwa adresy IP, pod którymi usługi Azure Active Directory Domain Services są dostępne w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f8241-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="f8241-108">Po włączeniu usług Azure Active Directory Domain Services dla katalogu zanotuj ich adresy IP wyświetlane na karcie **Konfigurowanie** katalogu.</span><span class="sxs-lookup"><span data-stu-id="f8241-108">After you've enabled Azure Active Directory Domain Services for the directory, note the IP addresses for Azure Active Directory Domain Services that are displayed on the **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="f8241-109">Wykonaj poniższe kroki, aby zaktualizować ustawienia serwera DNS dla sieci wirtualnej, w której włączono usługi Azure Active Directory Domain Services:</span><span class="sxs-lookup"><span data-stu-id="f8241-109">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="f8241-110">Przejdź do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f8241-110">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f8241-111">W lewym okienku wybierz opcję **Sieci**.</span><span class="sxs-lookup"><span data-stu-id="f8241-111">In the left pane, select **Networks**.</span></span>  
    <span data-ttu-id="f8241-112">Zostanie otwarte okno **Sieci**.</span><span class="sxs-lookup"><span data-stu-id="f8241-112">The **Networks** window opens.</span></span>

    ![Okno Sieci wirtualne](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="f8241-114">Na karcie **Sieci wirtualne** wybierz sieć wirtualną, w której włączono usługi Azure Active Directory Domain Services, aby wyświetlić jej właściwości.</span><span class="sxs-lookup"><span data-stu-id="f8241-114">On the **Virtual Networks** tab, select the virtual network in which you enabled Azure Active Directory Domain Services to view its properties.</span></span>
4. <span data-ttu-id="f8241-115">Kliknij kartę **Konfiguracja**.</span><span class="sxs-lookup"><span data-stu-id="f8241-115">Click the **Configure** tab.</span></span>

    ![Okno Sieci wirtualne](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="f8241-117">W sekcji **Serwery DNS** wprowadź obydwa adresy IP wyświetlane w sekcji **Usługi domenowe** na karcie **Konfigurowanie** katalogu.</span><span class="sxs-lookup"><span data-stu-id="f8241-117">In the **DNS servers** section, enter both of the IP addresses that were displayed in the **Domain Services** section on the **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="f8241-118">Aby zapisać ustawienia serwera DNS tej sieci wirtualnej, kliknij pozycję **Zapisz** w okienku zadań w dolnej części okna.</span><span class="sxs-lookup"><span data-stu-id="f8241-118">To save the DNS server settings for this virtual network, in the task pane at the bottom of the window, click **Save**.</span></span>

   ![Aktualizowanie ustawień serwera DNS dla sieci wirtualnej](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="f8241-120">Maszyny wirtualne w sieci otrzymują nowe ustawienia DNS dopiero po ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="f8241-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="f8241-121">Jeśli chcesz, aby od razu miały zaktualizowane ustawienia usługi DNS, wyzwól ich ponowne uruchomienie przez portal, program PowerShell lub interfejs wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f8241-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f8241-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f8241-122">Next steps</span></span>
<span data-ttu-id="f8241-123">Zadanie 5. [Włączanie synchronizacji haseł w usługach Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="f8241-123">Task 5: [Enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
