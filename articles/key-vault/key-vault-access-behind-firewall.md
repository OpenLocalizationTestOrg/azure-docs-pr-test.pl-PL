---
title: "aaaAccess Key Vault za zaporą | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooaccess Azure klucza magazynu z aplikacji za zaporą"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>Uzyskiwanie dostępu do usługi Azure Key Vault za zaporą
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>Pytanie: czy Moja aplikacja klienta magazynu kluczy musi toobe za zaporą. Jakie porty, hosty lub adresy IP należy otworzyć magazynu kluczy tooa tooenable dostępu?
tooaccess magazyn kluczy, aplikacja kliencka magazynu kluczy ma tooaccess wiele punktów końcowych dla różnych funkcji:

* Uwierzytelnianie za pośrednictwem usługi Azure Active Directory (Azure AD).
* Zarządzanie usługą Azure Key Vault. Obejmuje to tworzenie, odczytywanie, aktualizowanie, usuwanie oraz ustawianie zasad dostępu za pośrednictwem usługi Azure Resource Manager.
* Dostęp i zarządzanie obiektów (kluczy i kluczy tajnych) przechowywanych w magazynie kluczy samego, pośrednictwa hello specyficzne dla klucza magazynu punktu końcowego (na przykład [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

W zależności od konfiguracji i środowiska istnieją pewne odstępstwa.   

## <a name="ports"></a>Porty
Przechodzi wszystkie ruchu tooa magazynu kluczy dla wszystkich trzech funkcji (dostęp płaszczyzny uwierzytelniania, zarządzania i dane) za pośrednictwem protokołu HTTPS: portu 443. Jednak w przypadku listy CRL może czasami wystąpić ruch za pośrednictwem protokołu HTTP (port 80). Klienci obsługujący protokół OCSP nie powinni docierać do listy CRL, ale czasami mogą dotrzeć do pliku [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl).  

## <a name="authentication"></a>Authentication
Aplikacje klienckie magazynu kluczy musi tooaccess punktów końcowych usługi Azure Active Directory do uwierzytelniania. Witaj punktowi końcowemu używanemu zależy hello konfiguracji dzierżawy usługi Azure AD, hello typ podmiotu zabezpieczeń (głównej nazwy użytkownika lub nazwy głównej usługi) i hello typ konta — na przykład konta Microsoft lub służbowy lub konta służbowego.  

| Typ nazwy głównej | Punkt końcowy:port |
| --- | --- |
| Użytkownik korzystający z konta Microsoft<br> (na przykład user@hotmail.com) |**Cały świat:**<br> login.microsoftonline.com:443<br><br> **Chińska wersja platformy Azure:**<br> login.chinacloudapi.cn:443<br><br>**Wersja platformy Azure dla administracji USA:**<br> login-us.microsoftonline.com:443<br><br>**Niemiecka wersja platformy Azure:**<br> login.microsoftonline.de:443<br><br> i <br>login.live.com:443 |
| Użytkownika lub nazwy głównej usługi przy użyciu konta służbowego z usługą Azure AD (na przykład user@contoso.com) |**Cały świat:**<br> login.microsoftonline.com:443<br><br> **Chińska wersja platformy Azure:**<br> login.chinacloudapi.cn:443<br><br>**Wersja platformy Azure dla administracji USA:**<br> login-us.microsoftonline.com:443<br><br>**Niemiecka wersja platformy Azure:**<br> login.microsoftonline.de:443 |
| Użytkownika lub nazwy głównej usługi przy użyciu służbowy lub konta służbowego, oraz usługi Active Directory Federation Services (AD FS) lub inne federacyjne punktu końcowego (na przykład user@contoso.com) |Wszystkie punkty końcowe dla konta służbowego oraz punkty końcowe usług AD FS lub inne federacyjne punkty końcowe |

Istnieją inne możliwe złożone scenariusze. Odwołuje się zbyt[Azure Active Directory Authentication przepływ](/documentation/articles/active-directory-authentication-scenarios/), [integracji aplikacji z usługą Azure Active Directory](/documentation/articles/active-directory-integrating-applications/), i [protokoły uwierzytelniania w usłudze Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) Aby uzyskać dodatkowe informacje.  

## <a name="key-vault-management"></a>Zarządzanie usługą Key Vault
Do zarządzania usługi Key Vault (CRUD i ustawienie zasad dostępu) aplikacji klienckiej hello magazynu kluczy musi tooaccess punktu końcowego usługi Azure Resource Manager.  

| Typ operacji | Punkt końcowy:port |
| --- | --- |
| Operacje warstwy kontroli usługi Key Vault<br> za pośrednictwem usługi Azure Resource Manager |**Cały świat:**<br> management.azure.com:443<br><br> **Chińska wersja platformy Azure:**<br> management.chinacloudapi.cn:443<br><br> **Wersja platformy Azure dla administracji USA:**<br> management.usgovcloudapi.net:443<br><br> **Niemiecka wersja platformy Azure:**<br> management.microsoftazure.de:443 |
| Interfejs API programu Graph usługi Azure Active Directory |**Cały świat:**<br> graph.windows.net:443<br><br> **Chińska wersja platformy Azure:**<br> graph.chinacloudapi.cn:443<br><br> **Wersja platformy Azure dla administracji USA:**<br> graph.windows.net:443<br><br> **Niemiecka wersja platformy Azure:**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Operacje usługi Key Vault
Do zarządzania (kluczy i kluczy tajnych) obiektów magazynu kluczy i operacje kryptograficzne powitania klienta magazynu kluczy musi tooaccess hello magazynu kluczy w punkcie końcowym. sufiks DNS punktu końcowego Hello różni się w zależności od lokalizacji hello magazynu kluczy. hello format jest punktu końcowego magazynu kluczy Hello *nazwę magazynu*. *region —-sufiks dns konkretnego*, zgodnie z opisem w poniższej tabeli hello.  

| Typ operacji | Punkt końcowy:port |
| --- | --- |
| Operacje, takie jak operacje kryptograficzne na kluczach, tworzenie, odczytywanie, aktualizowanie i usuwanie kluczy oraz wpisów tajnych, ustawianie lub pobieranie tagów i innych atrybutów obiektów magazynu kluczy (klucze lub wpisy tajne) |**Cały świat:**<br> &lt;nazwa_magazynu&gt;.vault.azure.net:443<br><br> **Chińska wersja platformy Azure:**<br> &lt;nazwa_magazynu&gt;.vault.azure.cn:443<br><br> **Wersja platformy Azure dla administracji USA:**<br> &lt;nazwa_magazynu&gt;.vault.usgovcloudapi.net:443<br><br> **Niemiecka wersja platformy Azure:**<br> &lt;nazwa_magazynu&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>Zakresy adresów IP
Witaj w usłudze Key Vault używa innych zasobów platformy Azure, takich jak PaaS infrastruktury. Tak nie jest możliwe tooprovide określonego zakresu adresów IP tego punktów końcowych usługi będzie mieć jednocześnie określonej usługi Key Vault. Jeśli zapora obsługuje tylko zakresów adresów IP, zobacz toohello [zakresy IP centrum danych Azure Microsoft](https://www.microsoft.com/download/details.aspx?id=41653) dokumentu. Uwierzytelnianie i tożsamość (Azure Active Directory), aplikacja musi być punkty końcowe toohello stanie tooconnect opisanego w [adresy uwierzytelnianie i tożsamość](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="next-steps"></a>Następne kroki
Jeśli masz pytania dotyczące usługi Key Vault, odwiedź stronę hello [fora magazynu kluczy Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

