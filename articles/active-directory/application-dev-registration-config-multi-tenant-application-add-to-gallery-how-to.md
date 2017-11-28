---
title: "Jak dodać aplikację wielodostępne do galerii aplikacji Azure AD | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak można wyświetlić listę własnej rozwinięte wielodostępnych aplikacji w galerii aplikacji usługi Azure AD"
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
ms.openlocfilehash: 208f0d40bd7a8e8f35f16e1fcb09c305d833dbb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-add-a-multi-tenant-application-to-the-azure-ad-application-gallery"></a><span data-ttu-id="62282-103">Jak dodać aplikację wielodostępne do galerii aplikacji Azure AD</span><span class="sxs-lookup"><span data-stu-id="62282-103">How to add a multi-tenant application to the Azure AD application gallery</span></span>

## <a name="what-is-the-azure-ad-application-gallery"></a><span data-ttu-id="62282-104">Co to jest galerii aplikacji usługi Azure AD?</span><span class="sxs-lookup"><span data-stu-id="62282-104">What is the Azure AD Application Gallery?</span></span>

<span data-ttu-id="62282-105">Galerii aplikacji usługi Azure AD jest doskonałym sposobem na aplikacji przed miliony klientów usługi Azure Active Directory rozszerzenie wpływ i osiągnąć aplikacji w witrynie marketplace.</span><span class="sxs-lookup"><span data-stu-id="62282-105">The Azure AD Application Gallery is a great way to get your application in front of all the millions of Azure Active Directory customers to broaden the impact and reach of your application in the marketplace.</span></span> <span data-ttu-id="62282-106">Kroki wyjaśniają, jak można wyświetlić listę aplikacji w galerii aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62282-106">The below steps explain how you can list your application in the Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="62282-107">Jeśli aplikacja obsługuje SAML lub OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="62282-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="62282-108">Jeśli masz aplikację wielodostępne, który chcesz wyświetlić w galerii aplikacji usługi Azure AD, najpierw należy się upewnić, czy aplikacja obsługuje jeden z następujących pojedynczego logowania jednokrotnego technologii:</span><span class="sxs-lookup"><span data-stu-id="62282-108">If you have a multi-tenant application you'd like to list in the Azure AD Application Gallery, you must first make sure that your application supports one of the following single sign-on technologies:</span></span>

1. <span data-ttu-id="62282-109">**OpenID Connect** -bezpośrednia Integracja z usługą Azure AD przy użyciu protokołu OpenID Connect do uwierzytelniania i Azure AD zgody interfejsu API dla konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="62282-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="62282-110">Jeśli aplikacja nie obsługuje SAML integracji jest uruchamiana, to tryb zaleca się.</span><span class="sxs-lookup"><span data-stu-id="62282-110">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
2. <span data-ttu-id="62282-111">**SAML** — aplikacja już ma możliwość konfigurowania przy użyciu protokołu SAML dostawcy tożsamości innych firm.</span><span class="sxs-lookup"><span data-stu-id="62282-111">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="62282-112">Jeżeli aplikacja obsługuje jeden z tych pojedynczego trybów logowania jednokrotnego i chcesz wyświetlanie wielodostępnych aplikacji w galerii aplikacji usługi Azure AD, należy wykonać kroki opisane w dokumencie poniżej.</span><span class="sxs-lookup"><span data-stu-id="62282-112">If your application supports one of these single sign-on modes and you'd like to list your multi-tenant application in the Azure AD Application Gallery, you can follow the steps in the document below.</span></span> <span data-ttu-id="62282-113">Aby szybko rozpocząć Wyślij wiadomość e-mail do  **waadpartners@microsoft.com** .</span><span class="sxs-lookup"><span data-stu-id="62282-113">To get started quickly send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="62282-114">Jeśli aplikacja nie obsługuje SAML lub OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="62282-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="62282-115">Nawet wtedy, gdy aplikacja nie obsługuje jeden z trybów, firma Microsoft może nadal zintegrować ją z galerii przy użyciu technologii nasze hasło logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="62282-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="62282-116">Jeśli chcesz zapoznać się z tej opcji, możesz wysłać wiadomość e-mail na adres  **waadpartners@microsoft.com** .</span><span class="sxs-lookup"><span data-stu-id="62282-116">If you'd like to explore this option, you can send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62282-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62282-117">Next steps</span></span>
[<span data-ttu-id="62282-118">Jak wyświetlić listę aplikacji w galerii aplikacji usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62282-118">How to list your application in the Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
