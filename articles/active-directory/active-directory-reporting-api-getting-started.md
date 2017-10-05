---
title: "Wprowadzenie do korzystania z usługi Azure AD raportowania interfejsu API w klasycznym portalu Azure AD | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć pracę z usługą Active Directory Azure, interfejsu API raportowania"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a><span data-ttu-id="5d6e7-103">Wprowadzenie do korzystania z usługi Azure Active Directory raportowania interfejsu API w klasycznym portalu Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d6e7-103">Getting started with the Azure Active Directory reporting API on the Azure AD classic portal</span></span>
<span data-ttu-id="5d6e7-104">*Ten temat jest częścią [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="5d6e7-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="5d6e7-105">Usługa Azure Active Directory oferuje szerokiej gamy raportów.</span><span class="sxs-lookup"><span data-stu-id="5d6e7-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="5d6e7-106">Dane z tych raportów mogą być bardzo przydatne w aplikacjach, takich jak systemy SIEM oraz narzędzia do inspekcji i analizy biznesowej.</span><span class="sxs-lookup"><span data-stu-id="5d6e7-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="5d6e7-107">Interfejsy API raportów usługi Azure AD umożliwiają dostęp programowy do danych za pomocą zestawu interfejsów API opartych na architekturze REST.</span><span class="sxs-lookup"><span data-stu-id="5d6e7-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="5d6e7-108">Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.</span><span class="sxs-lookup"><span data-stu-id="5d6e7-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="5d6e7-109">Ten artykuł zawiera informacje potrzebne do Rozpoczynanie pracy z usługą Azure AD, na zgłoszenie interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="5d6e7-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="5d6e7-110">W następnej sekcji możesz znaleźć szczegółowe informacje o użyciu inspekcji i logowania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="5d6e7-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="5d6e7-111">Dla wszystkich innych interfejsów API, zobacz [raportów usługi Azure AD i events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="5d6e7-111">For all other APIs, see the [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="5d6e7-112">Pytania, problemy lub opinie, skontaktuj się z [Pomoc raportowania usługi AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5d6e7-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="5d6e7-113">Mapa uczenia się</span><span class="sxs-lookup"><span data-stu-id="5d6e7-113">Learning map</span></span>
1. <span data-ttu-id="5d6e7-114">**Przygotowanie** — przed próbek interfejsu API można przetestować, należy wykonać [wymagania wstępne dotyczące raportowania interfejsu API usługi Azure AD dostęp](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="5d6e7-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="5d6e7-115">**Eksploruj** -uzyskać pierwszy wrażenie raportowania interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="5d6e7-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="5d6e7-116">Korzystanie z przykładów dla inspekcji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="5d6e7-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="5d6e7-117">Korzystanie z przykładów dla raport aktywności logowania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="5d6e7-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="5d6e7-118">**Dostosowywanie** — tworzenie własnych rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="5d6e7-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="5d6e7-119">Przy użyciu audytu dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="5d6e7-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="5d6e7-120">Przy użyciu działań logowania odwołania raportu interfejsu API</span><span class="sxs-lookup"><span data-stu-id="5d6e7-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="5d6e7-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d6e7-121">Next Steps</span></span>
<span data-ttu-id="5d6e7-122">Jeśli zastanawiasz się wyświetlić wszystkie dostępne punkty końcowe interfejsu API usługi Azure AD Graph, przechodząc do [https://graph.windows.net/tenant-name/reports/$ metadanych? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="5d6e7-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

