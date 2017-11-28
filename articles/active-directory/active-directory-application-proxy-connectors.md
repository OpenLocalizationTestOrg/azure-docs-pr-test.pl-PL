---
title: "łączniki serwera Proxy aplikacji usługi Azure AD z portalu aaaClassic | Dokumentacja firmy Microsoft"
description: "Obejmuje jak toocreate grup łączników w serwera Proxy aplikacji usługi Azure AD i zarządzanie nimi."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="6a92a-103">Publikowanie aplikacji w odrębnych sieci i lokalizacje przy użyciu grup łącznika</span><span class="sxs-lookup"><span data-stu-id="6a92a-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6a92a-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6a92a-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="6a92a-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6a92a-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="6a92a-106">Łącznik grupy są przydatne w przypadku różnych scenariuszy, w tym:</span><span class="sxs-lookup"><span data-stu-id="6a92a-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="6a92a-107">Lokacje z wielu połączonych centrów danych.</span><span class="sxs-lookup"><span data-stu-id="6a92a-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="6a92a-108">W takim przypadku ma tookeep tyle ruchu w ramach centrum danych hello możliwie ponieważ łącza między datacenter są kosztowne i bardzo wolno.</span><span class="sxs-lookup"><span data-stu-id="6a92a-108">In this case, you want tookeep as much traffic within hello datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="6a92a-109">Można wdrożyć łączników w każdym datacenter tooserve tylko hello aplikacje znajdujące się w obrębie centrum danych hello.</span><span class="sxs-lookup"><span data-stu-id="6a92a-109">You can deploy connectors in each datacenter tooserve only hello applications that reside within hello datacenter.</span></span> <span data-ttu-id="6a92a-110">Takie podejście minimalizuje łącza między datacenter i zapewnia całkowicie przezroczysty tooyour użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6a92a-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience tooyour users.</span></span>
* <span data-ttu-id="6a92a-111">Zarządzanie aplikacji zainstalowanych w izolowanych sieciach, które nie są częścią sieci firmowej głównego hello.</span><span class="sxs-lookup"><span data-stu-id="6a92a-111">Managing applications installed on isolated networks that are not part of hello main corporate network.</span></span> <span data-ttu-id="6a92a-112">Łącznik grup tooinstall dedykowanego łączników można użyć w izolowanych sieciach tooalso odizolowanego aplikacji toohello sieci.</span><span class="sxs-lookup"><span data-stu-id="6a92a-112">You can use connector groups tooinstall dedicated connectors on isolated networks tooalso isolate applications toohello network.</span></span>
* <span data-ttu-id="6a92a-113">Aplikacje zainstalowane na IaaS, aby uzyskać dostęp do chmury łącznik grupy zapewniają wspólnej toosecure hello dostępu tooall hello aplikacje usługi.</span><span class="sxs-lookup"><span data-stu-id="6a92a-113">For applications installed on IaaS for cloud access, connector groups provide a common service toosecure hello access tooall hello apps.</span></span> <span data-ttu-id="6a92a-114">Łącznik grup nie utworzyć dodatkowe zależności w sieci firmowej lub fragmentu środowisko aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6a92a-114">Connector groups don't create additional dependency on your corporate network, or fragment hello app experience.</span></span> <span data-ttu-id="6a92a-115">Łączniki można zainstalować na każdym centrum danych w chmurze i służyć tylko te aplikacje, które znajdują się w tej sieci.</span><span class="sxs-lookup"><span data-stu-id="6a92a-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="6a92a-116">Można zainstalować wiele łączników tooachieve wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="6a92a-116">You can install several connectors tooachieve high availability.</span></span>
* <span data-ttu-id="6a92a-117">Obsługa środowisk obejmującego wiele lasów, w których określonych łączników można wdrożone w każdym lesie i ustawić tooserve określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6a92a-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set tooserve specific applications.</span></span>
* <span data-ttu-id="6a92a-118">Łącznik grupy mogą być używane w lokacjach odzyskiwania po awarii tooeither wykryć pracy awaryjnej lub jako kopia zapasowa hello główny witryny.</span><span class="sxs-lookup"><span data-stu-id="6a92a-118">Connector groups can be used in Disaster Recovery sites tooeither detect failover or as backup for hello main site.</span></span>
* <span data-ttu-id="6a92a-119">Łącznik grup może również być używane tooserve wielu firm z pojedynczej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="6a92a-119">Connector groups can also be used tooserve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="6a92a-120">Wymaganie wstępne: Tworzenie łączników</span><span class="sxs-lookup"><span data-stu-id="6a92a-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="6a92a-121">toogroup łączników, [zainstalować wiele łączników](active-directory-application-proxy-enable.md), nazwie i grupować.</span><span class="sxs-lookup"><span data-stu-id="6a92a-121">toogroup your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="6a92a-122">Na koniec masz tooassign ich toospecific aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6a92a-122">Finally you have tooassign them toospecific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="6a92a-123">Krok 1: Tworzenie grup łącznika</span><span class="sxs-lookup"><span data-stu-id="6a92a-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="6a92a-124">Można utworzyć dowolną liczbę grup łącznika.</span><span class="sxs-lookup"><span data-stu-id="6a92a-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="6a92a-125">Tworzenie grupy łącznika odbywa się w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6a92a-125">Connector group creation is accomplished in hello Azure classic portal.</span></span>

