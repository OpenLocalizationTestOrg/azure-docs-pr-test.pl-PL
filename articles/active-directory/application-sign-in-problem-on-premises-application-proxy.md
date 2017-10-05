---
title: "Problemy przy logowaniu do aplikacji lokalnych przy użyciu serwera proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie typowych problemów, które muszą ponieść, gdy nie można zalogować się do aplikacji lokalnych zintegrowane z usługą Azure AD przy użyciu serwera Proxy aplikacji usługi AD platformy Azure"
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
ms.openlocfilehash: 5687f789355cc9769d26b53e98486bb213c66419
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-on-premises-application-using-the-azure-ad-application-proxy"></a><span data-ttu-id="ed1e4-103">Problemy przy logowaniu do aplikacji lokalnych przy użyciu serwera proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed1e4-103">Problems signing in to an on-premises application using the Azure AD application proxy</span></span>

<span data-ttu-id="ed1e4-104">Jeśli występują problemy przy logowaniu do aplikacji lokalnych, możesz wypróbować, wykonując poniższe czynności w celu rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="ed1e4-104">If you are having problems signing in an on-premises application, you can try following the steps below to resolving your problem.</span></span>

## <a name="i-can-load-my-application-but-something-on-the-page-looks-broken"></a><span data-ttu-id="ed1e4-105">I załadować mojej aplikacji, ale coś na stronie wygląda przerwany</span><span class="sxs-lookup"><span data-stu-id="ed1e4-105">I can load my application, but something on the page looks broken</span></span>

