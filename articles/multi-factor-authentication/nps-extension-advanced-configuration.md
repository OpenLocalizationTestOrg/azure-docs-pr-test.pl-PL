---
title: "aaaConfigure hello rozszerzenia usługi Azure MFA NPS | Dokumentacja firmy Microsoft"
description: "Po zainstalowaniu rozszerzenia serwera NPS hello, wykonaj następujące kroki dla konfiguracji zaawansowanej, takich jak listę dozwolonych podobnej IP i nazwy UPN zastąpienia."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: c3aed077b23c95f874861eb00c8e6dca668329c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-options-for-hello-nps-extension-for-multi-factor-authentication"></a>Zaawansowane opcje konfiguracji hello rozszerzenia serwera NPS uwierzytelnianie wieloskładnikowe

Witaj rozszerzenia serwera zasad sieciowych (NPS) obejmuje funkcje usługi Azure Multi-Factor Authentication oparte na chmurze infrastruktury lokalnej. W tym artykule założono, że już zostały zainstalowane rozszerzenia hello i ma teraz tooknow jak wymaga rozszerzenia hello toocustomize dla Ciebie. 

## <a name="alternate-login-id"></a>Alternatywnego Identyfikatora logowania

Ponieważ hello rozszerzenia serwera NPS łączy tooboth lokalnie i w chmurze katalogów, mogą wystąpić problem, gdy nie są zgodne hello nazwy w chmurze hello sieci lokalnych głównych nazw użytkowników (UPN). toosolve ten problem, użyj logowania alternatywnych identyfikatorów. 

W ramach hello rozszerzenia serwera zasad Sieciowych można wyznaczyć toobe atrybut usługi Active Directory używany zamiast hello UPN dla usługi Azure Multi-Factor Authentication. Umożliwia to możesz tooprotect zasobami lokalnymi w trakcie weryfikacji dwuetapowej bez modyfikowania nazwy UPN użytkownika lokalnego. 

alternatywne nazwy logowania tooconfigure identyfikatory, przejdź za`HKLM\SOFTWARE\Microsoft\AzureMfa` i edytować hello następujące wartości rejestru:

| Nazwa | Typ | Wartość domyślna | Opis |
| ---- | ---- | ------------- | ----------- |
| LDAP_ALTERNATE_LOGINID_ATTRIBUTE | Ciąg | pusty | Wyznaczanie hello nazwa atrybutu usługi Active Directory, które mają toouse zamiast hello głównej nazwy użytkownika. Ten atrybut jest używany jako atrybut AlternateLoginId hello. Jeśli ta wartość rejestru jest ustawiona tooa [nieprawidłowy atrybut usługi Active Directory](https://msdn.microsoft.com/library/ms675090.aspx) (na przykład poczty lub nazwa wyświetlana), następnie wartość atrybutu hello jest używany zamiast nazwy UPN użytkownika hello do uwierzytelniania. Jeśli ta wartość rejestru jest pusty lub nie skonfigurowane, następnie AlternateLoginId jest wyłączone i nazwy UPN użytkownika hello jest używany do uwierzytelniania. |
| LDAP_FORCE_GLOBAL_CATALOG | Wartość logiczna | False | Użyj tej flagi tooforce hello korzystania z wykazu globalnego dla wyszukiwań LDAP podczas wyszukiwania AlternateLoginId. Konfigurowanie kontrolera domeny jako wykazu globalnego, Dodaj hello AlternateLoginId atrybutu toohello wykazu globalnego, a następnie włącz tej flagi. <br><br> Skonfigurowanie (nie jest pusty), LDAP_LOOKUP_FORESTS **ta flaga jest wymuszana jako true**, niezależnie od wartości hello hello ustawienie rejestru. W takim przypadku hello rozszerzenia serwera NPS wymaga toobe wykazu globalnego hello skonfigurowana z atrybutem AlternateLoginId powitania dla każdego lasu. |
| LDAP_LOOKUP_FORESTS | Ciąg | pusty | Podaj Rozdzielana średnikami lista toosearch lasów. Na przykład *contoso.com;foobar.com*. Jeśli ta wartość rejestru jest skonfigurowany, hello rozszerzenia serwera NPS wielokrotnie powtarzane wyszukuje wszystkich lasach hello hello kolejności, w jakiej zostały wymienione i zwraca hello pierwszego pomyślnego AlternateLoginId wartość. Jeśli ta wartość rejestru nie jest skonfigurowane, wyszukiwanie AlternateLoginId hello jest zamkniętej toohello bieżącej domeny.|

tootroubleshoot problemy z logowaniem alternatywnych identyfikatorów, użyj hello zalecane kroki [alternatywny błędy identyfikator logowania](multi-factor-authentication-nps-errors.md#alternate-login-id-errors).

## <a name="ip-exceptions"></a>Wyjątki IP

Jeśli potrzebujesz toomonitor dostępności serwera, takich jak Jeśli moduły równoważenia obciążenia Sprawdź serwerów, które są uruchomione przed wysłaniem obciążeń, nie ma tych toobe kontroli zablokowane przez weryfikację żądania. Zamiast tego Utwórz listę adresów IP, które są używane przez konta usług i wyłączyć wymagania uwierzytelniania wieloskładnikowego dla tej listy. 

Lista dozwolonych adresów IP tooconfigure go za`HKLM\SOFTWARE\Microsoft\AzureMfa` i skonfigurować hello następujące wartości rejestru: 

| Nazwa | Typ | Wartość domyślna | Opis |
| ---- | ---- | ------------- | ----------- |
| IP_WHITELIST | Ciąg | pusty | Podaj Rozdzielana średnikami lista adresów IP. Obejmują hello adresy IP maszyn, których pochodzą żądania obsługi, takie jak hello serwera NAS lub sieć VPN. Zakresy adresów IP to podsieci nie są obsługiwane. <br><br> Na przykład *10.0.0.1;10.0.0.2;10.0.0.3*.

Gdy nadejdzie żądanie z adresu IP w dozwolonych hello, weryfikację dwuetapową zostało pominięte. Witaj lista dozwolonych adresów IP jest porównywany toohello adres IP, który znajduje się w hello *ratNASIPAddress* atrybutu hello żądań RADIUS. Gdy nadejdzie żądanie usługi RADIUS bez atrybutu ratNASIPAddress hello hello następujące ostrzeżenie jest rejestrowane: "Dozwolonych P_WHITE_LIST_WARNING::IP zostanie zignorowany ponieważ brakuje źródłowy adres IP, w żądaniu RADIUS w atrybucie NasIpAddress."

## <a name="next-steps"></a>Następne kroki

[Komunikatami o błędach z hello rozszerzenia serwera NPS uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-nps-errors.md)
