---
title: "Klasyczny portal łączniki serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Opisano sposób tworzenia i zarządzania grupami łączników w serwera Proxy aplikacji usługi Azure AD."
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
ms.openlocfilehash: fc65c4053c45d9c16c62ee0fe65924133a4bb94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="7a136-103">Publikowanie aplikacji w odrębnych sieci i lokalizacje przy użyciu grup łącznika</span><span class="sxs-lookup"><span data-stu-id="7a136-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a136-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7a136-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="7a136-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7a136-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="7a136-106">Łącznik grupy są przydatne w przypadku różnych scenariuszy, w tym:</span><span class="sxs-lookup"><span data-stu-id="7a136-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="7a136-107">Lokacje z wielu połączonych centrów danych.</span><span class="sxs-lookup"><span data-stu-id="7a136-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="7a136-108">W takim przypadku chcesz zachować tyle ruchu sieciowego w centrum danych jak to możliwe, ponieważ łącza między datacenter jest kosztowne i wolnego.</span><span class="sxs-lookup"><span data-stu-id="7a136-108">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="7a136-109">Można wdrożyć łączników w każde centrum danych do obsługi tylko te aplikacje, które znajdują się w centrum danych.</span><span class="sxs-lookup"><span data-stu-id="7a136-109">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span></span> <span data-ttu-id="7a136-110">Takie podejście minimalizuje łącza między datacenter i zapewnia całkowicie przezroczysty środowisko dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7a136-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span></span>
* <span data-ttu-id="7a136-111">Zarządzanie aplikacji zainstalowanych w izolowanych sieciach, które nie są częścią sieci firmowej głównego.</span><span class="sxs-lookup"><span data-stu-id="7a136-111">Managing applications installed on isolated networks that are not part of the main corporate network.</span></span> <span data-ttu-id="7a136-112">Łącznik grupy służy do instalowania dedykowanego łączników w izolowanych sieciach również Izolowanie aplikacji sieci.</span><span class="sxs-lookup"><span data-stu-id="7a136-112">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span></span>
* <span data-ttu-id="7a136-113">Aplikacje zainstalowane na IaaS, aby uzyskać dostęp do chmury łącznik grup Podaj wspólne usługi bezpieczny dostęp do wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a136-113">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span></span> <span data-ttu-id="7a136-114">Łącznik grup nie utworzyć dodatkowe zależności w sieci firmowej lub fragmentu środowisko aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a136-114">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span></span> <span data-ttu-id="7a136-115">Łączniki można zainstalować na każdym centrum danych w chmurze i służyć tylko te aplikacje, które znajdują się w tej sieci.</span><span class="sxs-lookup"><span data-stu-id="7a136-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="7a136-116">Można zainstalować wiele łączników w celu uzyskania wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="7a136-116">You can install several connectors to achieve high availability.</span></span>
* <span data-ttu-id="7a136-117">Obsługa środowisk obejmującego wiele lasów, w których określonych łączników można wdrożone w każdym lesie i ustawiony służyć określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a136-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set to serve specific applications.</span></span>
* <span data-ttu-id="7a136-118">Łącznik grup można w lokacjach odzyskiwania po awarii, albo wykrywa tryb failover lub jako kopii zapasowych dla lokacji głównej.</span><span class="sxs-lookup"><span data-stu-id="7a136-118">Connector groups can be used in Disaster Recovery sites to either detect failover or as backup for the main site.</span></span>
* <span data-ttu-id="7a136-119">Łącznik grupy mogą służyć do obsługi wielu firm z pojedynczej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="7a136-119">Connector groups can also be used to serve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="7a136-120">Wymaganie wstępne: Tworzenie łączników</span><span class="sxs-lookup"><span data-stu-id="7a136-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="7a136-121">Aby pogrupować łączników, [zainstalować wiele łączników](active-directory-application-proxy-enable.md), nazwie i grupować.</span><span class="sxs-lookup"><span data-stu-id="7a136-121">To group your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="7a136-122">Na koniec należy przypisać je do określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a136-122">Finally you have to assign them to specific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="7a136-123">Krok 1: Tworzenie grup łącznika</span><span class="sxs-lookup"><span data-stu-id="7a136-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="7a136-124">Można utworzyć dowolną liczbę grup łącznika.</span><span class="sxs-lookup"><span data-stu-id="7a136-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="7a136-125">Tworzenie grupy łącznika odbywa się w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7a136-125">Connector group creation is accomplished in the Azure classic portal.</span></span>