<span data-ttu-id="ed1e4-106">Następujące dokumenty mogą ułatwić rozwiązanie niektórych często spotykanych problemów tego typu.</span><span class="sxs-lookup"><span data-stu-id="ed1e4-106">The following documents can help you to resolve some of the most common issues in this category.</span></span>

  * [<span data-ttu-id="ed1e4-107">Mogę uzyskać dostęp do swojej aplikacji, ale strona aplikacji nie jest wyświetlana poprawnie</span><span class="sxs-lookup"><span data-stu-id="ed1e4-107">I can get to my application, but the application page isn't displaying correctly</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-appearance-broken-problem/)
  * [<span data-ttu-id="ed1e4-108">Mogę uzyskać dostęp do swojej aplikacji, ale jej załadowanie trwa zbyt długo</span><span class="sxs-lookup"><span data-stu-id="ed1e4-108">I can get to my application, but the application takes too long to load</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-load-speed-problem/)
  * [<span data-ttu-id="ed1e4-109">Mogę uzyskać dostęp do swojej aplikacji, ale linki na stronie aplikacji nie działają</span><span class="sxs-lookup"><span data-stu-id="ed1e4-109">I can get to my application, but the links on the application page do not work</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-links-broken-problem/)

## <a name="im-having-a-connectivity-problem-my-application"></a><span data-ttu-id="ed1e4-110">Mam problem z połączeniem Moja aplikacja</span><span class="sxs-lookup"><span data-stu-id="ed1e4-110">I'm having a connectivity problem my application</span></span>
  <span data-ttu-id="ed1e4-111">Następujące dokumenty mogą ułatwić rozwiązanie niektórych często spotykanych problemów tego typu.</span><span class="sxs-lookup"><span data-stu-id="ed1e4-111">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="ed1e4-112">Nie wiem, jakie porty otworzyć dla swojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ed1e4-112">I don't know what ports to open for my application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connectivity-ports-how-to/)
  * [<span data-ttu-id="ed1e4-113">Wystąpił problem spowodowany brakiem działającego łącznika w grupie łączników dla mojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ed1e4-113">I encountered a problem because there was no working connector in a connector group for my application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connectivity-no-working-connector/)

## <a name="im-having-a-problem-configuring-the-azure-ad-application-proxy-in-the-admin-portal"></a><span data-ttu-id="ed1e4-114">Mam problem podczas konfiguracji serwera Proxy aplikacji usługi AD platformy Azure w portalu administracyjnym</span><span class="sxs-lookup"><span data-stu-id="ed1e4-114">I'm having a problem configuring the Azure AD Application Proxy in the admin portal</span></span>
  <span data-ttu-id="ed1e4-115">Następujące dokumenty mogą ułatwić rozwiązanie niektórych często spotykanych problemów tego typu.</span><span class="sxs-lookup"><span data-stu-id="ed1e4-115">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="ed1e4-116">Mam problem z konfiguracją aplikacji serwera proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="ed1e4-116">I am having difficulty configuring an application Proxy application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-how-to/)
  * [<span data-ttu-id="ed1e4-117">Nie wiem, jak skonfigurować logowanie jednokrotne do aplikacji serwera proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="ed1e4-117">I don't know how to configure single sign-on to my application Proxy application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-sso-how-to/)
  * [<span data-ttu-id="ed1e4-118">Wystąpił problem podczas tworzenia aplikacji w portalu administracyjnym</span><span class="sxs-lookup"><span data-stu-id="ed1e4-118">I encountered a problem when creating my application in admin portal</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-problem/)

## <a name="im-having-a-problem-setting-up-back-end-authentication-to-my-application"></a><span data-ttu-id="ed1e4-119">Wystąpił problem podczas konfigurowania uwierzytelniania zaplecza do mojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ed1e4-119">I'm having a problem setting up back-end authentication to my application</span></span>
  <span data-ttu-id="ed1e4-120">Następujące dokumenty mogą ułatwić rozwiązanie niektórych często spotykanych problemów tego typu.</span><span class="sxs-lookup"><span data-stu-id="ed1e4-120">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="ed1e4-121">Nie wiem, jak skonfigurować ograniczone delegowanie protokołu Kerberos</span><span class="sxs-lookup"><span data-stu-id="ed1e4-121">I don't know how to configure Kerberos Constrained Delegation</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-back-end-kerberos-constrained-delegation-how-to/)
  * [<span data-ttu-id="ed1e4-122">Nie wiem, jak skonfigurować współdziałanie swojej aplikacji z usługą PingAccess</span><span class="sxs-lookup"><span data-stu-id="ed1e4-122">I don't know how to configure my application with PingAccess</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-back-end-ping-access-how-to/)

## <a name="im-having-a-problem-when-signing-in-to-my-application"></a><span data-ttu-id="ed1e4-123">Wystąpił problem podczas logowania do mojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ed1e4-123">I'm having a problem when signing in to my application</span></span>
  <span data-ttu-id="ed1e4-124">Następujące dokumenty mogą ułatwić rozwiązanie niektórych często spotykanych problemów tego typu.</span><span class="sxs-lookup"><span data-stu-id="ed1e4-124">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="ed1e4-125">Występuje błąd „Can't Access this Corporate Application” (Nie można uzyskać dostępu do tej aplikacji firmowej)</span><span class="sxs-lookup"><span data-stu-id="ed1e4-125">I get a "Can't Access this Corporate Application" error</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-sign-in-bad-gateway-timeout-error/)

## <a name="im-having-a-problem-with-the-application-proxy-agent-connector"></a><span data-ttu-id="ed1e4-126">Mam problem z łącznikiem agenta Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="ed1e4-126">I'm having a problem with the Application Proxy Agent Connector</span></span>
  <span data-ttu-id="ed1e4-127">Następujące dokumenty mogą ułatwić rozwiązanie niektórych często spotykanych problemów tego typu.</span><span class="sxs-lookup"><span data-stu-id="ed1e4-127">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="ed1e4-128">Mam problemy z instalacją łącznika agenta serwera proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="ed1e4-128">I am having issues installing the Application Proxy Agent Connector </span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connector-installation-problem/)

## <a name="next-steps"></a><span data-ttu-id="ed1e4-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ed1e4-129">Next steps</span></span>
[<span data-ttu-id="ed1e4-130">Jak zapewnić bezpieczny zdalny dostęp do aplikacji lokalnych</span><span class="sxs-lookup"><span data-stu-id="ed1e4-130">How to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
