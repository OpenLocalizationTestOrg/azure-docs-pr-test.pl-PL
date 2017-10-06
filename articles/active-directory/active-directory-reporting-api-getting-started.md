---
title: aaaGetting wprowadzenie do raportowania interfejsu API hello Azure AD w portalu klasycznym hello Azure AD | Dokumentacja firmy Microsoft
description: "Jak tooget wprowadzenie hello interfejsem API raportowania usługi Azure Active Directory"
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
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a><span data-ttu-id="1ab5c-103">Wprowadzenie do korzystania z hello Azure Active Directory raportowania interfejsu API w portalu klasycznym hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ab5c-103">Getting started with hello Azure Active Directory reporting API on hello Azure AD classic portal</span></span>
<span data-ttu-id="1ab5c-104">*Ten temat jest częścią hello [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="1ab5c-104">*This topic is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="1ab5c-105">Usługa Azure Active Directory oferuje szerokiej gamy raportów.</span><span class="sxs-lookup"><span data-stu-id="1ab5c-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="1ab5c-106">Hello dane z tych raportów mogą być bardzo przydatne tooyour aplikacji, takich jak systemów SIEM, inspekcji i narzędzia do analizy biznesowej.</span><span class="sxs-lookup"><span data-stu-id="1ab5c-106">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="1ab5c-107">interfejsy API zapewniają dostęp programistyczny toohello danych za pomocą zestawu opartego na interfejsie REST API raportowania Hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ab5c-107">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="1ab5c-108">Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.</span><span class="sxs-lookup"><span data-stu-id="1ab5c-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="1ab5c-109">Ten artykuł zawiera informacje hello należy tooget wprowadzenie do raportowania hello Azure AD interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="1ab5c-109">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="1ab5c-110">W następnej sekcji hello znajdziesz więcej informacji o używaniu hello inspekcji i logowania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="1ab5c-110">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> <span data-ttu-id="1ab5c-111">Dla wszystkich innych interfejsów API, zobacz hello [raportów usługi Azure AD i events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="1ab5c-111">For all other APIs, see hello [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="1ab5c-112">Pytania, problemy lub opinie, skontaktuj się z [Pomoc raportowania usługi AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1ab5c-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="1ab5c-113">Mapa uczenia się</span><span class="sxs-lookup"><span data-stu-id="1ab5c-113">Learning map</span></span>
1. <span data-ttu-id="1ab5c-114">**Przygotowanie** — przed próbek interfejsu API można przetestować, należy toocomplete hello [interfejsu API raportowania hello Azure AD tooaccess wymagania wstępne](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="1ab5c-114">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="1ab5c-115">**Eksploruj** -uzyskać pierwszy wrażenie hello raportowania interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="1ab5c-115">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="1ab5c-116">Przy użyciu hello próbek dla inspekcji hello interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1ab5c-116">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="1ab5c-117">Przy użyciu próbek hello interfejsu API raport aktywności logowania hello</span><span class="sxs-lookup"><span data-stu-id="1ab5c-117">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="1ab5c-118">**Dostosowywanie** — tworzenie własnych rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="1ab5c-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="1ab5c-119">Przy użyciu hello odwołanie do API inspekcji</span><span class="sxs-lookup"><span data-stu-id="1ab5c-119">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="1ab5c-120">Dokumentacja interfejsu API przy użyciu hello raport aktywności logowania</span><span class="sxs-lookup"><span data-stu-id="1ab5c-120">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="1ab5c-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1ab5c-121">Next Steps</span></span>
<span data-ttu-id="1ab5c-122">Jeśli zastanawiasz się toosee hello wszystkie dostępne punkty końcowe interfejsu API Azure AD Graph przechodząc zbyt[https://graph.windows.net/tenant-name/reports/$ metadanych? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="1ab5c-122">If you are curious toosee all of hello available Azure AD Graph API endpoints by navigating too[https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

