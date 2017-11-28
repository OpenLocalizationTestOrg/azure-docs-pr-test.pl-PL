---
title: "wprowadzenie do interfejsu API raportowania usługi Azure AD hello aaaGetting | Dokumentacja firmy Microsoft"
description: "Jak tooget wprowadzenie hello interfejsem API raportowania usługi Azure Active Directory"
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
ms.openlocfilehash: bb7d72ba445daa367d7502889c38a605a16f26d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api"></a><span data-ttu-id="65b6d-103">Wprowadzenie do korzystania z hello interfejsem API raportowania usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65b6d-103">Getting started with hello Azure Active Directory reporting API</span></span>

<span data-ttu-id="65b6d-104">Usługa Azure Active Directory oferuje szerokiej gamy raportów.</span><span class="sxs-lookup"><span data-stu-id="65b6d-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="65b6d-105">Hello dane z tych raportów mogą być bardzo przydatne tooyour aplikacji, takich jak systemów SIEM, inspekcji i narzędzia do analizy biznesowej.</span><span class="sxs-lookup"><span data-stu-id="65b6d-105">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="65b6d-106">interfejsy API zapewniają dostęp programistyczny toohello danych za pomocą zestawu opartego na interfejsie REST API raportowania Hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65b6d-106">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="65b6d-107">Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.</span><span class="sxs-lookup"><span data-stu-id="65b6d-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="65b6d-108">Ten artykuł zawiera informacje hello należy tooget wprowadzenie do raportowania hello Azure AD interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="65b6d-108">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="65b6d-109">W następnej sekcji hello znajdziesz więcej informacji o używaniu hello inspekcji i logowania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="65b6d-109">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> 

<span data-ttu-id="65b6d-110">Często zadawane pytania, przeczytaj nasze [— często zadawane pytania](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="65b6d-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="65b6d-111">W przypadku problemów skontaktuj się z [pliku biletu pomocy technicznej](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="65b6d-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="65b6d-112">Mapa uczenia się</span><span class="sxs-lookup"><span data-stu-id="65b6d-112">Learning map</span></span>
1. <span data-ttu-id="65b6d-113">**Przygotowanie** — przed próbek interfejsu API można przetestować, należy toocomplete hello [interfejsu API raportowania hello Azure AD tooaccess wymagania wstępne](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="65b6d-113">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="65b6d-114">**Eksploruj** -uzyskać pierwszy wrażenie hello raportowania interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="65b6d-114">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="65b6d-115">Przy użyciu hello próbek dla inspekcji hello interfejsu API</span><span class="sxs-lookup"><span data-stu-id="65b6d-115">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="65b6d-116">Przy użyciu próbek hello interfejsu API raport aktywności logowania hello</span><span class="sxs-lookup"><span data-stu-id="65b6d-116">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="65b6d-117">**Dostosowywanie** — tworzenie własnych rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="65b6d-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="65b6d-118">Przy użyciu hello odwołanie do API inspekcji</span><span class="sxs-lookup"><span data-stu-id="65b6d-118">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="65b6d-119">Dokumentacja interfejsu API przy użyciu hello raport aktywności logowania</span><span class="sxs-lookup"><span data-stu-id="65b6d-119">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="65b6d-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65b6d-120">Next Steps</span></span>
<span data-ttu-id="65b6d-121">Jeśli zastanawiasz się toosee wszystkie dostępne usługi Azure AD Graph punkty końcowe interfejsu API, użyj tego linku: [https://graph.windows.net/tenant-name/activities/$ metadanych? api-version = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="65b6d-121">If you are curious toosee all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

