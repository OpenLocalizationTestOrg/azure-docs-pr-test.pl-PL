---
title: "Azure Active Directory Domain Services: Aktualizowanie ustawień DNS dla sieci wirtualnej platformy Azure hello | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="4b782-103">Aktualizowanie ustawień DNS dla hello sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4b782-103">Update DNS settings for hello Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="4b782-104">Zadanie 4: Aktualizowanie ustawień DNS na potrzeby hello sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4b782-104">Task 4: Update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="4b782-105">W hello poprzedzających zadania konfiguracji została pomyślnie włączona Azure Active Directory Domain Services dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="4b782-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="4b782-106">następne zadanie Hello jest tooensure, że komputery w sieci wirtualnej hello łączyć i korzystanie z tych usług.</span><span class="sxs-lookup"><span data-stu-id="4b782-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="4b782-107">W tym artykule należy zaktualizować ustawienia serwera DNS hello sieci wirtualnej toopoint toohello dwa adresy IP gdzie usług domenowych Azure Active Directory jest dostępny w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="4b782-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="4b782-108">Po włączeniu usługi Azure Active Directory Domain Services dla katalogu hello Uwaga hello adresów IP dla usługi Azure Active Directory Domain Services, które są wyświetlane na powitania **Konfiguruj** katalogu.</span><span class="sxs-lookup"><span data-stu-id="4b782-108">After you've enabled Azure Active Directory Domain Services for hello directory, note hello IP addresses for Azure Active Directory Domain Services that are displayed on hello **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="4b782-109">tooupdate hello ustawienia serwera DNS dla sieci wirtualnej hello, w której włączono usługi Azure Active Directory Domain Services, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4b782-109">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="4b782-110">Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4b782-110">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4b782-111">Wybierz w okienku po lewej stronie powitania **sieci**.</span><span class="sxs-lookup"><span data-stu-id="4b782-111">In hello left pane, select **Networks**.</span></span>  
    <span data-ttu-id="4b782-112">Witaj **sieci** zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="4b782-112">hello **Networks** window opens.</span></span>

    ![Okno Sieci wirtualne](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="4b782-114">Na powitania **sieci wirtualnych** kartę, zaznacz hello sieci wirtualnej, w której włączono usługi Azure Active Directory Domain Services tooview jego właściwości.</span><span class="sxs-lookup"><span data-stu-id="4b782-114">On hello **Virtual Networks** tab, select hello virtual network in which you enabled Azure Active Directory Domain Services tooview its properties.</span></span>
4. <span data-ttu-id="4b782-115">Kliknij przycisk hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="4b782-115">Click hello **Configure** tab.</span></span>

    ![Okno Sieci wirtualne](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="4b782-117">W hello **serwerów DNS** wprowadź zarówno hello adresów IP, które były wyświetlane w hello **usług domenowych w usłudze** sekcji na powitania **Konfiguruj** katalogu.</span><span class="sxs-lookup"><span data-stu-id="4b782-117">In hello **DNS servers** section, enter both of hello IP addresses that were displayed in hello **Domain Services** section on hello **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="4b782-118">Kliknij przycisk Ustawienia serwera DNS hello toosave tej sieci wirtualnej, w okienku zadań hello u dołu okna hello hello **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="4b782-118">toosave hello DNS server settings for this virtual network, in hello task pane at hello bottom of hello window, click **Save**.</span></span>

   ![Zaktualizuj ustawienia serwera DNS hello hello sieci wirtualnej](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="4b782-120">Maszyny wirtualne w sieci hello pobierają tylko nowe ustawienia DNS powitania po ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="4b782-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="4b782-121">Jeśli potrzebne ustawienia DNS tooget hello zaktualizowane od razu, wyzwolić ponowne uruchomienie komputera przez hello portal, programu PowerShell lub hello interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4b782-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4b782-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4b782-122">Next steps</span></span>
<span data-ttu-id="4b782-123">Zadanie 5: [włączyć tooAzure synchronizacji haseł usług domenowych w usłudze Active Directory](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="4b782-123">Task 5: [Enable password synchronization tooAzure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
