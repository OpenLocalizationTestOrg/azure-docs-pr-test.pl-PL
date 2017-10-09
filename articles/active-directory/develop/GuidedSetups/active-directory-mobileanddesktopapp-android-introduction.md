---
title: "aaaAzure AD w wersji 2 dla systemu Android wprowadzenie — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Jak uzyskać token dostępu i wywołania interfejsu API programu Microsoft Graph lub interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory aplikacji systemu Android"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="da0e8-103">Wywołanie interfejsu API Graph usługi Microsoft hello z aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="da0e8-103">Call hello Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="da0e8-104">W tym przewodniku pokazano, jak natywnych aplikacji systemu Android mogą pobrać token dostępu i wywołania interfejsu API programu Graph firmy Microsoft lub innych interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da0e8-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="da0e8-105">Na końcu hello tego przewodnika, aplikacji będzie można toocall stanie interfejs API chronionych przy użyciu konta osobiste (w tym outlook.com, live.com i inne), a także pracy i kont służbowych z firmy lub organizacji, która ma usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da0e8-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="da0e8-106">Jak działa w tym przykładzie</span><span class="sxs-lookup"><span data-stu-id="da0e8-106">How this sample works</span></span>
![Jak działa w tym przykładzie](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="da0e8-108">Przykładowe Hello utworzone przez ten przewodnik jest oparty na scenariusz, w przypadku aplikacji systemu Android używane tooquery interfejsu API sieci Web, który akceptuje tokeny od usługi Azure Active Directory v2 punktu końcowego — w takim przypadku interfejsu API programu Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="da0e8-108">hello sample created by this guide is based on a scenario where an Android application is used tooquery a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="da0e8-109">W tym scenariuszu token jest dodawana tooHTTP żądań za pośrednictwem hello nagłówek autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="da0e8-109">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="da0e8-110">Token nabycia i odnawiania jest obsługiwany przez hello biblioteki uwierzytelniania firmy Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="da0e8-110">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="da0e8-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="da0e8-111">Pre-requisites</span></span>
* <span data-ttu-id="da0e8-112">Ten przewodnik instalacji koncentruje się na Android Studio, ale dopuszczalne jest również inne środowiska programowania aplikacji dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="da0e8-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="da0e8-113">Zestaw SDK systemu android 21 lub nowszy jest wymagany (zalecane 25 zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="da0e8-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="da0e8-114">Google Chrome lub przeglądarki sieci web przy użyciu karty niestandardowy jest wymagany dla tej wersji programu Microsoft biblioteki uwierzytelniania (MSAL) dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="da0e8-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="da0e8-115">Uwaga: Google Chrome nie jest uwzględniony w Visual Studio Emulator for Android.</span><span class="sxs-lookup"><span data-stu-id="da0e8-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="da0e8-116">Zalecamy tootest ten kod na emulatorze z interfejsu API 25 lub obraz z interfejsu API 21 lub nowszego z Google Chrome zainstalował.</span><span class="sxs-lookup"><span data-stu-id="da0e8-116">We recommend you tootest this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a><span data-ttu-id="da0e8-117">Jak toohandle token tooaccess nabycia chronionego interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="da0e8-117">How toohandle token acquisition tooaccess a protected Web API</span></span>

<span data-ttu-id="da0e8-118">Po uwierzytelniania użytkownika hello hello Przykładowa aplikacja odbiera token, który może być używane tooquery interfejsu API programu Microsoft Graph i interfejsu API sieci Web zabezpieczonych przez usługi Microsoft Azure Active Directory w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="da0e8-118">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="da0e8-119">Interfejsy API, takich jak Microsoft Graph wymagają tooallow tokenu dostępu podczas uzyskiwania dostępu do określonych zasobów — na przykład tooread profilu użytkownika, dostęp do kalendarza użytkownika lub Wyślij wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="da0e8-119">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="da0e8-120">Aplikacja może wysłać żądanie tokenu dostępu przy użyciu MSAL tooaccess tych zasobów za pośrednictwem interfejsu API zakresów.</span><span class="sxs-lookup"><span data-stu-id="da0e8-120">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="da0e8-121">Ten token dostępu jest dodany toohello nagłówek autoryzacji HTTP dla każdego wywołania wykonane w stosunku hello chroniony zasób.</span><span class="sxs-lookup"><span data-stu-id="da0e8-121">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="da0e8-122">MSAL zarządza buforowanie i odświeżanie tokenów dostępu, więc nie trzeba aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da0e8-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="da0e8-123">Biblioteki</span><span class="sxs-lookup"><span data-stu-id="da0e8-123">Libraries</span></span>

<span data-ttu-id="da0e8-124">W tym przewodniku używa hello następujące biblioteki:</span><span class="sxs-lookup"><span data-stu-id="da0e8-124">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="da0e8-125">Biblioteka</span><span class="sxs-lookup"><span data-stu-id="da0e8-125">Library</span></span>|<span data-ttu-id="da0e8-126">Opis</span><span class="sxs-lookup"><span data-stu-id="da0e8-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="da0e8-127">COM.microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="da0e8-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="da0e8-128">Biblioteka uwierzytelniania firmy Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="da0e8-128">Microsoft Authentication Library (MSAL)</span></span>|
