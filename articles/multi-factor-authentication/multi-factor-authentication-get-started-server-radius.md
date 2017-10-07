---
title: "aaaRADIUS uwierzytelniania i serwera usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Jest to hello Azure Multi-Factor authentication strony przydatnej Wdrażanie uwierzytelniania usługi RADIUS i serwera usługi Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>Integrowanie uwierzytelniania usługi RADIUS z serwerem usługi Azure Multi-Factor Authentication
Użyj sekcji uwierzytelnianie usługi RADIUS hello tooenable serwera usługi Azure MFA i skonfiguruj uwierzytelnianie usługi RADIUS. RADIUS jest standardem protokołu tooaccept żądań uwierzytelnienia i tooprocess te żądania. powitania serwera usługi Azure Multi-Factor Authentication działa jako serwer RADIUS. Wstaw go między klientem RADIUS (urządzenia sieci VPN), a cel uwierzytelniania, który może być usługi Active Directory (AD), katalogu LDAP i innym tooadd serwera RADIUS Azure Multi-Factor Authentication. Tak, aby umożliwić komunikację z serwerami klienckimi hello i hello cel uwierzytelniania dla toofunction Azure Multi-Factor Authentication (MFA), należy skonfigurować powitania serwera usługi Azure MFA. powitania serwera usługi Azure MFA akceptuje żądania od klientów RADIUS, weryfikuje poświadczenia cel uwierzytelniania hello dodaje Azure Multi-Factor Authentication i wysyła klienta RADIUS wstecz toohello odpowiedzi. żądanie uwierzytelnienia Hello powiedzie się tylko, jeśli zarówno podstawowe uwierzytelnianie hello i hello Azure Multi-Factor Authentication powiodło się.

> [!NOTE]
> powitania serwera usługi MFA obsługuje tylko PAP (protokół uwierzytelniania hasła) i MSCHAPv2 (protokół uwierzytelniania typu Challenge Handshake firmy Microsoft) RADIUS protokołów podczas działania jako serwer RADIUS.  Inne protokoły, takie jak protokół EAP (extensible authentication protocol), można po hello MFA serwer działa jako serwer RADIUS tooanother proxy RADIUS, który obsługuje tego protokołu.
>
> W tej konfiguracji jednokierunkowe tokeny SMS i OATH nie działać, ponieważ powitania serwera usługi MFA nie można zainicjować pomyślnej odpowiedzi żądania RADIUS przy użyciu protokołów alternatywnych.

