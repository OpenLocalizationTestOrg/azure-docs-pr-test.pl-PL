---
title: aaaAzure AD Connect w Niemczech Microsoft Cloud
description: "Program Azure AD Connect umożliwia integrowanie katalogów lokalnych z usługą Azure Active Directory. Dzięki temu tooprovide wspólną tożsamością dla usługi Office 365, Azure i aplikacji SaaS zintegrowanych z usługą Azure AD."
keywords: "wprowadzenie tooAzure AD Connect, omówienie usługi Azure AD Connect, co to jest usługa Azure AD Connect, instalowania usługi active directory, Niemczech, czarnym lesie"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="8f94c-105">Program Azure AD Connect w usłudze Microsoft Cloud w Niemczech — publiczna wersja zapoznawcza</span><span class="sxs-lookup"><span data-stu-id="8f94c-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="8f94c-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="8f94c-106">Introduction</span></span>
<span data-ttu-id="8f94c-107">Azure AD Connect zapewnia synchronizację między lokalną usługą Active Directory a usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8f94c-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="8f94c-108">Obecnie wiele scenariuszy hello w [Niemcy Microsoft Cloud](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) musi zostać wykonane przez operatora hello.</span><span class="sxs-lookup"><span data-stu-id="8f94c-108">Currently, many of hello scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by hello operator.</span></span> <span data-ttu-id="8f94c-109">Korzystając z Microsoft Cloud Niemczech, należy pamiętać o następujących hello:</span><span class="sxs-lookup"><span data-stu-id="8f94c-109">When using Microsoft Cloud Germany, you must be aware of hello following:</span></span>

* <span data-ttu-id="8f94c-110">Witaj następujące adresy URL muszą być otwarte na serwerze proxy dla synchronizacji toooccur pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="8f94c-110">hello following URLs must be opened on a proxy server for synchronization toooccur successfully:</span></span>
  
  * <span data-ttu-id="8f94c-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="8f94c-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="8f94c-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="8f94c-112">*.windows.net</span></span>
  * * <span data-ttu-id="8f94c-113">Listy odwołania certyfikatów</span><span class="sxs-lookup"><span data-stu-id="8f94c-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="8f94c-114">Po zarejestrowaniu się w katalogu usługi Azure AD tooyour, należy użyć konta w domenie onmicrosoft.de hello.</span><span class="sxs-lookup"><span data-stu-id="8f94c-114">When you sign in tooyour Azure AD directory, you must use an account in hello onmicrosoft.de domain.</span></span>
* <span data-ttu-id="8f94c-115">Witaj, następujące funkcje są niedostępne:</span><span class="sxs-lookup"><span data-stu-id="8f94c-115">hello following features are not available:</span></span>
  * <span data-ttu-id="8f94c-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="8f94c-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="8f94c-117">Automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="8f94c-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="8f94c-118">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="8f94c-118">Download</span></span>
<span data-ttu-id="8f94c-119">Azure AD Connect można pobrać z bloku Azure AD Connect hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="8f94c-119">You can download Azure AD Connect from hello Azure AD Connect blade within hello portal.</span></span>  <span data-ttu-id="8f94c-120">Użyj instrukcji hello poniżej toolocate hello Azure AD Connect bloku.</span><span class="sxs-lookup"><span data-stu-id="8f94c-120">Use hello instructions below toolocate hello Azure AD Connect blade.</span></span>

### <a name="hello-azure-ad-connect-blade"></a><span data-ttu-id="8f94c-121">Hello Azure AD Connect bloku</span><span class="sxs-lookup"><span data-stu-id="8f94c-121">hello Azure AD Connect Blade</span></span>
<span data-ttu-id="8f94c-122">Po zalogowaniu toohello portalu Azure hello następujące:</span><span class="sxs-lookup"><span data-stu-id="8f94c-122">Once you have signed in toohello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="8f94c-123">Przejdź tooBrowse</span><span class="sxs-lookup"><span data-stu-id="8f94c-123">Go tooBrowse</span></span>
2. <span data-ttu-id="8f94c-124">Wybierz pozycję Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f94c-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="8f94c-125">Następnie wybierz pozycję Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="8f94c-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="8f94c-126">Powinny pojawić się następujące hello:</span><span class="sxs-lookup"><span data-stu-id="8f94c-126">You should see hello following:</span></span>

![Blok programu Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="8f94c-128">Witaj poniższej tabeli opisano funkcje hello wyświetlane w bloku hello.</span><span class="sxs-lookup"><span data-stu-id="8f94c-128">hello following table describes hello features shown in hello blade.</span></span>

| <span data-ttu-id="8f94c-129">Tytuł</span><span class="sxs-lookup"><span data-stu-id="8f94c-129">Title</span></span> | <span data-ttu-id="8f94c-130">Opis</span><span class="sxs-lookup"><span data-stu-id="8f94c-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f94c-131">STAN SYNCHRONIZACJI</span><span class="sxs-lookup"><span data-stu-id="8f94c-131">SYNC STATUS</span></span> |<span data-ttu-id="8f94c-132">Informuje, czy synchronizacja jest włączona, czy wyłączona.</span><span class="sxs-lookup"><span data-stu-id="8f94c-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="8f94c-133">OSTATNIA SYNCHRONIZACJA</span><span class="sxs-lookup"><span data-stu-id="8f94c-133">LAST SYNC</span></span> |<span data-ttu-id="8f94c-134">Witaj czas ostatniej pomyślnej synchronizacji ukończone.</span><span class="sxs-lookup"><span data-stu-id="8f94c-134">hello last time a successful sync completed.</span></span> |
| <span data-ttu-id="8f94c-135">DOMENY FEDERACYJNE</span><span class="sxs-lookup"><span data-stu-id="8f94c-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="8f94c-136">Pokazuje liczbę hello Sfederowanych domen obecnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="8f94c-136">Shows hello number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="8f94c-137">Instalacja</span><span class="sxs-lookup"><span data-stu-id="8f94c-137">Installation</span></span>
<span data-ttu-id="8f94c-138">tooinstall Azure AD Connect, korzystając z dokumentacji hello [tutaj](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="8f94c-138">tooinstall Azure AD Connect, you can use hello documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="8f94c-139">Funkcje zaawansowane i dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="8f94c-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="8f94c-140">Aby uzyskać dodatkowe informacje i wskazówki dotyczące ustawień niestandardowych lub zaawansowanych konfiguracji, na początek zapoznaj się z artykułem [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="8f94c-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="8f94c-141">Ta strona zawiera informacje i linki tooadditional wskazówki.</span><span class="sxs-lookup"><span data-stu-id="8f94c-141">This page provides information and links tooadditional guidance.</span></span>

