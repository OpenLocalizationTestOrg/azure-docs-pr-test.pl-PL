---
title: "Wyświetlanie listy aplikacji w galerii aplikacji usługi Azure Active Directory"
description: "Jak wyświetlić listę aplikacji, która obsługuje logowanie jednokrotne w galerii Azure Active Directory | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: cf25772bd9d92b59401aa5da76e6bbd5fa5ee3e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="listing-your-application-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="db174-103">Wyświetlanie listy aplikacji w galerii aplikacji usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="db174-103">Listing your application in the Azure Active Directory application gallery</span></span>
<span data-ttu-id="db174-104">Aby wyświetlić listę aplikacji, która obsługuje logowanie jednokrotne z usługą Azure Active Directory w [galerii Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), aplikacja musi najpierw implementować jeden z następujących trybów integracji:</span><span class="sxs-lookup"><span data-stu-id="db174-104">To list an application that supports single sign-on with Azure Active Directory in the [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), the application first needs to implement one of the following integration modes:</span></span>

* <span data-ttu-id="db174-105">**OpenID Connect** -bezpośrednia Integracja z usługą Azure AD przy użyciu protokołu OpenID Connect do uwierzytelniania i Azure AD zgody interfejsu API dla konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="db174-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="db174-106">Jeśli aplikacja nie obsługuje SAML integracji jest uruchamiana, to tryb zaleca się.</span><span class="sxs-lookup"><span data-stu-id="db174-106">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
* <span data-ttu-id="db174-107">**SAML** — aplikacja już ma możliwość konfigurowania przy użyciu protokołu SAML dostawcy tożsamości innych firm.</span><span class="sxs-lookup"><span data-stu-id="db174-107">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="db174-108">Listę wymagań dotyczących każdego trybu są poniżej.</span><span class="sxs-lookup"><span data-stu-id="db174-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="db174-109">OpenID Connect integracji</span><span class="sxs-lookup"><span data-stu-id="db174-109">OpenID Connect Integration</span></span>
<span data-ttu-id="db174-110">Integracja aplikacji z usługą Azure AD po [instrukcje developer](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="db174-110">To integrate your application with Azure AD, following the [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="db174-111">Następnie wypełnij poniższe pytania i wysłać do waadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="db174-111">Then complete the questions below and send to waadpartners@microsoft.com.</span></span>

* <span data-ttu-id="db174-112">Podaj poświadczenia dla dzierżawy testowej lub konto z aplikacji, która może służyć przez zespół usługi Azure AD do testowania integracji.</span><span class="sxs-lookup"><span data-stu-id="db174-112">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="db174-113">Zawierają informacje o tym jak zespół usługi Azure AD zalogowanie się i nawiązać połączenia z wystąpieniem usługi Azure AD przy użyciu aplikacji [framework zgody usługi Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="db174-113">Provide instructions on how the Azure AD team can sign in and connect an instance of Azure AD to your application using the [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="db174-114">Podaj wszelkie dodatkowe informacje wymagane przez zespół usługi Azure AD do testowania rejestracji jednokrotnej z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="db174-114">Provide any further instructions required for the Azure AD team to test single sign-on with your application.</span></span> 
* <span data-ttu-id="db174-115">Podaj poniższe informacje:</span><span class="sxs-lookup"><span data-stu-id="db174-115">Provide the info below:</span></span>

> <span data-ttu-id="db174-116">Nazwa firmy:</span><span class="sxs-lookup"><span data-stu-id="db174-116">Company Name:</span></span>
> 
> <span data-ttu-id="db174-117">Witryna sieci Web firmy:</span><span class="sxs-lookup"><span data-stu-id="db174-117">Company Website:</span></span>
> 
> <span data-ttu-id="db174-118">Nazwa aplikacji:</span><span class="sxs-lookup"><span data-stu-id="db174-118">Application Name:</span></span>
> 
> <span data-ttu-id="db174-119">Opis aplikacji (limit 200 znaków):</span><span class="sxs-lookup"><span data-stu-id="db174-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="db174-120">Aplikacji witryny sieci Web (informacyjnych):</span><span class="sxs-lookup"><span data-stu-id="db174-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="db174-121">Witryny sieci Web aplikacji Technical pomocy technicznej lub informacje o kontaktach:</span><span class="sxs-lookup"><span data-stu-id="db174-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="db174-122">Identyfikator aplikacji, jak pokazano w sekcji szczegółów aplikacji w https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="db174-122">Application  ID of the application, as shown in the application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="db174-123">Gdy klienci przejdź do zarejestrowania się w adres URL zapisywania się do aplikacji i notebooka zakupu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="db174-123">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="db174-124">Należy wybrać maksymalnie trzy kategorie aplikacji do wyświetlenia na liście (Aby uzyskać dostępne kategorie, zobacz Azure Active Directory Marketplace):</span><span class="sxs-lookup"><span data-stu-id="db174-124">Choose up to three categories for your application to be listed under (for available categories see the Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="db174-125">Dołącz małych ikon aplikacji (plik PNG, 45px przez 45px, pełny kolor tła):</span><span class="sxs-lookup"><span data-stu-id="db174-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="db174-126">Dołącz dużych ikon aplikacji (plik PNG, 215px przez 215px, pełny kolor tła):</span><span class="sxs-lookup"><span data-stu-id="db174-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="db174-127">Dołącz Logo aplikacji (plik PNG, 150px przez 122px, przezroczystego tła):</span><span class="sxs-lookup"><span data-stu-id="db174-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="db174-128">Integrację SAML</span><span class="sxs-lookup"><span data-stu-id="db174-128">SAML Integration</span></span>
<span data-ttu-id="db174-129">Dowolną aplikację, który obsługuje SAML 2.0 może być bezpośrednio integrowany z dzierżawy usługi Azure AD przy użyciu [te instrukcje, aby dodać niestandardową aplikację](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="db174-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions to add a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="db174-130">Po przetestowaniu się, że integracją aplikacji współpracuje z usługą Azure AD, należy wysłać następujące informacje, aby < mailto:waadpartners@microsoft.com >.</span><span class="sxs-lookup"><span data-stu-id="db174-130">Once you have tested that your application integration works with Azure AD, send the following information to <mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="db174-131">Podaj poświadczenia dla dzierżawy testowej lub konto z aplikacji, która może służyć przez zespół usługi Azure AD do testowania integracji.</span><span class="sxs-lookup"><span data-stu-id="db174-131">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="db174-132">Podaj SAML adres URL logowania, adres URL wystawcy (identyfikator jednostki) i adres URL odpowiedzi (usługa konsumenta potwierdzenia) wartości dla aplikacji, zgodnie z opisem [tutaj](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="db174-132">Provide the SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="db174-133">Jeśli podasz zwykle te wartości jako część pliku metadanych SAML, można wysyłać również.</span><span class="sxs-lookup"><span data-stu-id="db174-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="db174-134">Podaj krótki opis sposobu konfigurowania usługi Azure AD jako dostawcy tożsamości w aplikacji przy użyciu SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="db174-134">Provide a brief description of how to configure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="db174-135">Jeśli aplikacja obsługuje konfigurowanie usługi Azure AD jako dostawcy tożsamości za pośrednictwem portalu samoobsługowego administracyjne, następnie upewnij się, że poświadczenia podane powyżej obejmują możliwość tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="db174-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure the credentials provided above include the ability to set this up.</span></span>
* <span data-ttu-id="db174-136">Podaj poniższe informacje:</span><span class="sxs-lookup"><span data-stu-id="db174-136">Provide the info below:</span></span>

> <span data-ttu-id="db174-137">Nazwa firmy:</span><span class="sxs-lookup"><span data-stu-id="db174-137">Company Name:</span></span>
> 
> <span data-ttu-id="db174-138">Witryna sieci Web firmy:</span><span class="sxs-lookup"><span data-stu-id="db174-138">Company Website:</span></span>
> 
> <span data-ttu-id="db174-139">Nazwa aplikacji:</span><span class="sxs-lookup"><span data-stu-id="db174-139">Application Name:</span></span>
> 
> <span data-ttu-id="db174-140">Opis aplikacji (limit 200 znaków):</span><span class="sxs-lookup"><span data-stu-id="db174-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="db174-141">Aplikacji witryny sieci Web (informacyjnych):</span><span class="sxs-lookup"><span data-stu-id="db174-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="db174-142">Witryny sieci Web aplikacji Technical pomocy technicznej lub informacje o kontaktach:</span><span class="sxs-lookup"><span data-stu-id="db174-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="db174-143">Gdy klienci przejdź do zarejestrowania się w adres URL zapisywania się do aplikacji i notebooka zakupu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="db174-143">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="db174-144">Wybrać maksymalnie trzy kategorie aplikacji do wyświetlenia na liście (dostępne kategorie można znaleźć [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="db174-144">Choose up to three categories for your application to be listed under (for available categories see the [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="db174-145">Dołącz małych ikon aplikacji (plik PNG, 45px przez 45px, pełny kolor tła):</span><span class="sxs-lookup"><span data-stu-id="db174-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="db174-146">Dołącz dużych ikon aplikacji (plik PNG, 215px przez 215px, pełny kolor tła):</span><span class="sxs-lookup"><span data-stu-id="db174-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="db174-147">Dołącz Logo aplikacji (plik PNG, 150px przez 122px, przezroczystego tła):</span><span class="sxs-lookup"><span data-stu-id="db174-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

