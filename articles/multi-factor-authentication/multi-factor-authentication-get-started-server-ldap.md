---
title: "aaaLDAP uwierzytelniania i serwera usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Jest to strona uwierzytelnianie wieloskładnikowe Azure hello przydatnej Wdrażanie uwierzytelniania LDAP i serwera usługi Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 17a26b57dbf6afa2fcfdb3d19c5b5ba2987a9f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>Uwierzytelnianie LDAP i serwera usługi Azure Multi-Factor Authentication
Domyślnie program hello Azure aplikacji serwer Multi-Factor Authentication jest skonfigurowany tooimport lub synchronizowania użytkowników z usługi Active Directory. Jednak może być skonfigurowany toobind katalogów LDAP toodifferent, takich jak katalogiem ADAM lub określonym kontrolerem domeny usługi Active Directory. Gdy katalogu tooa połączonych za pośrednictwem protokołu LDAP, powitania serwera usługi Azure Multi-Factor Authentication może działać jako uwierzytelnienia tooperform proxy LDAP. Umożliwia on również hello użycie wiązanie LDAP jako celu serwera RADIUS, wstępnego uwierzytelniania użytkowników za pomocą uwierzytelniania usług IIS lub uwierzytelniania podstawowego w portalu użytkowników usługi Azure MFA hello.

toouse Azure Multi-Factor Authentication jako serwer proxy LDAP, Wstaw powitania serwera usługi Azure Multi-Factor Authentication między klientem LDAP hello (na przykład urządzenia sieci VPN, aplikacji) i serwera katalogu LDAP hello. powitania serwera usługi Azure Multi-Factor Authentication musi być skonfigurowany toocommunicate z serwerami klienckimi hello i hello katalogu LDAP. W tej konfiguracji powitania serwera usługi Azure Multi-Factor Authentication akceptuje żądań LDAP na serwerach klienckie i aplikacje i przekazuje je toohello docelowej LDAP katalogu toovalidate hello głównej poświadczeń serwera. Jeśli katalog LDAP hello sprawdza poprawność poświadczeń głównej hello, uwierzytelnianie wieloskładnikowe Azure wykonuje drugi weryfikacji tożsamości i wysyła klienta LDAP wstecz toohello odpowiedzi. Witaj cały proces uwierzytelniania powiedzie się tylko w przypadku zarówno uwierzytelniania serwera LDAP hello i hello drugi etap weryfikacji.

## <a name="configure-ldap-authentication"></a>Skonfigurowanie uwierzytelniania LDAP
tooconfigure uwierzytelniania LDAP, hello instalacji serwera usługi Azure Multi-Factor Authentication w systemie Windows server. Użyj hello następujące procedury:

### <a name="add-an-ldap-client"></a>Dodawanie klienta LDAP

