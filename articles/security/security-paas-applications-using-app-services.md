---
title: "aaaSecuring PaaS w sieci web i aplikacji dla urządzeń przenośnych za pomocą usługi aplikacji Azure | Dokumentacja firmy Microsoft"
description: " Więcej informacji na temat usługi aplikacji Azure najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: 68a741c668efe2157cff114b649e0e287ef196f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>Zabezpieczanie PaaS w sieci web i aplikacji dla urządzeń przenośnych za pomocą usługi aplikacji Azure

W tym artykule omówiono Kolekcja [usługi aplikacji Azure](https://azure.microsoft.com/services/app-service/) najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. Następujące najlepsze rozwiązania są uzyskiwane z wiemy z doświadczenia z platformy Azure i doświadczenia hello klientów, takich jak samodzielnie.

## <a name="azure-app-services"></a>Azure App Services
[Usługa Azure App Service](../app-service/app-service-value-prop-what-is.md) jest PaaS oferty, która umożliwia tworzenie aplikacji sieci web i aplikacji mobilnych dla dowolnej platformy lub urządzenia i połączyć toodata w dowolnym miejscu i w chmurze hello lub lokalnie. Usługi aplikacji obejmuje hello sieci web i mobilnych możliwości, które były wcześniej dostępne oddzielnie jako witryny sieci Web Azure oraz Azure Mobile Services. Obejmuje ona także nowe funkcje automatyzacji procesów biznesowych i hostowania interfejsów API w chmurze. Jako pojedyncza zintegrowana usługa usługi aplikacji oferuje bogaty zestaw funkcji scenariusze tooweb, mobilnych i umożliwiających integrację.

toolearn więcej, zobacz Omówienie na [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) i [aplikacje sieci Web](../app-service-web/app-service-web-overview.md).

## <a name="best-practices"></a>Najlepsze praktyki

Korzystając z usługi aplikacji, wykonaj następujące najlepsze rozwiązania:

- [Uwierzytelnianie za pomocą usługi Azure Active Directory (AD)](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory). Usługi aplikacji udostępnia usługę OAuth 2.0 dla dostawcy tożsamości. OAuth 2.0 koncentruje się na prostotę developer klienta zapewniając przepływów określonych autoryzacji dla aplikacji sieci Web, aplikacje i telefony komórkowe. Korzysta z usługi Azure AD tooenable OAuth 2.0 możesz tooauthorize dostępu toomobile i aplikacji sieci web.
- Ograniczanie dostępu na podstawie tooknow potrzeby hello i co najmniej uprawnień zabezpieczeń zasad. Ograniczanie dostępu jest dla organizacji, które mają tooenforce zasad zabezpieczeń dla dostępu do danych. Kontroli dostępu opartej na rolach (RBAC) mogą być używane tooassign toousers uprawnienia, grup i aplikacji w zakresie niektórych. Zobacz toolearn więcej informacji na temat udzielanie użytkownicy uzyskują dostęp do tooapplications, [wprowadzenie do zarządzania dostępem](../active-directory/role-based-access-control-what-is.md).
- Ochrona kluczy. Jaka jest zabezpieczeń nie ma znaczenia w przypadku utraty klucze subskrypcji. Usługa Azure Key Vault ułatwia ochronę kluczy kryptograficznych i kluczy tajnych używanych przez aplikacje i usługi w chmurze. Za pomocą usługi Key Vault możesz szyfrować klucze i klucze tajne (takie jak klucze uwierzytelniania, klucze konta magazynu, klucze szyfrowania danych, pliki PFX oraz hasła) przy użyciu kluczy chronionych przez sprzętowe moduły zabezpieczeń (HSM, hardware security module). W celu zapewnienia dodatkowego bezpieczeństwa możesz zaimportować lub wygenerować klucze w modułach HSM. Zobacz [usługi Azure Key Vault](../key-vault/key-vault-whatis.md) toolearn więcej. Umożliwia także toomanage Key Vault certyfikaty protokołu TLS z automatycznego odnawiania.
- Ogranicz przychodzące źródłowych adresów IP. [Środowiska usługi aplikacji](../app-service-web/app-service-app-service-environment-intro.md) funkcją integracji sieci wirtualnej, która pomaga ograniczyć przychodzące źródłowych adresów IP za pomocą grup zabezpieczeń sieci (NSG). Jeśli znasz sieci wirtualnych Azure (sieci wirtualne), jest możliwość, która pozwala tooplace przez wiele zasobów platformy Azure w sieci z systemem innym niż internet, wzajemnie obsługiwać Routing możesz kontrolować dostęp do. toolearn więcej, zobacz [integracji aplikacji z sieci wirtualnej platformy Azure](../app-service-web/web-sites-integrate-with-vnet.md).

## <a name="next-steps"></a>Następne kroki
W tym artykule wprowadzono tooa zbiór usług aplikacji zabezpieczeń najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. toolearn więcej informacji na temat zabezpieczania wdrożeń typu PaaS, zobacz:

- [Zabezpieczanie wdrożeń typu PaaS](security-paas-deployments.md)
- [Zabezpieczanie PaaS w sieci web i aplikacji dla urządzeń przenośnych przy użyciu usługi Azure SQL Database i SQL Data Warehouse](security-paas-applications-using-sql.md)
