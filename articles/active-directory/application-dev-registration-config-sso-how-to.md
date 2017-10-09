---
title: "tooconfigure aaaHow nowej aplikacji wielodostępnych | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure logowanie jednokrotne dla aplikacji niestandardowej opracowywania i rejestrowanie w usłudze Azure AD."
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
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a><span data-ttu-id="1c393-103">Jak tooconfigure nowej aplikacji wieloma dzierżawcami</span><span class="sxs-lookup"><span data-stu-id="1c393-103">How tooconfigure a new multi-tenant application</span></span>

<span data-ttu-id="1c393-104">Włączanie federacyjnych rejestracji jednokrotnej (SSO) w aplikacji jest automatycznie włączone podczas federowania za pośrednictwem usługi Azure AD dla OpenID Connect SAML 2.0 i WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="1c393-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="1c393-105">Jeśli użytkownicy końcowi toosign pomimo już o istniejącej sesji z usługą Azure AD, prawdopodobnie aplikacji może być niepoprawnie skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="1c393-105">If your end users are having toosign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="1c393-106">Jeśli korzystasz z biblioteki ADAL/MSAL, upewnij się, masz **PromptBehavior** ustawić także**automatycznie** zamiast **zawsze**.</span><span class="sxs-lookup"><span data-stu-id="1c393-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set too**Auto** rather than **Always**.</span></span>

* <span data-ttu-id="1c393-107">Jeśli tworzysz aplikację mobilną, może być konieczne dodatkowe konfiguracje tooenable obsługiwanych przez brokera lub z systemem innym niż nieobsługiwana przez brokera logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="1c393-107">If you’re building a mobile app, you may need additional configurations tooenable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="1c393-108">Dla systemu Android, zobacz [włączanie dla wielu aplikacji rejestracji Jednokrotnej w systemie Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="1c393-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="1c393-109">Dla systemu iOS, zobacz [włączanie dla wielu aplikacji rejestracji Jednokrotnej w systemie iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="1c393-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c393-110">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c393-110">Next steps</span></span>

[<span data-ttu-id="1c393-111">Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="1c393-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="1c393-112">Włączanie Cross logowania jednokrotnego aplikacji w systemie Android</span><span class="sxs-lookup"><span data-stu-id="1c393-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="1c393-113">Włączanie dla wielu aplikacji rejestracji Jednokrotnej w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="1c393-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="1c393-114">Integrowanie aplikacji tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="1c393-114">Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="1c393-115">Permissioning dla AzureAD w wersji 2.0 i zgody zbieżność aplikacji</span><span class="sxs-lookup"><span data-stu-id="1c393-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="1c393-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="1c393-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
