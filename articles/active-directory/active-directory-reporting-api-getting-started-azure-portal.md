---
title: "Wprowadzenie do raportowania interfejsu API usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć pracę z usługą Active Directory Azure, interfejsu API raportowania"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 9944cbd2b1b7c4acb18d37da1394c0bbc170f77d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api"></a><span data-ttu-id="a3224-103">Wprowadzenie do korzystania z usługi Azure Active Directory raportowania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a3224-103">Getting started with the Azure Active Directory reporting API</span></span>

<span data-ttu-id="a3224-104">Usługa Azure Active Directory oferuje szerokiej gamy raportów.</span><span class="sxs-lookup"><span data-stu-id="a3224-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="a3224-105">Dane z tych raportów mogą być bardzo przydatne w aplikacjach, takich jak systemy SIEM oraz narzędzia do inspekcji i analizy biznesowej.</span><span class="sxs-lookup"><span data-stu-id="a3224-105">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="a3224-106">Interfejsy API raportów usługi Azure AD umożliwiają dostęp programowy do danych za pomocą zestawu interfejsów API opartych na architekturze REST.</span><span class="sxs-lookup"><span data-stu-id="a3224-106">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="a3224-107">Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.</span><span class="sxs-lookup"><span data-stu-id="a3224-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="a3224-108">Ten artykuł zawiera informacje potrzebne do Rozpoczynanie pracy z usługą Azure AD, na zgłoszenie interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a3224-108">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="a3224-109">W następnej sekcji możesz znaleźć szczegółowe informacje o użyciu inspekcji i logowania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a3224-109">In the next section, you find more details about using the audit and sign-in APIs.</span></span> 

<span data-ttu-id="a3224-110">Często zadawane pytania, przeczytaj nasze [— często zadawane pytania](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="a3224-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="a3224-111">W przypadku problemów skontaktuj się z [pliku biletu pomocy technicznej](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="a3224-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="a3224-112">Mapa uczenia się</span><span class="sxs-lookup"><span data-stu-id="a3224-112">Learning map</span></span>
1. <span data-ttu-id="a3224-113">**Przygotowanie** — przed próbek interfejsu API można przetestować, należy wykonać [wymagania wstępne dotyczące raportowania interfejsu API usługi Azure AD dostęp](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a3224-113">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="a3224-114">**Eksploruj** -uzyskać pierwszy wrażenie raportowania interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="a3224-114">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="a3224-115">Korzystanie z przykładów dla inspekcji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a3224-115">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="a3224-116">Korzystanie z przykładów dla raport aktywności logowania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a3224-116">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="a3224-117">**Dostosowywanie** — tworzenie własnych rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="a3224-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="a3224-118">Przy użyciu audytu dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a3224-118">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="a3224-119">Przy użyciu działań logowania odwołania raportu interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a3224-119">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="a3224-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a3224-120">Next Steps</span></span>
<span data-ttu-id="a3224-121">Jeśli zastanawiasz się wyświetlić wszystkie dostępne punkty końcowe interfejsu API usługi Azure AD Graph, użyj tego linku: [https://graph.windows.net/tenant-name/activities/$ metadanych? api-version = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="a3224-121">If you are curious to see all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

