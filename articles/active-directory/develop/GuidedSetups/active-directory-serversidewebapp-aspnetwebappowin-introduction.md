---
title: "aaaAzure AD v2 ASP.NET Web Server wprowadzenie — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Implementowanie logowania firmy Microsoft dla rozwiązania ASP.NET z aplikacji opartych na przeglądarce sieci web tradycyjnych przy użyciu standardowego protokołu OpenID Connect"
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="5c62f-103">Dodaj logowanie do aplikacji sieci web ASP.NET tooan firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="5c62f-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="5c62f-104">W tym przewodniku pokazano, jak tooimplement logowania z firmą Microsoft za pomocą rozwiązania ASP.NET MVC z tradycyjnego aplikacji sieci web opartej na przeglądarce przy użyciu protokołu OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="5c62f-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="5c62f-105">Na końcu hello tego przewodnika aplikacja zostanie logowania może tooaccept ins osobiste konta (w tym outlook.com, live.com i inne), a także pracować i służbowych z firmy lub organizacji, która ma być zintegrowane z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5c62f-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="5c62f-106">W tym przewodniku wymaga programu Visual Studio 2015 Update 3 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="5c62f-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="5c62f-107">Nie masz?</span><span class="sxs-lookup"><span data-stu-id="5c62f-107">Don’t have it?</span></span>  [<span data-ttu-id="5c62f-108">Bezpłatnie pobrać Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="5c62f-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="5c62f-109">Jak działa w tym przewodniku</span><span class="sxs-lookup"><span data-stu-id="5c62f-109">How this guide works</span></span>

![Jak działa w tym przewodniku](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="5c62f-111">W tym przewodniku opiera się na scenariuszu hello których przeglądarką uzyskuje dostęp do witryny sieci web ASP.NET, żądanie tooauthenticate użytkownika, klikając przycisk logowania.</span><span class="sxs-lookup"><span data-stu-id="5c62f-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="5c62f-112">W tym scenariuszu większość strony sieci web hello hello pracy toorender występuje na powitania po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="5c62f-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="5c62f-113">Biblioteki</span><span class="sxs-lookup"><span data-stu-id="5c62f-113">Libraries</span></span>

<span data-ttu-id="5c62f-114">W tym przewodniku używa hello następujące biblioteki:</span><span class="sxs-lookup"><span data-stu-id="5c62f-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="5c62f-115">Biblioteka</span><span class="sxs-lookup"><span data-stu-id="5c62f-115">Library</span></span>|<span data-ttu-id="5c62f-116">Opis</span><span class="sxs-lookup"><span data-stu-id="5c62f-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="5c62f-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="5c62f-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="5c62f-118">Oprogramowanie pośredniczące, umożliwiający OpenIdConnect toouse aplikacji uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="5c62f-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="5c62f-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="5c62f-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="5c62f-120">Oprogramowanie pośredniczące, umożliwiającą sesję użytkownika toomaintain dla aplikacji przy użyciu plików cookie</span><span class="sxs-lookup"><span data-stu-id="5c62f-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="5c62f-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="5c62f-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="5c62f-122">Umożliwia aplikacji OWIN toorun w usługach IIS za pomocą potoku żądania ASP.NET hello</span><span class="sxs-lookup"><span data-stu-id="5c62f-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|

