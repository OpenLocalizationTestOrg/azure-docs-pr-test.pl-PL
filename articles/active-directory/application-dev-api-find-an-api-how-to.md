---
title: toofind aaaHow interfejsu API wymagane dla aplikacji utworzonych niestandardowych | Dokumentacja firmy Microsoft
description: "Jak należy tooaccess określony interfejs API w niestandardowe uprawnienia hello tooconfigure opracowała aplikację usługi Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="f70a6-103">Jak toofind określonego interfejsu API wymagane dla aplikacji utworzonych niestandardowych</span><span class="sxs-lookup"><span data-stu-id="f70a6-103">How toofind a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="f70a6-104">TooAPIs dostępu wymagają konfiguracji, zakresów dostępu i ról.</span><span class="sxs-lookup"><span data-stu-id="f70a6-104">Access tooAPIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="f70a6-105">Jeśli chcesz tooexpose zasobów aplikacji sieci web API tooclient aplikacji, należy tooconfigure zakresów dostępu i role dla hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f70a6-105">If you want tooexpose your resource application web APIs tooclient applications, you need tooconfigure access scopes and roles for hello API.</span></span> <span data-ttu-id="f70a6-106">Jeśli chcesz tooaccess aplikacji klienta interfejsu API sieci web, należy tooconfigure uprawnienia tooaccess hello API w rejestracji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f70a6-106">If you want a client application tooaccess a web API, you need tooconfigure permissions tooaccess hello API in hello app registration.</span></span>

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a><span data-ttu-id="f70a6-107">Konfigurowanie zasobów aplikacji tooexpose interfejsów API sieci web</span><span class="sxs-lookup"><span data-stu-id="f70a6-107">Configuring a resource application tooexpose web APIs</span></span>

<span data-ttu-id="f70a6-108">Gdy uwidacznia interfejs API, sieci web hello interfejsu API można wyświetlić w hello **wybierz interfejs API** listy podczas dodawania rejestracji aplikacji tooan uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="f70a6-108">When you expose your web API, hello API be displayed in hello **Select an API** list when adding permissions tooan app registration.</span></span> <span data-ttu-id="f70a6-109">zakresy dostępu tooadd, wykonaj kroki hello opisane w temacie [Dodawanie dostępu zakresów aplikacji zasobów tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="f70a6-109">tooadd access scopes, follow hello steps outlined in [adding access scopes tooyour resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-tooaccess-web-apis"></a><span data-ttu-id="f70a6-110">Konfigurowanie klienta aplikacji tooaccess interfejsów API sieci web</span><span class="sxs-lookup"><span data-stu-id="f70a6-110">Configuring a client application tooaccess web APIs</span></span>

<span data-ttu-id="f70a6-111">Po dodaniu rejestracji aplikacji tooyour uprawnienia można **dodać dostępu do interfejsu API** tooexposed interfejsów API sieci web.</span><span class="sxs-lookup"><span data-stu-id="f70a6-111">When you add permissions tooyour app registration, you can **add API access** tooexposed web APIs.</span></span> <span data-ttu-id="f70a6-112">tooaccess interfejsów API sieci web, wykonaj czynności hello opisane w temacie [dodać interfejsów API sieci web tooaccess poświadczeń lub uprawnienia](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="f70a6-112">tooaccess web APIs, follow hello steps outlined in [add credentials or permissions tooaccess web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f70a6-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f70a6-113">Next steps</span></span>

-   <span data-ttu-id="f70a6-114">[Integrating applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications) (Integrowanie aplikacji za pomocą usługi Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="f70a6-114">[Integrating applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)</span></span>

-   [<span data-ttu-id="f70a6-115">Opis manifestu aplikacji hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f70a6-115">Understanding hello Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