1. <span data-ttu-id="6a92a-126">Wybierz katalog, a następnie kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="6a92a-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="6a92a-127">![Serwer proxy aplikacji, skonfiguruj zrzut ekranu — kliknij przycisk Zarządzaj grupami łącznika](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="6a92a-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="6a92a-128">W obszarze Serwer Proxy aplikacji, kliknij **grup zarządzania łącznika** i utworzyć grupę łącznika przez nadanie grupy hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="6a92a-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving hello group a name.</span></span>  
    <span data-ttu-id="6a92a-129">![Zrzut ekranu — Nazwa nowej grupy grup łącznika serwera proxy aplikacji](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="6a92a-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-tooyour-groups"></a><span data-ttu-id="6a92a-130">Krok 2: Przypisywanie łączniki tooyour grup</span><span class="sxs-lookup"><span data-stu-id="6a92a-130">Step 2: Assign connectors tooyour groups</span></span>
<span data-ttu-id="6a92a-131">Po utworzeniu grupy łącznika hello Przenieś hello łączniki toohello odpowiedniej grupy.</span><span class="sxs-lookup"><span data-stu-id="6a92a-131">Once hello connector groups are created, move hello connectors toohello appropriate group.</span></span>

1. <span data-ttu-id="6a92a-132">W obszarze **serwera Proxy aplikacji**, kliknij przycisk **Zarządzanie łączniki**.</span><span class="sxs-lookup"><span data-stu-id="6a92a-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="6a92a-133">W obszarze **grupy**, zaznacz grupę hello ma przez każdy łącznik.</span><span class="sxs-lookup"><span data-stu-id="6a92a-133">Under **Group**, select hello group you want for each connector.</span></span> <span data-ttu-id="6a92a-134">Łączniki hello się toobecome minut too10 może potrwać aktywne w hello nowej grupy.</span><span class="sxs-lookup"><span data-stu-id="6a92a-134">It might take hello connectors up too10 minutes toobecome active in hello new group.</span></span>  
    <span data-ttu-id="6a92a-135">![Zrzut w ekranu łączniki serwera proxy aplikacji — wybierz grupę z menu rozwijanego](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="6a92a-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-tooyour-connector-groups"></a><span data-ttu-id="6a92a-136">Krok 3: Przypisywanie aplikacji tooyour łącznika grup</span><span class="sxs-lookup"><span data-stu-id="6a92a-136">Step 3: Assign applications tooyour connector groups</span></span>
<span data-ttu-id="6a92a-137">ostatni krok Hello jest tooset każdej grupy łącznika toohello aplikacji, która dostarcza je.</span><span class="sxs-lookup"><span data-stu-id="6a92a-137">hello last step is tooset each application toohello connector group that serves it.</span></span>

1. <span data-ttu-id="6a92a-138">W hello klasycznego portalu Azure w danym katalogu, wybierz hello aplikacji tooassign toohello grupy i kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="6a92a-138">In hello Azure classic portal, in your directory, select hello Application you want tooassign toohello group and click **Configure**.</span></span>
2. <span data-ttu-id="6a92a-139">W obszarze **grupy łącznika**, wybierz grupy hello ma hello toouse aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6a92a-139">Under **Connector group**, select hello group you want hello application toouse.</span></span> <span data-ttu-id="6a92a-140">Ta zmiana zostanie zastosowane natychmiast.</span><span class="sxs-lookup"><span data-stu-id="6a92a-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="6a92a-141">![Zrzut ekranu z grupy łącznika serwera proxy aplikacji — wybierz grupę z menu rozwijanego](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="6a92a-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="6a92a-142">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6a92a-142">See also</span></span>
* [<span data-ttu-id="6a92a-143">Włączanie serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="6a92a-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="6a92a-144">Włączanie logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="6a92a-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="6a92a-145">Włączanie dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="6a92a-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="6a92a-146">Rozwiązywanie problemów, które masz problem z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="6a92a-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="6a92a-147">Najnowsze wiadomości powitania i aktualizacji, zapoznaj się z hello [Blog dotyczący serwera Proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="6a92a-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
