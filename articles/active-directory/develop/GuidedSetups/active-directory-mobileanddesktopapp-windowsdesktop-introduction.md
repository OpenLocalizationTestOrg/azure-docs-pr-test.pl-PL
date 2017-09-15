---
title: "Usługi Azure AD v2 Windows Desktop pobieranie rozpoczęte — wprowadzenie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4a695c00fce4deb02261ba58ec95469746bb1486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="call-the-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="a87ef-103">Wywoływanie Microsoft Graph API z pulpitu aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a87ef-103">Call the Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="a87ef-104">W tym przewodniku pokazano, jak natywnych aplikacji .NET pulpitu systemu Windows (XAML) można uzyskać token dostępu i wywołania interfejsu API programu Graph firmy Microsoft lub innych interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a87ef-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="a87ef-105">Na końcu tego przewodnika aplikacja będzie mogła wywołać interfejs API chronionych przy użyciu konta osobiste (w tym outlook.com, live.com i inne) oraz pracy i służbowych z firmy lub organizacji, która ma usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a87ef-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="a87ef-106">W tym przewodniku wymaga programu Visual Studio 2015 Update 3 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="a87ef-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="a87ef-107">Nie masz?</span><span class="sxs-lookup"><span data-stu-id="a87ef-107">Don’t have it?</span></span> [<span data-ttu-id="a87ef-108">Bezpłatnie pobrać Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="a87ef-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="a87ef-109">Jak działa w tym przewodniku</span><span class="sxs-lookup"><span data-stu-id="a87ef-109">How this guide works</span></span>

![Jak działa w tym przewodniku](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="a87ef-111">Przykładowa aplikacja utworzone przez ten przewodnik umożliwia aplikacji pulpitu systemu Windows do zapytania interfejsu API programu Microsoft Graph i interfejsu API sieci Web, który akceptuje tokeny od punktu końcowego w wersji 2 usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a87ef-111">The sample application created by this guide enables a Windows Desktop Application to query Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="a87ef-112">W tym scenariuszu token zostanie dodany do żądań HTTP za pośrednictwem nagłówek autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="a87ef-112">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="a87ef-113">Token nabycia i odnawiania jest obsługiwany przez bibliotekę uwierzytelniania firmy Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="a87ef-113">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="a87ef-114">Obsługa tokenów nabycia do uzyskiwania dostępu do chronionego interfejsów API sieci Web</span><span class="sxs-lookup"><span data-stu-id="a87ef-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="a87ef-115">Po użytkownik jest uwierzytelniany, przykładowa aplikacja odbiera token, który może służyć do badania interfejsu API programu Microsoft Graph i interfejsu API sieci Web zabezpieczonych przez usługi Microsoft Azure Active Directory w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="a87ef-115">After the user authenticates, the sample application receives a token that can be used to query Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="a87ef-116">Interfejsy API, takich jak Microsoft Graph wymagają tokenu dostępu, aby umożliwić uzyskiwanie dostępu do określonych zasobów — na przykład do odczytu profilu użytkownika, kalendarz dostęp użytkownika lub Wyślij wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="a87ef-116">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="a87ef-117">Aplikacja może żądać tokenu dostępu przy użyciu MSAL dostępu do tych zasobów, określając zakresy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a87ef-117">Your application can request an access token using MSAL to access these resources by specifying API scopes.</span></span> <span data-ttu-id="a87ef-118">Ten token dostępu jest dodawane do nagłówka HTTP autoryzacji dla każdego wywołania wykonane w stosunku do chronionego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a87ef-118">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span> 

<span data-ttu-id="a87ef-119">MSAL zarządza buforowanie i odświeżanie tokenów dostępu, więc nie trzeba aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a87ef-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="a87ef-120">Pakiety NuGet</span><span class="sxs-lookup"><span data-stu-id="a87ef-120">NuGet Packages</span></span>

<span data-ttu-id="a87ef-121">W tym przewodniku używa następujących pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="a87ef-121">This guide uses the following NuGet packages:</span></span>

|<span data-ttu-id="a87ef-122">Biblioteka</span><span class="sxs-lookup"><span data-stu-id="a87ef-122">Library</span></span>|<span data-ttu-id="a87ef-123">Opis</span><span class="sxs-lookup"><span data-stu-id="a87ef-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="a87ef-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="a87ef-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="a87ef-125">Biblioteka uwierzytelniania firmy Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="a87ef-125">Microsoft Authentication Library (MSAL)</span></span>|

