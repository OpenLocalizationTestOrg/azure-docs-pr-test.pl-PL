---
title: "aaaAzure AD v2 JS SPA instrukcje konfiguracji — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Jak aplikacje JavaScript SPA można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="80105-103">Wywołanie interfejsu API Graph usługi Microsoft hello z JavaScript jednej strony aplikacji JEDNOSTRONICOWEJ</span><span class="sxs-lookup"><span data-stu-id="80105-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="80105-104">W tym przewodniku pokazano, jak JavaScript jednej strony aplikacji JEDNOSTRONICOWEJ mógł zalogować się w osobistym, pracy i kont służbowych uzyskać token dostępu i wywołania interfejsu API Graph usługi Microsoft hello lub innych interfejsów API, które wymagają tokenów dostępu z hello punktu końcowego w wersji 2 usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="80105-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="80105-105">Jak działa w tym przewodniku</span><span class="sxs-lookup"><span data-stu-id="80105-105">How this guide works</span></span>

![Jak działa hello przykładowej aplikacji wygenerowane przez ten przewodnik](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="80105-107">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="80105-107">More Information</span></span>

<span data-ttu-id="80105-108">Witaj przykładowej aplikacji utworzonych przez ten przewodnik umożliwia hello tooquery JavaScript SPA interfejsu API programu Microsoft Graph lub interfejsu API sieci Web, który akceptuje tokeny od punktu końcowego w wersji 2 usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="80105-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="80105-109">W tym scenariuszu po użytkownika logowania, token dostępu jest tooHTTP żądanego i dodać żądań za pośrednictwem hello nagłówek autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="80105-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="80105-110">Token nabycia i odnawiania są obsługiwane przez hello biblioteki uwierzytelniania firmy Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="80105-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="80105-111">Biblioteki</span><span class="sxs-lookup"><span data-stu-id="80105-111">Libraries</span></span>

<span data-ttu-id="80105-112">W tym przewodniku używa hello następujące biblioteki:</span><span class="sxs-lookup"><span data-stu-id="80105-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="80105-113">Biblioteka</span><span class="sxs-lookup"><span data-stu-id="80105-113">Library</span></span>|<span data-ttu-id="80105-114">Opis</span><span class="sxs-lookup"><span data-stu-id="80105-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="80105-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="80105-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="80105-116">Biblioteka uwierzytelniania firmy Microsoft dla podglądu JavaScript</span><span class="sxs-lookup"><span data-stu-id="80105-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="80105-117">*msal.js* hello cele *punktu końcowego w wersji 2 usługi Azure Active Directory* — który umożliwia toosign konta osobiste, szkolnego i pracy w i uzyskać tokeny.</span><span class="sxs-lookup"><span data-stu-id="80105-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="80105-118">Witaj *punktu końcowego w wersji 2 usługi Azure Active Directory* ma [pewne ograniczenia](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="80105-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="80105-119">Jeśli interesuje Cię tylko na kontach służbowych, jak i szkoły, użyj *adal.js* i hello *punktu końcowego V1*.</span><span class="sxs-lookup"><span data-stu-id="80105-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="80105-120">toounderstand różnice między punktami końcowymi v1 i v2 hello odczytu hello [porównania v1 v2](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="80105-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
