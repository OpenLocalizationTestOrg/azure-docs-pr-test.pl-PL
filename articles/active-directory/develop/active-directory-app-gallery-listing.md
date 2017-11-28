---
title: aaaListing aplikacji w galerii aplikacji hello Azure Active Directory
description: "Jak toolist aplikacji, która obsługuje logowanie jednokrotne w hello galerii Azure Active Directory | Microsoft Azure"
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
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a><span data-ttu-id="f4e7f-103">Wyświetlanie listy aplikacji w galerii aplikacji hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4e7f-103">Listing your application in hello Azure Active Directory application gallery</span></span>
<span data-ttu-id="f4e7f-104">toolist aplikacji, która obsługuje logowanie jednokrotne z usługą Azure Active Directory w hello [galerii Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), aplikacja hello musi najpierw tooimplement hello następujące tryby integracji:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-104">toolist an application that supports single sign-on with Azure Active Directory in hello [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), hello application first needs tooimplement one of hello following integration modes:</span></span>

* <span data-ttu-id="f4e7f-105">**OpenID Connect** — bezpośrednia Integracja z usługą Azure AD do uwierzytelniania przy użyciu protokołu OpenID Connect i hello Azure AD zgody interfejsu API dla konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="f4e7f-106">Jeśli aplikacja nie obsługuje SAML integracji jest uruchamiana, to hello zalecamy tryb.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-106">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
* <span data-ttu-id="f4e7f-107">**SAML** — hello możliwości tooconfigure dostawcy tożsamości innych firm przy użyciu protokołu SAML hello ma już aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-107">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="f4e7f-108">Listę wymagań dotyczących każdego trybu są poniżej.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="f4e7f-109">OpenID Connect integracji</span><span class="sxs-lookup"><span data-stu-id="f4e7f-109">OpenID Connect Integration</span></span>
<span data-ttu-id="f4e7f-110">toointegrate aplikacji z usługą Azure AD, następujące hello [instrukcje developer](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="f4e7f-110">toointegrate your application with Azure AD, following hello [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="f4e7f-111">Następnie ukończyć powitalnych pytań poniżej i wysłać toowaadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-111">Then complete hello questions below and send toowaadpartners@microsoft.com.</span></span>

* <span data-ttu-id="f4e7f-112">Podaj poświadczenia dla dzierżawy testowej lub konto z aplikacją, które mogą być używane przez hello Azure zespołu tootest hello integracji z usługą AD.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-112">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="f4e7f-113">Zawierają informacje o tym jak zarejestrować się w team hello Azure AD i połącz wystąpienie aplikacji tooyour usługi Azure AD przy użyciu hello [framework zgody usługi Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="f4e7f-113">Provide instructions on how hello Azure AD team can sign in and connect an instance of Azure AD tooyour application using hello [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="f4e7f-114">Podaj wszelkie dodatkowe informacje wymagane dla hello Azure AD zespołu tootest rejestracji jednokrotnej z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-114">Provide any further instructions required for hello Azure AD team tootest single sign-on with your application.</span></span> 
* <span data-ttu-id="f4e7f-115">Podaj poniższe informacje hello:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-115">Provide hello info below:</span></span>

> <span data-ttu-id="f4e7f-116">Nazwa firmy:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-116">Company Name:</span></span>
> 
> <span data-ttu-id="f4e7f-117">Witryna sieci Web firmy:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-117">Company Website:</span></span>
> 
> <span data-ttu-id="f4e7f-118">Nazwa aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-118">Application Name:</span></span>
> 
> <span data-ttu-id="f4e7f-119">Opis aplikacji (limit 200 znaków):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="f4e7f-120">Aplikacji witryny sieci Web (informacyjnych):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="f4e7f-121">Witryny sieci Web aplikacji Technical pomocy technicznej lub informacje o kontaktach:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="f4e7f-122">Identyfikator aplikacji hello, jak pokazano w szczegółach aplikacji hello na https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-122">Application  ID of hello application, as shown in hello application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="f4e7f-123">Adres URL z zapisywania się do aplikacji, gdzie toosign dla klientów i notebooka zakupu aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-123">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="f4e7f-124">Wybierz kategorie toothree Twojego toobe aplikacji na liście (aby dostępne kategorie Zobacz hello Azure Active Directory Marketplace):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-124">Choose up toothree categories for your application toobe listed under (for available categories see hello Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="f4e7f-125">Dołącz małych ikon aplikacji (plik PNG, 45px przez 45px, pełny kolor tła):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="f4e7f-126">Dołącz dużych ikon aplikacji (plik PNG, 215px przez 215px, pełny kolor tła):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="f4e7f-127">Dołącz Logo aplikacji (plik PNG, 150px przez 122px, przezroczystego tła):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="f4e7f-128">Integrację SAML</span><span class="sxs-lookup"><span data-stu-id="f4e7f-128">SAML Integration</span></span>
<span data-ttu-id="f4e7f-129">Dowolną aplikację, który obsługuje SAML 2.0 może być bezpośrednio integrowany z dzierżawy usługi Azure AD przy użyciu [tooadd te instrukcje niestandardową aplikację](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="f4e7f-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions tooadd a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="f4e7f-130">Po przetestowaniu się, że integracją aplikacji współpracuje z usługą Azure AD, Wyślij hello zbyt następujących informacji<mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-130">Once you have tested that your application integration works with Azure AD, send hello following information too<mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="f4e7f-131">Podaj poświadczenia dla dzierżawy testowej lub konto z aplikacją, które mogą być używane przez hello Azure zespołu tootest hello integracji z usługą AD.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-131">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="f4e7f-132">Podaj hello SAML adres URL logowania, adres URL wystawcy (identyfikator jednostki,) i adres URL odpowiedzi (usługa konsumenta potwierdzenia) wartości dla aplikacji, zgodnie z opisem [tutaj](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="f4e7f-132">Provide hello SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="f4e7f-133">Jeśli podasz zwykle te wartości jako część pliku metadanych SAML, można wysyłać również.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="f4e7f-134">Podaj krótki opis sposobu tooconfigure usługi Azure AD jako dostawcy tożsamości w aplikacji przy użyciu SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-134">Provide a brief description of how tooconfigure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="f4e7f-135">Jeśli aplikacja obsługuje konfigurowanie usługi Azure AD jako dostawcy tożsamości za pośrednictwem portalu samoobsługowego administracyjne, następnie sprawdź, czy poświadczenia hello podanego powyżej obejmują hello możliwości tooset to się.</span><span class="sxs-lookup"><span data-stu-id="f4e7f-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure hello credentials provided above include hello ability tooset this up.</span></span>
* <span data-ttu-id="f4e7f-136">Podaj poniższe informacje hello:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-136">Provide hello info below:</span></span>

> <span data-ttu-id="f4e7f-137">Nazwa firmy:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-137">Company Name:</span></span>
> 
> <span data-ttu-id="f4e7f-138">Witryna sieci Web firmy:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-138">Company Website:</span></span>
> 
> <span data-ttu-id="f4e7f-139">Nazwa aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-139">Application Name:</span></span>
> 
> <span data-ttu-id="f4e7f-140">Opis aplikacji (limit 200 znaków):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="f4e7f-141">Aplikacji witryny sieci Web (informacyjnych):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="f4e7f-142">Witryny sieci Web aplikacji Technical pomocy technicznej lub informacje o kontaktach:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="f4e7f-143">Adres URL z zapisywania się do aplikacji, gdzie toosign dla klientów i notebooka zakupu aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="f4e7f-143">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="f4e7f-144">Wybierz kategorie toothree Twojego toobe aplikacji kategorii (dostępne kategorie można znaleźć hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-144">Choose up toothree categories for your application toobe listed under (for available categories see hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="f4e7f-145">Dołącz małych ikon aplikacji (plik PNG, 45px przez 45px, pełny kolor tła):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="f4e7f-146">Dołącz dużych ikon aplikacji (plik PNG, 215px przez 215px, pełny kolor tła):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="f4e7f-147">Dołącz Logo aplikacji (plik PNG, 150px przez 122px, przezroczystego tła):</span><span class="sxs-lookup"><span data-stu-id="f4e7f-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

