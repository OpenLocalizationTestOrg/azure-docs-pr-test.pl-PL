---
title: "Tożsamość hybrydowa wymagane porty i protokoły - Azure | Dokumentacja firmy Microsoft"
description: "Ta strona jest stroną informacje techniczne dotyczące portów, które są wymagane toobe Otwórz programu Azure AD Connect"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: de97b225-ae06-4afc-b2ef-a72a3643255b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 9c62b74b45e7f266e3a55baa2db07a9ff1c9c6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-required-ports-and-protocols"></a>Wymagane porty i protokoły dotyczące tożsamości hybrydowej
powitania po dokumentu jest techniczne na powitania wymagane porty i protokoły dotyczące implementowania rozwiązania z tożsamością hybrydową. Użyj następującej ilustracji hello i można znaleźć odpowiedniej tabeli toohello.

![Co to jest program Azure AD Connect](./media/active-directory-aadconnect-ports/required3.png)

## <a name="table-1---azure-ad-connect-and-on-premises-ad"></a>Tabela 1 - usługi Azure AD Connect i lokalnej usłudze AD
Ta tabela opisuje hello porty i protokoły, które są wymagane do komunikacji między serwerem usługi Azure AD Connect hello i lokalnej usłudze AD.

| Protokół | Porty | Opis |
| --- | --- | --- |
| DNS |53 (TCP/UDP) |Wyszukiwania DNS na powitania lasu docelowego. |
| Protokół Kerberos |88 (TCP/UDP) |Las toohello AD uwierzytelniania Kerberos. |
| MS-RPC |135 (TCP/UDP) |Używane podczas konfiguracji początkowej hello hello Kreator Azure AD Connect, gdy jest on powiązany toohello AD lasu, a także podczas synchronizacji haseł. |
| LDAP |389 (TCP/UDP) |Używany do importowania danych z usługi Active Directory. Dane są szyfrowane z protokołu Kerberos i zamknięcia. |
| RPC | 445 (TCP/UDP) |Używane przez toocreate bezproblemowe logowania jednokrotnego konta komputera w lesie hello AD. |
| LDAP/SSL |636 (TCP/UDP) |Używany do importowania danych z usługi Active Directory. transfer danych Hello jest podpisane i zaszyfrowane. Używane, jeśli jest używany protokół SSL. |
| RPC |Od 49152 do 65535 (losowe wysokiej RPC Port)(TCP/UDP) |Używane podczas konfiguracji początkowej hello programu Azure AD Connect, gdy jest on powiązany toohello AD lasów i podczas synchronizacji haseł. Zobacz [KB929851](https://support.microsoft.com/kb/929851), [KB832017](https://support.microsoft.com/kb/832017), i [KB224196](https://support.microsoft.com/kb/224196) Aby uzyskać więcej informacji. |

## <a name="table-2---azure-ad-connect-and-azure-ad"></a>Tabela 2 - usługi Azure AD Connect i Azure AD
W tej tabeli opisano hello porty i protokoły, które są wymagane do komunikacji między hello Azure AD Connect server a usługą Azure AD.

| Protokół | Porty | Opis |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |Używane certyfikaty SSL tooverify listy odwołania certyfikatów (listy odwołania certyfikatów) toodownload. |
| HTTPS |443(TCP/UDP) |Toosynchronize używane z usługą Azure AD. |

Aby uzyskać listę adresów URL i IP adresów należy tooopen w zaporze, zobacz [zakresów adresów IP i URL usługi Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="table-3---azure-ad-connect-and-ad-fs-federation-serverswap"></a>Tabela 3 - usługi Azure AD Connect i serwery federacyjne FS AD/WAP
W tej tabeli opisano hello porty i protokoły, które są wymagane do komunikacji między hello Azure AD Connect serwera i serwerów AD FS Federation/protokół WAP usług.  

| Protokół | Porty | Opis |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |Używane certyfikaty SSL tooverify listy odwołania certyfikatów (listy odwołania certyfikatów) toodownload. |
| HTTPS |443(TCP/UDP) |Toosynchronize używane z usługą Azure AD. |
| Usługa WinRM |5985 |Odbiornik usługi WinRM |

## <a name="table-4---wap-and-federation-servers"></a>Tabela 4 - WAP i serwerów federacyjnych
Ta tabela zawiera opis hello porty i protokoły, które są wymagane do komunikacji między serwerami federacyjnymi hello i serwerów proxy.

| Protokół | Porty | Opis |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |Używany do uwierzytelniania. |

## <a name="table-5---wap-and-users"></a>Tabela 5 - WAP i użytkowników
W tej tabeli opisano hello porty i protokoły, które są wymagane do komunikacji między użytkownikami i serwerów proxy hello.

| Protokół | Porty | Opis |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |Używany do uwierzytelniania urządzeń. |
| TCP |49443 (TCP) |Używany do uwierzytelniania certyfikatów. |

## <a name="table-6a--6b---pass-through-authentication-with-single-sign-on-sso-and-password-hash-sync-with-single-sign-on-sso"></a>Tabela 6a & 6b - uwierzytelniania przekazywanego z logowania jednokrotnego (SSO) i synchronizacją skrótów haseł z logowania jednokrotnego (SSO)
następujące tabele Hello opisuje hello porty i protokoły, które są wymagane do komunikacji między hello Azure AD Connect i Azure AD.

### <a name="table-6a---pass-through-authentication-with-sso"></a>Tabela 6a - uwierzytelniania przekazywanego z logowania jednokrotnego
|Protokół|Numer portu|Opis
| --- | --- | ---
|HTTP|80|Włącz wychodzącego ruchu HTTP na potrzeby weryfikacji zabezpieczeń na przykład protokołu SSL. Również wymagane dla łącznika hello automatycznej aktualizacji toofunction możliwości poprawnie.
|HTTPS|443| Włącz ruch wychodzący protokołu HTTPS dla operacji, takich jak włączanie i wyłączanie funkcji hello, rejestrowanie łączniki pobierania aktualizacji łącznika i obsługi wszystkich żądań logowania użytkownika.

Ponadto program Azure AD Connect potrzebuje toobe toomake stanie bezpośredniego toohello połączeń IP [zakresy IP centrum danych Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).

### <a name="table-6b---password-hash-sync-with-sso"></a>Tabela 6b - synchronizacji skrótów haseł z logowania jednokrotnego

|Protokół|Numer portu|Opis
| --- | --- | ---
|HTTPS|443| Włącz rejestrację logowania jednokrotnego (wymagane tylko dla hello procesu rejestracji logowania jednokrotnego).

Ponadto program Azure AD Connect potrzebuje toobe toomake stanie bezpośredniego toohello połączeń IP [zakresy IP centrum danych Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653). Ponownie, jest to tylko wymagane dla procesu rejestracji hello logowania jednokrotnego.

## <a name="table-7a--7b---azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Tabela 7a & 7b — usługi Azure AD i Azure AD Connect Health agent dla (AD FS/Sync)
Witaj poniższych tabelach opisano hello punktów końcowych, porty i protokoły, które są wymagane do komunikacji między agentami Azure AD Connect Health i usługi Azure AD

### <a name="table-7a---ports-and-protocols-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Tabela 7a - porty i protokoły dla usługi Azure AD Connect Health agent dla (AD FS/Sync) i Azure AD
Poniższa tabela zawiera opis powitania po wychodzącego porty i protokoły, które są wymagane do komunikacji między hello Azure AD Connect Health agentów i Azure AD.  

| Protokół | Porty | Opis |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |Wychodzący |
| Azure Service Bus |5671 (TCP/UDP) |Wychodzący |

### <a name="7b---endpoints-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>7b — punkty końcowe dla usługi Azure AD Connect Health agent dla (AD FS/Sync) i Azure AD
Aby uzyskać listę punktów końcowych, zobacz [hello sekcji wymagania hello Azure AD Connect Health Agent](../connect-health/active-directory-aadconnect-health-agent-install.md#requirements).