1. <span data-ttu-id="7a136-126">Wybierz katalog, a następnie kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="7a136-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="7a136-127">![Serwer proxy aplikacji, skonfiguruj zrzut ekranu — kliknij przycisk Zarządzaj grupami łącznika](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="7a136-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="7a136-128">W obszarze Serwer Proxy aplikacji, kliknij **grup zarządzania łącznika** i utworzyć grupę łącznika przez nadanie nazwy grupy.</span><span class="sxs-lookup"><span data-stu-id="7a136-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving the group a name.</span></span>  
    <span data-ttu-id="7a136-129">![Zrzut ekranu — Nazwa nowej grupy grup łącznika serwera proxy aplikacji](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="7a136-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-to-your-groups"></a><span data-ttu-id="7a136-130">Krok 2: Przypisanie łączniki do grup</span><span class="sxs-lookup"><span data-stu-id="7a136-130">Step 2: Assign connectors to your groups</span></span>
<span data-ttu-id="7a136-131">Po utworzeniu grupy łącznika, przesuń łączniki do odpowiedniej grupy.</span><span class="sxs-lookup"><span data-stu-id="7a136-131">Once the connector groups are created, move the connectors to the appropriate group.</span></span>

1. <span data-ttu-id="7a136-132">W obszarze **serwera Proxy aplikacji**, kliknij przycisk **Zarządzanie łączniki**.</span><span class="sxs-lookup"><span data-stu-id="7a136-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="7a136-133">W obszarze **grupy**, wybierz grupę dla poszczególnych łączników.</span><span class="sxs-lookup"><span data-stu-id="7a136-133">Under **Group**, select the group you want for each connector.</span></span> <span data-ttu-id="7a136-134">Łączniki może potrwać do 10 minut, staje się aktywny w nowej grupie.</span><span class="sxs-lookup"><span data-stu-id="7a136-134">It might take the connectors up to 10 minutes to become active in the new group.</span></span>  
    <span data-ttu-id="7a136-135">![Zrzut w ekranu łączniki serwera proxy aplikacji — wybierz grupę z menu rozwijanego](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="7a136-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-to-your-connector-groups"></a><span data-ttu-id="7a136-136">Krok 3: Przypisanie aplikacji do grup łącznika</span><span class="sxs-lookup"><span data-stu-id="7a136-136">Step 3: Assign applications to your connector groups</span></span>
<span data-ttu-id="7a136-137">Ostatnim krokiem jest ustalenie każdej aplikacji do grupy łącznika, która dostarcza je.</span><span class="sxs-lookup"><span data-stu-id="7a136-137">The last step is to set each application to the connector group that serves it.</span></span>

1. <span data-ttu-id="7a136-138">W klasycznym portalu Azure, w katalogu, wybierz aplikacji, którą chcesz przypisać do grupy, a następnie kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="7a136-138">In the Azure classic portal, in your directory, select the Application you want to assign to the group and click **Configure**.</span></span>
2. <span data-ttu-id="7a136-139">W obszarze **grupy łącznika**, wybierz grupę, która będzie używać aplikacja.</span><span class="sxs-lookup"><span data-stu-id="7a136-139">Under **Connector group**, select the group you want the application to use.</span></span> <span data-ttu-id="7a136-140">Ta zmiana zostanie zastosowane natychmiast.</span><span class="sxs-lookup"><span data-stu-id="7a136-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="7a136-141">![Zrzut ekranu z grupy łącznika serwera proxy aplikacji — wybierz grupę z menu rozwijanego](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="7a136-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="7a136-142">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7a136-142">See also</span></span>
* [<span data-ttu-id="7a136-143">Włączanie serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="7a136-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="7a136-144">Włączanie logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="7a136-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="7a136-145">Włączanie dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="7a136-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="7a136-146">Rozwiązywanie problemów, które masz problem z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="7a136-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="7a136-147">Aby zapoznać się z najnowszymi informacjami i aktualizacjami, zobacz [blog dotyczący serwera proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="7a136-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
