---
title: "Ustawienia rejestru odnajdywania aplikacji dla usługi serwera Proxy aaaCloud | Dokumentacja firmy Microsoft"
description: "cel Hello tego tematu jest tooprovide program hello kroki należy dodać port hello wymagane tooset tooperform na powitania komputerach hello agenta Cloud App Discovery."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="897e5-103">Ustawienia funkcji cloud Discovery aplikacji rejestru dla usługi serwera Proxy</span><span class="sxs-lookup"><span data-stu-id="897e5-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="897e5-104">Domyślnie agenta Cloud App Discovery hello jest skonfigurowany toouse tylko porty hello 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="897e5-104">By default, hello Cloud App Discovery agent is configured toouse only hello ports 80 or 443.</span></span> <span data-ttu-id="897e5-105">Jeśli planujesz zainstalowanie Cloud App Discovery w środowisku z serwera proxy, który jest używany niestandardowy port (80 ani 443), należy tooconfigure Twojego toouse agentów tego portu.</span><span class="sxs-lookup"><span data-stu-id="897e5-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need tooconfigure your agents toouse this port.</span></span> <span data-ttu-id="897e5-106">Konfiguracja Hello jest oparta na klucz rejestru.</span><span class="sxs-lookup"><span data-stu-id="897e5-106">hello configuration is based on a registry key.</span></span>

<span data-ttu-id="897e5-107">cel Hello tego tematu jest tooprovide program hello kroki należy dodać port hello wymagane tooset tooperform na powitania komputerach hello agenta Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="897e5-107">hello objective of this topic is tooprovide you with hello steps you need tooperform tooset hello required port on hello computers running hello Cloud App Discovery agent.</span></span>

<span data-ttu-id="897e5-108">**toomodify hello port używany przez program hello komputerze agenta Cloud App Discovery hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="897e5-108">**toomodify hello port used by hello computer running hello Cloud App Discovery agent, perform hello following steps:**</span></span>

1. <span data-ttu-id="897e5-109">Uruchom Edytor rejestru hello.</span><span class="sxs-lookup"><span data-stu-id="897e5-109">Start hello registry editor.</span></span> <br> ![Uruchom polecenie](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="897e5-111">Przejdź tooor utworzyć powitania po klucz rejestru:</span><span class="sxs-lookup"><span data-stu-id="897e5-111">Navigate tooor create hello following registry key:</span></span> <br> <span data-ttu-id="897e5-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud Discovery\Endpoint aplikacji**</span><span class="sxs-lookup"><span data-stu-id="897e5-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="897e5-113">Utwórz nową **ciągu wielokrotnego** wartość o nazwie **porty**.</span><span class="sxs-lookup"><span data-stu-id="897e5-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="897e5-114">![Nowy](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="897e5-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="897e5-115">Witaj tooopen **Edytowanie ciągu wielokrotnego** okna dialogowego, kliknij dwukrotnie wartość porty hello.</span><span class="sxs-lookup"><span data-stu-id="897e5-115">tooopen hello **Edit Multi-String** dialog, double-click hello Ports value.</span></span>
5. <span data-ttu-id="897e5-116">W pole tekstowe danych wartości hello wpisz następujące wartości hello i dodać wszystkie porty niestandardowe, które są używane przez Twoją organizację:</span><span class="sxs-lookup"><span data-stu-id="897e5-116">In hello Value data textbox, type hello following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="897e5-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="897e5-117">
   **80**</span></span> <br><span data-ttu-id="897e5-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="897e5-118">
   **8080**</span></span> <br><span data-ttu-id="897e5-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="897e5-119">
   **8118**</span></span> <br><span data-ttu-id="897e5-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="897e5-120">
   **8888**</span></span> <br><span data-ttu-id="897e5-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="897e5-121">
   **81**</span></span> <br><span data-ttu-id="897e5-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="897e5-122">
   **12080**</span></span> <br><span data-ttu-id="897e5-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="897e5-123">
**6999**</span></span> <br><span data-ttu-id="897e5-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="897e5-124">
**30606**</span></span> <br><span data-ttu-id="897e5-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="897e5-125">
**31595**</span></span> <br><span data-ttu-id="897e5-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="897e5-126">
**4080**</span></span> <br><span data-ttu-id="897e5-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="897e5-127">
**443**</span></span> <br><span data-ttu-id="897e5-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="897e5-128">
**1110**</span></span> <br><br><span data-ttu-id="897e5-129">
![Edytowanie ciągu wielokrotnego](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="897e5-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="897e5-130">Kliknij przycisk **OK** tooclose hello **Edytowanie ciągu wielokrotnego** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="897e5-130">Click **OK** tooclose hello **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="897e5-131">**Dodatkowe zasoby**</span><span class="sxs-lookup"><span data-stu-id="897e5-131">**Additional Resources**</span></span>

* [<span data-ttu-id="897e5-132">Jak odnajdywać niezatwierdzone aplikacje w chmurze używanych mojej organizacji</span><span class="sxs-lookup"><span data-stu-id="897e5-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

