---
title: "Zabezpieczanie PaaS w sieci web i aplikacji dla urządzeń przenośnych za pomocą usługi aplikacji Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 0738522250f1863c9584936a2d2b2c7a0a823c8c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>Zabezpieczanie PaaS w sieci web i aplikacji dla urządzeń przenośnych za pomocą usługi aplikacji Azure

W tym artykule omówiono Kolekcja [usługi aplikacji Azure](https://azure.microsoft.com/services/app-service/) najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. Następujące najlepsze rozwiązania są uzyskiwane z wiemy z doświadczenia z platformy Azure i doświadczenia klientów, takie jak samodzielnie.

## <a name="azure-app-services"></a>Azure App Services
[Usługa Azure App Service](../app-service/app-service-value-prop-what-is.md) jest PaaS, oferty, która umożliwia tworzenie aplikacji sieci web i aplikacji mobilnych dla dowolnej platformy lub urządzenia i połącz się z danymi w dowolnym miejscu, w chmurze lub lokalnie. Usługi aplikacji obejmuje sieci web i mobilnych możliwości, które były wcześniej dostępne oddzielnie jako witryny sieci Web Azure oraz Azure Mobile Services. Obejmuje ona także nowe funkcje automatyzacji procesów biznesowych i hostowania interfejsów API w chmurze. Jako pojedyncza zintegrowana usługa App Services oferuje bogaty zestaw funkcji do sieci web, mobilnych i scenariuszy integracji.

Aby dowiedzieć się więcej, zobacz Omówienie na [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) i [aplikacje sieci Web](../app-service-web/app-service-web-overview.md).

## <a name="best-practices"></a>Najlepsze praktyki

Korzystając z usługi aplikacji, wykonaj następujące najlepsze rozwiązania:

- [Uwierzytelnianie za pomocą usługi Azure Active Directory (AD)](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory). Usługi aplikacji udostępnia usługę OAuth 2.0 dla dostawcy tożsamości. OAuth 2.0 koncentruje się na prostotę developer klienta zapewniając przepływów określonych autoryzacji dla aplikacji sieci Web, aplikacje i telefony komórkowe. Usługi Azure AD używa protokołu OAuth 2.0 do autoryzowania dostępu dla urządzeń przenośnych i aplikacji sieci web.
- Ograniczanie dostępu na podstawie musi znać i co najmniej uprawnień zabezpieczeń zasad. Ograniczanie dostępu jest dla organizacji, które mają zostać wymuszone zasady zabezpieczeń dla dostępu do danych. Kontroli dostępu opartej na rolach (RBAC) może służyć do przypisywania uprawnień do użytkowników, grup i aplikacji w określonego zakresu. Aby dowiedzieć się więcej o udzielenie użytkownikom dostęp do aplikacji, zobacz [wprowadzenie do zarządzania dostępem](../active-directory/role-based-access-control-what-is.md).
- Ochrona kluczy. Jaka jest zabezpieczeń nie ma znaczenia w przypadku utraty klucze subskrypcji. Usługa Azure Key Vault ułatwia ochronę kluczy kryptograficznych i kluczy tajnych używanych przez aplikacje i usługi w chmurze. Za pomocą usługi Key Vault możesz szyfrować klucze i klucze tajne (takie jak klucze uwierzytelniania, klucze konta magazynu, klucze szyfrowania danych, pliki PFX oraz hasła) przy użyciu kluczy chronionych przez sprzętowe moduły zabezpieczeń (HSM, hardware security module). W celu zapewnienia dodatkowego bezpieczeństwa możesz zaimportować lub wygenerować klucze w modułach HSM. Zobacz [usługi Azure Key Vault](../key-vault/key-vault-whatis.md) Aby dowiedzieć się więcej. Magazyn kluczy umożliwia także zarządzanie certyfikatami TLS z automatycznego odnawiania.
- Ogranicz przychodzące źródłowych adresów IP. [Środowiska usługi aplikacji](../app-service-web/app-service-app-service-environment-intro.md) funkcją integracji sieci wirtualnej, która pomaga ograniczyć przychodzące źródłowych adresów IP za pomocą grup zabezpieczeń sieci (NSG). Jeśli znasz sieci wirtualnych Azure (sieci wirtualne), jest możliwość, która pozwala na umieszczenie wielu zasobów platformy Azure w kontroli dostępu do sieci z systemem innym niż internet, wzajemnie obsługiwać Routing. Aby dowiedzieć się więcej, zobacz [integracji aplikacji z sieci wirtualnej platformy Azure](../app-service-web/web-sites-integrate-with-vnet.md).

## <a name="next-steps"></a>Następne kroki
W tym artykule wprowadzona w kolekcji usługi aplikacji zabezpieczeń najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. Aby dowiedzieć się więcej na temat zabezpieczania wdrożeń typu PaaS, zobacz:

- [Zabezpieczanie wdrożeń typu PaaS](security-paas-deployments.md)
- [Zabezpieczanie PaaS w sieci web i aplikacji dla urządzeń przenośnych przy użyciu usługi Azure SQL Database i SQL Data Warehouse](security-paas-applications-using-sql.md)
