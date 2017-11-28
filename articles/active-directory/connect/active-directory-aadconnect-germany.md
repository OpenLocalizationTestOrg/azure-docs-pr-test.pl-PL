---
title: "Program Azure AD Connect w usłudze Microsoft Cloud w Niemczech"
description: "Program Azure AD Connect umożliwia integrowanie katalogów lokalnych z usługą Azure Active Directory. Dzięki temu można posługiwać się wspólną tożsamością dla usługi Office 365, platformy Azure i aplikacji SaaS zintegrowanych z usługą Azure AD."
keywords: "wprowadzenie do programu Azure AD Connect, omówienie programu Azure AD Connect, co to jest program Azure AD Connect, instalowanie usługi Active Directory, Niemcy, Black Forest"
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
ms.openlocfilehash: 4c55b116c0dc080ae316caca873a7b693caa793b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="f2b54-105">Program Azure AD Connect w usłudze Microsoft Cloud w Niemczech — publiczna wersja zapoznawcza</span><span class="sxs-lookup"><span data-stu-id="f2b54-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="f2b54-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="f2b54-106">Introduction</span></span>
<span data-ttu-id="f2b54-107">Azure AD Connect zapewnia synchronizację między lokalną usługą Active Directory a usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f2b54-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="f2b54-108">Obecnie wiele scenariuszy w usłudze [Microsoft Cloud w Niemczech](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) musi być wykonywanych przez operatora.</span><span class="sxs-lookup"><span data-stu-id="f2b54-108">Currently, many of the scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by the operator.</span></span> <span data-ttu-id="f2b54-109">Korzystając z usługi Microsoft Cloud w Niemczech, należy pamiętać o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="f2b54-109">When using Microsoft Cloud Germany, you must be aware of the following:</span></span>

* <span data-ttu-id="f2b54-110">Następujące adresy URL muszą zostać otwarte na serwerze proxy, aby synchronizacja zakończyła się pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="f2b54-110">The following URLs must be opened on a proxy server for synchronization to occur successfully:</span></span>
  
  * <span data-ttu-id="f2b54-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="f2b54-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="f2b54-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="f2b54-112">*.windows.net</span></span>
  * * <span data-ttu-id="f2b54-113">Listy odwołania certyfikatów</span><span class="sxs-lookup"><span data-stu-id="f2b54-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="f2b54-114">Po zalogowaniu do katalogu usługi Azure AD należy używać konta w domenie onmicrosoft.de.</span><span class="sxs-lookup"><span data-stu-id="f2b54-114">When you sign in to your Azure AD directory, you must use an account in the onmicrosoft.de domain.</span></span>
* <span data-ttu-id="f2b54-115">Następujące funkcje nie są dostępne:</span><span class="sxs-lookup"><span data-stu-id="f2b54-115">The following features are not available:</span></span>
  * <span data-ttu-id="f2b54-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="f2b54-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="f2b54-117">Automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="f2b54-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="f2b54-118">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="f2b54-118">Download</span></span>
<span data-ttu-id="f2b54-119">Usługę Azure AD Connect można pobrać z bloku programu Azure AD Connect w portalu.</span><span class="sxs-lookup"><span data-stu-id="f2b54-119">You can download Azure AD Connect from the Azure AD Connect blade within the portal.</span></span>  <span data-ttu-id="f2b54-120">Znajdź blok programu Azure AD Connect, korzystając z poniższych instrukcji.</span><span class="sxs-lookup"><span data-stu-id="f2b54-120">Use the instructions below to locate the Azure AD Connect blade.</span></span>

### <a name="the-azure-ad-connect-blade"></a><span data-ttu-id="f2b54-121">Blok programu Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f2b54-121">The Azure AD Connect Blade</span></span>
<span data-ttu-id="f2b54-122">Po zalogowaniu się do witryny Azure Portal wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f2b54-122">Once you have signed in to the Azure portal, do the following:</span></span>

1. <span data-ttu-id="f2b54-123">Przejdź do pozycji Przeglądaj</span><span class="sxs-lookup"><span data-stu-id="f2b54-123">Go to Browse</span></span>
2. <span data-ttu-id="f2b54-124">Wybierz pozycję Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2b54-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="f2b54-125">Następnie wybierz pozycję Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f2b54-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="f2b54-126">Powinien zostać wyświetlony następujący ekran:</span><span class="sxs-lookup"><span data-stu-id="f2b54-126">You should see the following:</span></span>

![Blok programu Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="f2b54-128">W poniższej tabeli opisano funkcje wyświetlane w bloku.</span><span class="sxs-lookup"><span data-stu-id="f2b54-128">The following table describes the features shown in the blade.</span></span>

| <span data-ttu-id="f2b54-129">Tytuł</span><span class="sxs-lookup"><span data-stu-id="f2b54-129">Title</span></span> | <span data-ttu-id="f2b54-130">Opis</span><span class="sxs-lookup"><span data-stu-id="f2b54-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f2b54-131">STAN SYNCHRONIZACJI</span><span class="sxs-lookup"><span data-stu-id="f2b54-131">SYNC STATUS</span></span> |<span data-ttu-id="f2b54-132">Informuje, czy synchronizacja jest włączona, czy wyłączona.</span><span class="sxs-lookup"><span data-stu-id="f2b54-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="f2b54-133">OSTATNIA SYNCHRONIZACJA</span><span class="sxs-lookup"><span data-stu-id="f2b54-133">LAST SYNC</span></span> |<span data-ttu-id="f2b54-134">Godzina zakończenia ostatniej pomyślnej synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="f2b54-134">The last time a successful sync completed.</span></span> |
| <span data-ttu-id="f2b54-135">DOMENY FEDERACYJNE</span><span class="sxs-lookup"><span data-stu-id="f2b54-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="f2b54-136">Wyświetla liczbę obecnie skonfigurowanych domen federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="f2b54-136">Shows the number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="f2b54-137">Instalacja</span><span class="sxs-lookup"><span data-stu-id="f2b54-137">Installation</span></span>
<span data-ttu-id="f2b54-138">Możesz zainstalować program Azure AD Connect, korzystając z dokumentacji znajdującej się [tutaj](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="f2b54-138">To install Azure AD Connect, you can use the documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="f2b54-139">Funkcje zaawansowane i dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="f2b54-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="f2b54-140">Aby uzyskać dodatkowe informacje i wskazówki dotyczące ustawień niestandardowych lub zaawansowanych konfiguracji, na początek zapoznaj się z artykułem [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="f2b54-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="f2b54-141">Ta strona zawiera informacje i linki do dodatkowych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="f2b54-141">This page provides information and links to additional guidance.</span></span>

