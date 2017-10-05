---
title: 'Azure Active Directory B2C: Strona docelowa zasad niestandardowych | Microsoft Docs'
description: "Tworzenie aplikacji dla użytkowników za pomocą usługi Azure Active Directory B2C i zasad niestandardowych"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f2079f53-a637-4f2d-b3a0-61a9647ad433
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 5/06/2017
ms.author: parakhj
ms.openlocfilehash: cb7a9f01e43d41eb7315cb37a41e69f044ce5566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-up-and-sign-in-consumers-in-your-applications-using-custom-policies"></a><span data-ttu-id="a343b-103">Azure Active Directory B2C: Rejestrowanie i logowanie użytkowników w aplikacjach za pomocą zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="a343b-103">Azure Active Directory B2C: Sign up and sign in consumers in your applications using custom policies</span></span>
<span data-ttu-id="a343b-104">Zasady niestandardowe to pliki konfiguracji definiujące zachowanie Twojej dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a343b-104">Custom policies are configuration files that define the behavior of your Azure AD B2C tenant.</span></span> <span data-ttu-id="a343b-105">Mogą być w pełni edytowane przez dewelopera tożsamości, dzięki czemu mogą wykonywać niemal nieograniczoną liczbę zadań.</span><span class="sxs-lookup"><span data-stu-id="a343b-105">They can be fully edited by an identity developer to complete a near unlimited number of tasks.</span></span>

## <a name="how-to-articles"></a><span data-ttu-id="a343b-106">Instrukcje</span><span class="sxs-lookup"><span data-stu-id="a343b-106">How-to articles</span></span>
<span data-ttu-id="a343b-107">Informacje o sposobie korzystania z określonych funkcji usługi Azure Active Directory B2C:</span><span class="sxs-lookup"><span data-stu-id="a343b-107">Learn how to use specific Azure Active Directory B2C features:</span></span>

* [<span data-ttu-id="a343b-108">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="a343b-108">Get Started</span></span>](active-directory-b2c-overview-custom.md)
* <span data-ttu-id="a343b-109">Konfigurowanie dostawców uwierzytelniania OIDC, takich jak usługa [Azure AD](active-directory-b2c-setup-aad-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a343b-109">Configure OIDC Providers such as [Azure AD](active-directory-b2c-setup-aad-custom.md).</span></span>
* <span data-ttu-id="a343b-110">Konfigurowanie dostawców uwierzytelniania SAML, takich jak usługa [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a343b-110">Configure SAML Providers such as [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span></span>
* <span data-ttu-id="a343b-111">Integrowanie interfejsów API RESTful:</span><span class="sxs-lookup"><span data-stu-id="a343b-111">Integrate RESTful APIs:</span></span>
    * <span data-ttu-id="a343b-112">[Uzyskiwanie dodatkowych oświadczeń](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a343b-112">[Obtain additional claims](active-directory-b2c-rest-api-step-custom.md).</span></span>
    * <span data-ttu-id="a343b-113">[Weryfikowanie danych wejściowych użytkownika](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a343b-113">[Validate user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>
* <span data-ttu-id="a343b-114">Dostosowywanie logowania:</span><span class="sxs-lookup"><span data-stu-id="a343b-114">Customize Login:</span></span>
    * [<span data-ttu-id="a343b-115">Konfigurowanie danych wejściowych użytkownika</span><span class="sxs-lookup"><span data-stu-id="a343b-115">Configure User Input</span></span>](active-directory-b2c-configure-signup-self-asserted-custom.md)
    * [<span data-ttu-id="a343b-116">Dostosowywanie interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="a343b-116">Customize UI</span></span>](active-directory-b2c-ui-customization-custom.md)
    * [<span data-ttu-id="a343b-117">Dostosowywanie tokenu</span><span class="sxs-lookup"><span data-stu-id="a343b-117">Customize Token</span></span>](active-directory-b2c-reference-manage-sso-and-token-configuration.md)
* <span data-ttu-id="a343b-118">Rozwiązywanie problemów przez [zbieranie dzienników przy użyciu usługi Application Insights](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a343b-118">Troubleshoot by [collecting logs using Application Insights](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="whats-new"></a><span data-ttu-id="a343b-119">Co nowego</span><span class="sxs-lookup"><span data-stu-id="a343b-119">What's new</span></span>
<span data-ttu-id="a343b-120">Zaglądaj tu często, aby dowiadywać się o nadchodzących zmianach w usłudze Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="a343b-120">Check back here often to learn about future changes to the Azure Active Directory B2C.</span></span> <span data-ttu-id="a343b-121">Będziemy również tweetować o wszystkich aktualizacjach, korzystając z @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="a343b-121">We'll also tweet about any updates by using @AzureAD.</span></span>



