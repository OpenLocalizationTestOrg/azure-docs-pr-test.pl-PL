---
title: "aaaAzure AD v2 Windows Desktop wprowadzenie — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Jak aplikacje .NET pulpitu systemu Windows (XAML) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="02d2b-103">Wywołanie interfejsu API Graph usługi Microsoft hello z aplikacji pulpitu systemu Windows</span><span class="sxs-lookup"><span data-stu-id="02d2b-103">Call hello Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="02d2b-104">W tym przewodniku pokazano, jak natywnych aplikacji .NET pulpitu systemu Windows (XAML) można uzyskać token dostępu i wywołania interfejsu API programu Graph firmy Microsoft lub innych interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="02d2b-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="02d2b-105">Na końcu hello tego przewodnika, aplikacji będzie można toocall stanie interfejs API chronionych przy użyciu konta osobiste (w tym outlook.com, live.com i inne), a także pracy i kont służbowych z firmy lub organizacji, która ma usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="02d2b-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="02d2b-106">W tym przewodniku wymaga programu Visual Studio 2015 Update 3 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="02d2b-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="02d2b-107">Nie masz?</span><span class="sxs-lookup"><span data-stu-id="02d2b-107">Don’t have it?</span></span> [<span data-ttu-id="02d2b-108">Bezpłatnie pobrać Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="02d2b-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="02d2b-109">Jak działa w tym przewodniku</span><span class="sxs-lookup"><span data-stu-id="02d2b-109">How this guide works</span></span>

![Jak działa w tym przewodniku](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="02d2b-111">Witaj przykładowej aplikacji utworzonych przez ten przewodnik umożliwia tooquery Windows Desktop aplikacji interfejsu API programu Microsoft Graph lub interfejsu API sieci Web, który akceptuje tokeny od punktu końcowego w wersji 2 usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="02d2b-111">hello sample application created by this guide enables a Windows Desktop Application tooquery Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="02d2b-112">W tym scenariuszu token jest dodawana tooHTTP żądań za pośrednictwem hello nagłówek autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="02d2b-112">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="02d2b-113">Token nabycia i odnawiania jest obsługiwany przez hello biblioteki uwierzytelniania firmy Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="02d2b-113">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="02d2b-114">Obsługa tokenów nabycia do uzyskiwania dostępu do chronionego interfejsów API sieci Web</span><span class="sxs-lookup"><span data-stu-id="02d2b-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="02d2b-115">Po uwierzytelniania użytkownika hello hello Przykładowa aplikacja odbiera token, który może być używane tooquery interfejsu API programu Microsoft Graph i interfejsu API sieci Web zabezpieczonych przez usługi Microsoft Azure Active Directory w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="02d2b-115">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="02d2b-116">Interfejsy API, takich jak Microsoft Graph wymagają tooallow tokenu dostępu podczas uzyskiwania dostępu do określonych zasobów — na przykład tooread profilu użytkownika, dostęp do kalendarza użytkownika lub Wyślij wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="02d2b-116">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="02d2b-117">Aplikacja może wysłać żądanie tokenu dostępu przy użyciu MSAL tooaccess tych zasobów za pośrednictwem interfejsu API zakresów.</span><span class="sxs-lookup"><span data-stu-id="02d2b-117">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="02d2b-118">Ten token dostępu jest dodany toohello nagłówek autoryzacji HTTP dla każdego wywołania wykonane w stosunku hello chroniony zasób.</span><span class="sxs-lookup"><span data-stu-id="02d2b-118">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="02d2b-119">MSAL zarządza buforowanie i odświeżanie tokenów dostępu, więc nie trzeba aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02d2b-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="02d2b-120">Pakiety NuGet</span><span class="sxs-lookup"><span data-stu-id="02d2b-120">NuGet Packages</span></span>

<span data-ttu-id="02d2b-121">W tym przewodniku używa powitania po pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="02d2b-121">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="02d2b-122">Biblioteka</span><span class="sxs-lookup"><span data-stu-id="02d2b-122">Library</span></span>|<span data-ttu-id="02d2b-123">Opis</span><span class="sxs-lookup"><span data-stu-id="02d2b-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="02d2b-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="02d2b-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="02d2b-125">Biblioteka uwierzytelniania firmy Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="02d2b-125">Microsoft Authentication Library (MSAL)</span></span>|

