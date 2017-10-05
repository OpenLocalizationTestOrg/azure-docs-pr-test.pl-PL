---
title: "Ustawienia funkcji cloud App Discovery rejestru dla serwera Proxy usług | Dokumentacja firmy Microsoft"
description: "Celem tego tematu jest dostarczają czynności, które należy wykonać, aby ustawić wymaganego portu na komputerach z systemem agenta Cloud App Discovery."
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
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="7a9f4-103">Ustawienia funkcji cloud Discovery aplikacji rejestru dla usługi serwera Proxy</span><span class="sxs-lookup"><span data-stu-id="7a9f4-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="7a9f4-104">Domyślnie agenta Cloud App Discovery jest skonfigurowany do użycia tylko porty 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="7a9f4-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span></span> <span data-ttu-id="7a9f4-105">Jeśli planujesz zainstalowanie Cloud App Discovery w środowisku z serwera proxy, który jest używany niestandardowy port (80 ani 443), należy skonfigurować agentów do użycia tego portu.</span><span class="sxs-lookup"><span data-stu-id="7a9f4-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span></span> <span data-ttu-id="7a9f4-106">Konfiguracja jest oparta na kluczu rejestru.</span><span class="sxs-lookup"><span data-stu-id="7a9f4-106">The configuration is based on a registry key.</span></span>

<span data-ttu-id="7a9f4-107">Celem tego tematu jest dostarczają czynności, które należy wykonać, aby ustawić wymaganego portu na komputerach z systemem agenta Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="7a9f4-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span></span>

<span data-ttu-id="7a9f4-108">**Aby zmodyfikować port używany przez komputer z uruchomionym agentem Cloud App Discovery, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span></span>

1. <span data-ttu-id="7a9f4-109">Uruchom Edytor rejestru.</span><span class="sxs-lookup"><span data-stu-id="7a9f4-109">Start the registry editor.</span></span> <br> ![Uruchom polecenie](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="7a9f4-111">Przejdź do lub utwórz następujący klucz rejestru:</span><span class="sxs-lookup"><span data-stu-id="7a9f4-111">Navigate to or create the following registry key:</span></span> <br> <span data-ttu-id="7a9f4-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud Discovery\Endpoint aplikacji**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="7a9f4-113">Utwórz nową **ciągu wielokrotnego** wartość o nazwie **porty**.</span><span class="sxs-lookup"><span data-stu-id="7a9f4-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="7a9f4-114">![Nowy](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="7a9f4-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="7a9f4-115">Aby otworzyć **Edytowanie ciągu wielokrotnego** okna dialogowego, kliknij dwukrotnie wartość portów.</span><span class="sxs-lookup"><span data-stu-id="7a9f4-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span></span>
5. <span data-ttu-id="7a9f4-116">W polu tekstowym wartość danych wpisz następujące wartości, a następnie dodaj wszystkie porty niestandardowe, które są używane przez Twoją organizację:</span><span class="sxs-lookup"><span data-stu-id="7a9f4-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="7a9f4-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-117">
   **80**</span></span> <br><span data-ttu-id="7a9f4-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-118">
   **8080**</span></span> <br><span data-ttu-id="7a9f4-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-119">
   **8118**</span></span> <br><span data-ttu-id="7a9f4-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-120">
   **8888**</span></span> <br><span data-ttu-id="7a9f4-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-121">
   **81**</span></span> <br><span data-ttu-id="7a9f4-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-122">
   **12080**</span></span> <br><span data-ttu-id="7a9f4-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-123">
**6999**</span></span> <br><span data-ttu-id="7a9f4-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-124">
**30606**</span></span> <br><span data-ttu-id="7a9f4-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-125">
**31595**</span></span> <br><span data-ttu-id="7a9f4-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-126">
**4080**</span></span> <br><span data-ttu-id="7a9f4-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-127">
**443**</span></span> <br><span data-ttu-id="7a9f4-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-128">
**1110**</span></span> <br><br><span data-ttu-id="7a9f4-129">
![Edytowanie ciągu wielokrotnego](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="7a9f4-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="7a9f4-130">Kliknij przycisk **OK** zamknąć **Edytowanie ciągu wielokrotnego** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7a9f4-130">Click **OK** to close the **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="7a9f4-131">**Dodatkowe zasoby**</span><span class="sxs-lookup"><span data-stu-id="7a9f4-131">**Additional Resources**</span></span>

* [<span data-ttu-id="7a9f4-132">Jak odnajdywać niezatwierdzone aplikacje w chmurze używanych mojej organizacji</span><span class="sxs-lookup"><span data-stu-id="7a9f4-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

