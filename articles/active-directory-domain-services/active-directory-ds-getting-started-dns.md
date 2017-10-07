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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="d481a-103">Włączanie usług Azure Active Directory Domain Services (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d481a-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="d481a-104">Zadanie 4: aktualizowanie ustawień DNS na potrzeby hello sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d481a-104">Task 4: update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="d481a-105">W hello poprzedzających zadania konfiguracji została pomyślnie włączona Azure Active Directory Domain Services dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="d481a-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="d481a-106">następne zadanie Hello jest tooensure, że komputery w sieci wirtualnej hello łączyć i korzystanie z tych usług.</span><span class="sxs-lookup"><span data-stu-id="d481a-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="d481a-107">W tym artykule należy zaktualizować ustawienia serwera DNS hello sieci wirtualnej toopoint toohello dwa adresy IP gdzie usług domenowych Azure Active Directory jest dostępny w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="d481a-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

<span data-ttu-id="d481a-108">tooupdate hello ustawienia serwera DNS dla sieci wirtualnej hello, w której włączono usługi Azure Active Directory Domain Services, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d481a-108">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="d481a-109">Witaj **omówienie** karta zawiera zestaw **wymagane kroki konfiguracji** toobe wykonać po domeny zarządzanej jest w pełni zaaprowizowanym.</span><span class="sxs-lookup"><span data-stu-id="d481a-109">hello **Overview** tab lists a set of **Required configuration steps** toobe performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="d481a-110">pierwszym krokiem konfiguracji Hello jest **ustawienia serwera DNS aktualizacji dla sieci wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="d481a-110">hello first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Usługi Domain Services — karta Przegląd po pełnej aprowizacji](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="d481a-112">Gdy domena zostanie w pełni zaaprowizowana, na tym kafelku będą wyświetlane dwa adresy IP.</span><span class="sxs-lookup"><span data-stu-id="d481a-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="d481a-113">Każdy z tych adresów IP reprezentuje kontroler domeny dla domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="d481a-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="d481a-114">pierwszy adres IP toocopy hello tooclipboard adresów, kliknij przycisk hello kopiowania przycisku Dalej tooit.</span><span class="sxs-lookup"><span data-stu-id="d481a-114">toocopy hello first IP address tooclipboard, click hello copy button next tooit.</span></span> <span data-ttu-id="d481a-115">Następnie kliknij przycisk hello **serwerów DNS skonfigurować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d481a-115">Then click hello **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="d481a-116">Wklej hello pierwszego adresu IP do hello **serwer DNS dodać** textbox w hello **serwerów DNS** bloku.</span><span class="sxs-lookup"><span data-stu-id="d481a-116">Paste hello first IP address into hello **Add DNS server** textbox in hello **DNS servers** blade.</span></span> <span data-ttu-id="d481a-117">Przewijane w poziomie toohello toocopy hello drugiego adresu IP w lewo i wklej go do hello **serwera DNS Dodaj** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d481a-117">Scroll horizontally toohello left toocopy hello second IP address and paste it into hello **Add DNS server** textbox.</span></span>

    ![Usługi Domain Services — aktualizacja usługi DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="d481a-119">Kliknij przycisk **zapisać** po zakończeniu serwerów DNS hello tooupdate hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d481a-119">Click **Save** when you are done tooupdate hello DNS servers for hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="d481a-120">Maszyny wirtualne w sieci hello pobierają tylko nowe ustawienia DNS powitania po ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="d481a-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="d481a-121">Jeśli potrzebne ustawienia DNS tooget hello zaktualizowane od razu, wyzwolić ponowne uruchomienie komputera przez hello portal, programu PowerShell lub hello interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d481a-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="d481a-122">Następny krok</span><span class="sxs-lookup"><span data-stu-id="d481a-122">Next step</span></span>
[<span data-ttu-id="d481a-123">Zadanie 5: Włączanie tooAzure synchronizacji haseł usług domenowych w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="d481a-123">Task 5: enable password synchronization tooAzure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
