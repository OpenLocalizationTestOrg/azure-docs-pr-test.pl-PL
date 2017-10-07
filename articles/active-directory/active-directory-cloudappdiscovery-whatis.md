---
title: "aaaFinding niezarządzanych aplikacji w chmurze z usługi Cloud App Discovery | Dokumentacja firmy Microsoft"
description: "Zawiera informacje o znajdowanie aplikacji i zarządzanie nimi z Cloud App Discovery, jakie są zalety hello i jak działa."
services: active-directory
keywords: "Usługa cloud app discovery, zarządzanie aplikacjami"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="c9006-104">Znajdowanie niezarządzanych aplikacji w chmurze z usługi Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="c9006-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="c9006-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c9006-105">Overview</span></span>
<span data-ttu-id="c9006-106">W nowoczesnych przedsiębiorstwa działów IT często nie są znane wszystkie hello aplikacji w chmurze czy członków organizacji używać toodo służbowym.</span><span class="sxs-lookup"><span data-stu-id="c9006-106">In modern enterprises, IT departments are often not aware of all hello cloud applications that members of their organization use toodo their work.</span></span> <span data-ttu-id="c9006-107">Jest łatwy toosee Dlaczego Administratorzy byłyby danych toocorporate nieautoryzowanym dostępem, wycieku danych oraz inne zagrożenia dla bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="c9006-107">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="c9006-108">To Brak świadomości ułatwia tworzenie planu zajmowanie się te zagrożenia bezpieczeństwa wydawać się czasochłonnym zadaniem.</span><span class="sxs-lookup"><span data-stu-id="c9006-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="c9006-109">Usługa cloud App Discovery jest funkcją Premium usługi Azure Active Directory (AD), umożliwiającą aplikacji w chmurze toodiscover używany przez hello osób w danej organizacji.</span><span class="sxs-lookup"><span data-stu-id="c9006-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you toodiscover cloud applications being used by hello people in your organization.</span></span>

<span data-ttu-id="c9006-110">**Usługa Cloud App Discovery można:**</span><span class="sxs-lookup"><span data-stu-id="c9006-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="c9006-111">Znajdź hello używane aplikacje w chmurze i pomiar wykorzystanie przez liczbę użytkowników, ilości ruchu lub liczba aplikacji toohello żądania sieci web.</span><span class="sxs-lookup"><span data-stu-id="c9006-111">Find hello cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests toohello application.</span></span>
* <span data-ttu-id="c9006-112">Zidentyfikuj hello użytkowników, którzy korzystają z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9006-112">Identify hello users that are using an application.</span></span>
* <span data-ttu-id="c9006-113">Eksportowanie danych do analizy w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="c9006-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="c9006-114">Przenoszenie tych aplikacji pod kontrolą IT i Włącz funkcji logowania jednokrotnego do zarządzania użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="c9006-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="c9006-115">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="c9006-115">How it works</span></span>
1. <span data-ttu-id="c9006-116">Aplikacja użycia agenci są zainstalowani na komputerach użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c9006-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="c9006-117">informacje o użycia aplikacji Hello przechwycone przez agentów hello jest przesyłany przez bezpieczny kanał zaszyfrowany toohello aplikacji odnajdywania usługą w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c9006-117">hello application usage information captured by hello agents is sent over a secure, encrypted channel toohello cloud app discovery service.</span></span>
3. <span data-ttu-id="c9006-118">Hello usługi Cloud App Discovery daje w wyniku hello danych i generuje raporty.</span><span class="sxs-lookup"><span data-stu-id="c9006-118">hello Cloud App Discovery service evaluates hello data and generates reports.</span></span>

![Diagram odnajdywania aplikacji w chmurze](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="c9006-120">Zobacz tooget wprowadzenie Cloud App Discovery [pobierania uruchomiona z Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="c9006-120">tooget started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="c9006-121">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="c9006-121">Related articles</span></span>
* [<span data-ttu-id="c9006-122">Cloud App Discovery zabezpieczeń i zagadnienia dotyczące ochrony prywatności</span><span class="sxs-lookup"><span data-stu-id="c9006-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="c9006-123">Przewodnik wdrażania zasad grupy odnajdywania aplikacji chmury</span><span class="sxs-lookup"><span data-stu-id="c9006-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="c9006-124">Przewodnik wdrażania programu System Center cloud App odnajdywania</span><span class="sxs-lookup"><span data-stu-id="c9006-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="c9006-125">Ustawienia funkcji cloud Discovery aplikacji rejestru dotyczące serwerów Proxy z portami niestandardowe</span><span class="sxs-lookup"><span data-stu-id="c9006-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="c9006-126">Wykaz cloud App Discovery agenta zmian</span><span class="sxs-lookup"><span data-stu-id="c9006-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="c9006-127">Usługa cloud App Discovery — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="c9006-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="c9006-128">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9006-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

