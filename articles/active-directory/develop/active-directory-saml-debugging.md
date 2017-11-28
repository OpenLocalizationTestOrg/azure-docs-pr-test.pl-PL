---
title: "toodebug aaaHow SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure Active Directory "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="f5aef-103">Jak toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5aef-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="f5aef-104">Podczas debugowania integracji aplikacji opartej na SAML, jest często przydatne toouse narzędzia, takiego jak [Fiddler](http://www.telerik.com/fiddler) toosee hello żądania, odpowiedzi SAML hello i hello rzeczywiste tokenu SAML wystawiony toohello aplikacji SAML.</span><span class="sxs-lookup"><span data-stu-id="f5aef-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="f5aef-105">Przez sprawdzenie tokenu SAML hello, upewnij się, że wszystkie hello wymaganych atrybutów, hello nazwę użytkownika w hello SAML podmiotu, a Witaj wystawca identyfikatora URI są dostępne za pośrednictwem zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="f5aef-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="f5aef-106">Hello odpowiedzi z usługi Azure AD, który zawiera hello SAML token jest zwykle Witaj, który występuje po przekierowania HTTP 302 z https://login.windows.net i skonfigurowano wysłane toohello **adres URL odpowiedzi** aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f5aef-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="f5aef-107">Możesz wyświetlić tokenu SAML hello tego wiersza, a następnie zaznaczając hello **inspektorzy > WebForms** kartę hello prawym panelu.</span><span class="sxs-lookup"><span data-stu-id="f5aef-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="f5aef-108">Z tego miejsca, kliknij prawym przyciskiem myszy hello **SAMLResponse** wartość, a następnie wybierz **wysyłania tooTextWizard**.</span><span class="sxs-lookup"><span data-stu-id="f5aef-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="f5aef-109">Następnie wybierz **Base64 z** z hello **przekształcenie** menu toodecode hello token i wyświetlić jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="f5aef-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="f5aef-110">**Uwaga**: toosee hello zawartość HTTP tego żądania, Fiddler może monitować odszyfrowywanie tooconfigure ruch protokołu HTTPS, który będzie potrzebny toodo.</span><span class="sxs-lookup"><span data-stu-id="f5aef-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="f5aef-111">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="f5aef-111">Related Articles</span></span>
* [<span data-ttu-id="f5aef-112">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5aef-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="f5aef-113">Konfigurowanie jednego logowania jednokrotnego tooapplications, które nie znajdują się w galerii aplikacji hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5aef-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="f5aef-114">W jaki sposób tooCustomize oświadczenia wydane w hello tokenu SAML dla aplikacji Pre-Integrated</span><span class="sxs-lookup"><span data-stu-id="f5aef-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png