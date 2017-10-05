---
title: "Debugowanie na języku SAML logowanie jednokrotne do aplikacji w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można debugować na języku SAML logowanie jednokrotne do aplikacji w usłudze Azure Active Directory "
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
ms.openlocfilehash: 31447d597296bac57481dc2acb4a95ee3a104161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="ff88e-103">Debugowanie na języku SAML logowanie jednokrotne do aplikacji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff88e-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>
<span data-ttu-id="ff88e-104">Podczas debugowania integracji aplikacji opartej na SAML, warto często za pomocą narzędzia, takie jak [Fiddler](http://www.telerik.com/fiddler) żądania SAML, odpowiedzi SAML i rzeczywistego tokenu SAML wystawiony do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ff88e-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span></span> <span data-ttu-id="ff88e-105">Po sprawdzeniu tokenu SAML zapewni, że wszystkie wymagane atrybuty, nazwę użytkownika w podmiotu SAML i wystawcy identyfikatora URI pochodzą za pośrednictwem zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="ff88e-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="ff88e-106">Odpowiedź z usługi Azure AD, który zawiera SAML token jest zwykle występuje po przekierowania HTTP 302 z https://login.windows.net, która jest wysyłana do skonfigurowanych **adres URL odpowiedzi** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ff88e-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span></span> 

<span data-ttu-id="ff88e-107">SAML token można wyświetlić tego wiersza, a następnie zaznaczając **inspektorzy > WebForms** kartę na prawym panelu.</span><span class="sxs-lookup"><span data-stu-id="ff88e-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span></span> <span data-ttu-id="ff88e-108">Z tego miejsca, kliknij prawym przyciskiem myszy **SAMLResponse** wartość, a następnie wybierz **przesyłają TextWizard**.</span><span class="sxs-lookup"><span data-stu-id="ff88e-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span></span> <span data-ttu-id="ff88e-109">Następnie wybierz **Base64 z** z **przekształcenie** menu do zdekodowania token i wyświetlić jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="ff88e-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span></span>

<span data-ttu-id="ff88e-110">**Uwaga**: Aby wyświetlić zawartość tego żądania HTTP, narzędzia Fiddler może zostać wyświetlony komunikat można konfigurować odszyfrowywania ruchu HTTPS, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="ff88e-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span></span>

## <a name="related-articles"></a><span data-ttu-id="ff88e-111">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="ff88e-111">Related Articles</span></span>
* [<span data-ttu-id="ff88e-112">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff88e-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="ff88e-113">Konfigurowanie logowania jednokrotnego do aplikacji, które nie znajdują się w galerii aplikacji Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff88e-113">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="ff88e-114">Dostosowywanie oświadczeń wydanych w tokenie SAML dla wstępnie zintegrowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="ff88e-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png