![Uwierzytelnianie usługi Radius](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>Dodawanie klienta usługi RADIUS
Uwierzytelnianie usługi RADIUS tooconfigure, hello instalacji serwera usługi Azure Multi-Factor Authentication w systemie Windows server. Jeśli masz środowiska usługi Active Directory, serwer hello powinien być toohello przyłączone do domeny w sieci hello. Użyj hello następujące procedury tooconfigure powitania serwera usługi Azure Multi-Factor Authentication:

1. Na powitania serwera usługi Azure Multi-Factor Authentication kliknij ikonę uwierzytelnianie usługi RADIUS hello w menu po lewej stronie powitania.
2. Sprawdź hello **Włącz uwierzytelnianie usługi RADIUS** wyboru.
3. Na karcie klientom Witaj Jeśli hello usługi Azure MFA RADIUS musi toolisten żądań RADIUS na portach niestandardowym zmienić hello uwierzytelnianie i porty ewidencjonowania aktywności.
4. Kliknij pozycję **Dodaj**.
5. Wprowadź adres IP hello hello urządzenia/serwera, który będzie się uwierzytelniał toohello serwera usługi Azure Multi-Factor Authentication, nazwy aplikacji (opcjonalnie) i wspólny klucz tajny.

  Nazwa aplikacji Hello jest wyświetlana w raportach usługi Azure Multi-Factor Authentication i może być wyświetlany w komunikatach uwierzytelniania wiadomości SMS lub aplikacji mobilnej.

  Hello udostępnionego hello toobe tajny potrzeb identyczna w obu powitania serwera usługi Azure Multi-Factor Authentication i urządzenia/serwera.

6. Sprawdź hello **dopasowania użytkownika wymagają uwierzytelniania wieloskładnikowego** Jeśli wszyscy użytkownicy zostały lub zostaną zaimportowane na powitania serwera i uwierzytelniania wieloskładnikowego toomulti podmiotu. Jeśli duża liczba użytkowników nie zostały zaimportowane na powitania serwera i/lub będą wykluczone z weryfikacji dwuetapowej, nie zaznaczaj hello pola wyboru.
7. Sprawdź hello **Włącz rezerwowy token OATH** polu toouse kodów OATH z aplikacji mobilnych weryfikacji jako połączenie telefoniczne rezerwowy toohello poza pasmem, programu SMS, lub powiadomienie wypychane.
8. Kliknij przycisk **OK**.

Powtórz kroki od 4 do 8 tooadd dowolną liczbę dodatkowych klientów usługi RADIUS, zgodnie z potrzebami.

## <a name="configure-your-radius-client"></a>Konfigurowanie klienta usługi RADIUS

1. Kliknij przycisk hello **docelowej** kartę.
2. Jeśli powitania serwera usługi Azure MFA jest zainstalowany na serwerze przyłączonym do domeny w środowisku usługi Active Directory, wybierz opcję Domena systemu Windows.
3. Jeśli użytkownicy mają być uwierzytelniani względem katalogu LDAP, wybierz pozycję **Powiązanie z protokołem LDAP**.

  toouse wiązanie LDAP, kliknij ikonę integracji katalogów hello i edytować hello konfiguracji katalogu LDAP na karcie Ustawienia hello, tak aby hello serwera wiązać tooyour katalogu. Instrukcje dotyczące konfigurowania LDAP można znaleźć w hello [przewodnik konfiguracji serwera Proxy LDAP](multi-factor-authentication-get-started-server-ldap.md).

4. Jeśli użytkownicy mają być uwierzytelniani względem innego serwera RADIUS, wybierz co najmniej jeden serwer RADIUS.
5. Kliknij przycisk **Dodaj** żądań tooconfigure powitania serwera toowhich powitania serwera usługi Azure MFA zostanie proxy hello RADIUS.
6. Okno dialogowe Dodawanie serwera RADIUS hello wprowadź adres IP hello powitania serwera usługi RADIUS i wspólny klucz tajny.

  Hello udostępnionego hello toobe tajny potrzeb identyczna w obu powitania serwera usługi Azure Multi-Factor Authentication i serwera RADIUS. Jeśli inne porty są używane przez serwer RADIUS hello zmienić hello port uwierzytelniania i ewidencjonowania aktywności.

7. Kliknij przycisk **OK**.
8. Dodaj powitania serwera usługi Azure MFA jako klient usługi RADIUS w hello innego serwera RADIUS, dzięki czemu może przetwarzać żądań dostępu wysyłane tooit z powitania serwera usługi Azure MFA. Użyj hello sam wspólny klucz tajny skonfigurowane w powitania serwera usługi Azure Multi-Factor Authentication.

Powtórz te kroki tooadd więcej serwerów usługi RADIUS i skonfiguruj hello kolejność, w których powitania serwera usługi Azure MFA powinny wywoływać je z hello **Przenieś w górę** i **Przenieś w dół** przycisków.

Na tym kończy się hello konfiguracji serwera usługi Azure Multi-Factor Authentication. powitania serwera jest teraz nasłuchiwanie hello skonfigurowane porty dla żądań dostępu usługi RADIUS od klientów hello skonfigurowane.   

## <a name="radius-client-configuration"></a>Konfiguracja klienta RADIUS
tooconfigure powitania klienta usługi RADIUS, należy użyć hello wytyczne:

* Skonfiguruj tooauthenticate Twojego urządzenia/serwera za pomocą adresu IP toohello Azure Multi-Factor Authentication serwera RADIUS, które będą działać jako serwer RADIUS hello.
* Użyj hello sam wspólny klucz tajny, który został wcześniej skonfigurowany.
* Skonfiguruj hello RADIUS limitu czasu too30 60 sekund, dzięki czemu jest czas toovalidate hello poświadczenia użytkownika, przeprowadzenia weryfikacji dwuetapowej otrzymał ich odpowiedzi i następnie odpowiadać żądanie dostępu toohello RADIUS.
