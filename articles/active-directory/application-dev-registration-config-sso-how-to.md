---
title: "Jak skonfigurować nową aplikację wielodostępne | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować logowanie jednokrotne dla aplikacji niestandardowej opracowywania i rejestrowanie w usłudze Azure AD."
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
ms.openlocfilehash: 0fdc58d82d9cd2e7edac33cc5af4b98d2fd06c56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-a-new-multi-tenant-application"></a><span data-ttu-id="2dbe1-103">Jak skonfigurować nową aplikację wieloma dzierżawcami</span><span class="sxs-lookup"><span data-stu-id="2dbe1-103">How to configure a new multi-tenant application</span></span>

<span data-ttu-id="2dbe1-104">Włączanie federacyjnych rejestracji jednokrotnej (SSO) w aplikacji jest automatycznie włączone podczas federowania za pośrednictwem usługi Azure AD dla OpenID Connect SAML 2.0 i WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="2dbe1-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="2dbe1-105">Jeśli użytkownicy końcowi mogą się zalogować pomimo już o istniejącej sesji z usługą Azure AD, prawdopodobnie aplikacji może być niepoprawnie skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="2dbe1-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="2dbe1-106">Jeśli korzystasz z biblioteki ADAL/MSAL, upewnij się, masz **PromptBehavior** ustawioną **automatycznie** zamiast **zawsze**.</span><span class="sxs-lookup"><span data-stu-id="2dbe1-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span></span>

* <span data-ttu-id="2dbe1-107">Jeśli tworzysz aplikację mobilną, może być konieczne dodatkowe konfiguracje do włączenia funkcji logowania jednokrotnego obsługiwanych przez brokera lub z systemem innym niż obsługiwane przez brokera.</span><span class="sxs-lookup"><span data-stu-id="2dbe1-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="2dbe1-108">Dla systemu Android, zobacz [włączanie dla wielu aplikacji rejestracji Jednokrotnej w systemie Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="2dbe1-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="2dbe1-109">Dla systemu iOS, zobacz [włączanie dla wielu aplikacji rejestracji Jednokrotnej w systemie iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="2dbe1-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dbe1-110">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2dbe1-110">Next steps</span></span>

[<span data-ttu-id="2dbe1-111">Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="2dbe1-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="2dbe1-112">Włączanie Cross logowania jednokrotnego aplikacji w systemie Android</span><span class="sxs-lookup"><span data-stu-id="2dbe1-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="2dbe1-113">Włączanie dla wielu aplikacji rejestracji Jednokrotnej w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="2dbe1-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="2dbe1-114">Integrowanie aplikacji AzureAD</span><span class="sxs-lookup"><span data-stu-id="2dbe1-114">Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="2dbe1-115">Permissioning dla AzureAD w wersji 2.0 i zgody zbieżność aplikacji</span><span class="sxs-lookup"><span data-stu-id="2dbe1-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="2dbe1-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="2dbe1-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