1. W hello Azure aplikacji serwer Multi-Factor Authentication wybierz ikonę uwierzytelniania LDAP hello w menu po lewej stronie powitania.
2. Sprawdź hello **Włącz uwierzytelnianie LDAP** wyboru.

   ![Uwierzytelnianie LDAP](./media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. Na karcie klientom Witaj Zmień hello TCP port i SSL port Jeśli hello usługi Azure Multi-Factor Authentication LDAP muszą być powiązane toolisten toonon standardowe porty żądań LDAP.
4. Jeśli planujesz toouse LDAPS z powitania klienta toohello serwera usługi Azure Multi-Factor Authentication, certyfikat SSL musi być zainstalowany na powitania tym samym serwerze co serwer usługi MFA. Kliknij przycisk **Przeglądaj** dalej toohello SSL pole certyfikatu, a następnie wybierz toouse certyfikatu, dla hello bezpiecznego połączenia.
5. Kliknij pozycję **Dodaj**.
6. Okno dialogowe Dodawanie klienta LDAP hello wprowadź adres IP hello hello urządzenia, serwera lub aplikacji, który uwierzytelnia toohello serwera i nazwy aplikacji (opcjonalnie). Nazwa aplikacji Hello jest wyświetlana w raportach usługi Azure Multi-Factor Authentication i może być wyświetlany w komunikatach uwierzytelniania wiadomości SMS lub aplikacji mobilnej.
7. Sprawdź hello **dopasowania użytkownika wymagane uwierzytelnianie wieloskładnikowe Azure** Jeśli wszyscy użytkownicy zostały lub zostaną zaimportowane do powitania serwera i podmiotu tootwo krok weryfikacji. Jeśli duża liczba użytkowników nie zostały zaimportowane na powitania serwera i/lub są wykluczone z weryfikacji dwuetapowej, nie zaznaczaj hello pola wyboru. Zobacz plik Pomocy serwera usługi MFA hello, aby uzyskać dodatkowe informacje na temat tej funkcji.

Powtórz te kroki tooadd dodatkowych LDAP klientów.

### <a name="configure-hello-ldap-directory-connection"></a>Skonfiguruj połączenie katalogu LDAP hello

Gdy hello Azure Multi-Factor Authentication jest skonfigurowany tooreceive uwierzytelniania LDAP, musi ona proxy tych katalogu LDAP toohello uwierzytelnienia. W związku z tym karta cel hello wyświetlane są tylko jeden wygaszone toouse opcja Cel LDAP.

1. Witaj tooconfigure połączenia katalogu LDAP, kliknij przycisk hello **integracji katalogów** ikony.
2. Na karcie Ustawienia hello wybierz hello **użyj konkretnej konfiguracji LDAP** przycisk radiowy.
3. Wybierz pozycję **Edytuj...**
4. Okno dialogowe Edycja konfiguracji katalogu LDAP hello należy wypełnić pola hello z katalogiem LDAP toohello tooconnect informacje wymagane hello. Opisy hello pola znajdują się w pliku pomocy powitania serwera usługi Azure Multi-Factor Authentication.

    ![Integracja katalogu](./media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. Testuj połączenie LDAP hello klikając hello **testu** przycisku.
6. Jeśli test połączenia LDAP hello zakończyło się pomyślnie, kliknij przycisk hello **OK** przycisku.
7. Kliknij przycisk hello **filtry** kartę powitania serwera jest wstępnie skonfigurowane tooload kontenerów, grup zabezpieczeń i użytkowników usługi Active Directory. Jeśli powiązanie tooa innym katalogiem LDAP, prawdopodobnie trzeba tooedit hello filtrów wyświetlane. Kliknij przycisk hello **pomocy** łącze, aby uzyskać więcej informacji o filtrach.
8. Kliknij przycisk hello **atrybuty** kartę powitania serwera jest wstępnie skonfigurowana toomap atrybutów z usługi Active Directory.
9. W przypadku powiązania tooa różnych LDAP katalogu lub toochange hello wstępnie skonfigurowane mapowań atrybutów, kliknij przycisk **edycji...**
10. Okno dialogowe Edycja atrybutów hello zmodyfikuj hello Mapowanie atrybutów LDAP dla katalogu. Nazwy atrybutów może być wpisana lub przez kliknięcie przycisku hello **...** pole tooeach przycisk Dalej. Kliknij przycisk hello **pomocy** łącze, aby uzyskać więcej informacji na temat atrybutów.
11. Kliknij przycisk hello **OK** przycisku.
12. Kliknij przycisk hello **ustawienia firmy** ikony, jak i wybierz hello **rozpoznawanie nazwy użytkownika** kartę.
13. Jeśli łączysz tooActive katalogu na serwerze przyłączonym do domeny, należy pozostawić hello **Windows Użyj identyfikatorów zabezpieczeń (SID) w celu dopasowania nazw użytkowników** zaznaczony przycisk radiowy. Witaj, w przeciwnym razie wybierz opcję **atrybutu unikatowego identyfikatora użyj katalogu LDAP w celu dopasowania nazw użytkowników** przycisk radiowy. 

Gdy hello **atrybutu unikatowego identyfikatora użyj katalogu LDAP w celu dopasowania nazw użytkowników** przycisk radiowy zostanie wybrany, powitania serwera usługi Azure Multi-Factor Authentication podejmie tooresolve każdego username tooa Unikatowy identyfikator w katalogu LDAP hello. Przeprowadzone wyszukiwanie LDAP na powitania Username atrybuty zdefiniowane w hello integracji katalogów -> kartę atrybuty. Podczas uwierzytelniania użytkownika, hello username jest rozwiązany toohello Unikatowy identyfikator w katalogu LDAP hello. Unikatowy identyfikator Hello służy do dopasowania hello użytkownika w pliku danych hello Azure Multi-Factor Authentication. Dzięki temu porównania bez uwzględniania wielkości liter, a nazwa użytkownika długich i krótkich formatów.

Po wykonaniu tych kroków hello wykrywa serwera usługi MFA na powitania skonfigurowane porty dla żądań dostępu LDAP z hello skonfigurowany klientów i działania jako serwer proxy dla tych żądań toohello katalogu LDAP dla uwierzytelniania.

## <a name="configure-ldap-client"></a>Konfigurowanie klienta LDAP
tooconfigure powitania klienta LDAP, użyj hello wytycznych:

* Tak, jakby była katalogu LDAP, należy skonfigurować urządzenie, serwer lub tooauthenticate aplikacji za pośrednictwem protokołu LDAP toohello serwera usługi Azure Multi-Factor Authentication. Użyj hello takie same ustawienia, których zwykle użyć tooconnect bezpośrednio tooyour katalogu LDAP, z wyjątkiem hello nazwę serwera lub adres IP, który będzie powitania serwera usługi Azure Multi-Factor Authentication.
* Skonfiguruj hello LDAP limitu czasu too30 60 sekund, dzięki czemu jest czas toovalidate hello poświadczenia użytkownika z katalogiem LDAP hello, wykonaj hello drugi etap weryfikacji otrzymał ich odpowiedzi i odpowiadanie na żądanie dostępu toohello LDAP.
* Jeśli używasz LDAPS, hello urządzenia lub wykonywania kwerend protokołu LDAP powitania serwera muszą ufać hello certyfikatu SSL zainstalowanego na powitania serwera usługi Azure Multi-Factor Authentication.

