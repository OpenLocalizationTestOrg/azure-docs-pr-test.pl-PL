---
title: "aaaRDG i korzystanie z usługi RADIUS serwera usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Jest to hello Azure Multi-Factor authentication strony przydatnej wdrażania bramy usług pulpitu zdalnego (RD) i Azure przy użyciu usługi RADIUS serwera Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fd280e9b6ff90c82927cffe593c4f1fda7047842
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a>Brama usług pulpitu zdalnego i serwer Azure Multi-Factor Authentication korzystające z usługi RADIUS
Często bramy usług pulpitu zdalnego (RD) używa hello użytkowników lokalnych tooauthenticate usług zasad sieciowych (NPS). W tym artykule opisano, jak tooroute RADIUS żąda się od hello bramy usług pulpitu zdalnego (za pośrednictwem hello lokalny serwer NPS) toohello aplikacji serwer Multi-Factor Authentication. Witaj w połączeniu z usługą Azure MFA bramy usług pulpitu zdalnego oznacza użytkownikom dostęp do swoich środowiskach pracy z dowolnego miejsca podczas wykonywania silnego uwierzytelniania. 

Ponieważ uwierzytelnianie systemu Windows dla usług terminalowych nie jest obsługiwana dla Server 2012 R2, należy użyć toointegrate bramy usług pulpitu zdalnego i usługi RADIUS z serwera usługi MFA. 

Powitania serwera usługi Azure Multi-Factor Authentication należy zainstalować na osobnym serwerze, którego serwera proxy hello PROMIEŃ żądania kopii toohello serwera NPS na powitania serwera bramy usług pulpitu zdalnego. Po NPS weryfikuje hello nazwy użytkownika i hasła, zwraca odpowiedź toohello aplikacji serwer Multi-Factor Authentication. Następnie powitania serwera usługi MFA wykonuje hello drugiego etapu uwierzytelniania i zwraca wynik toohello bramy.

## <a name="prerequisites"></a>Wymagania wstępne

- Przyłączony do domeny serwer Azure MFA. Jeśli nie masz już zainstalowany, wykonaj kroki hello w [wprowadzenie powitania serwera usługi Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server.md).
- Brama usług pulpitu zdalnego uwierzytelniana za pomocą usług Network Policy Services.

## <a name="configure-hello-remote-desktop-gateway"></a>Skonfiguruj hello bramy usług pulpitu zdalnego
Skonfiguruj hello bramy usług pulpitu zdalnego toosend RADIUS uwierzytelniania tooan serwera usługi Azure Multi-Factor Authentication. 

1. W Menedżerze bramy usług pulpitu zdalnego, kliknij prawym przyciskiem myszy nazwę serwera hello i wybierz **właściwości**.
2. Przejdź toohello **magazynu zasad RD CAP** i wybierz **centralnym serwerze NPS**. 
3. Dodaj jeden lub więcej serwerów uwierzytelnianie wieloskładnikowe Azure jako serwery RADIUS, wprowadzając hello nazwę lub adres IP każdego serwera. 
4. Utwórz wspólny klucz tajny dla każdego serwera.

## <a name="configure-nps"></a>Konfigurowanie serwera NPS
Witaj bramy usług pulpitu zdalnego używa serwera NPS toosend hello PROMIEŃ żądania tooAzure usługi Multi-Factor Authentication. tooconfigure serwera NPS, najpierw możesz zmienić ustawienia limitu czasu hello tooprevent hello bramy usług pulpitu zdalnego z przekroczeniem limitu czasu przed ukończeniem weryfikacji dwuetapowej hello ma. Następnie należy zaktualizować uwierzytelnienia usługi RADIUS tooreceive serwera NPS z serwera usługi MFA. Użyj hello następujące procedury tooconfigure serwera NPS:

### <a name="modify-hello-timeout-policy"></a>Modyfikowanie zasad limitu czasu hello

1. Na serwerze NPS Otwórz hello **klientów usługi RADIUS i serwer** w hello lewego kolumny i wybierz menu **grup serwerów zdalnych RADIUS**. 
2. Wybierz hello **grupy serwerów bramy usług terminalowych**. 
3. Przejdź toohello **równoważenia obciążenia** kartę. 
4. Zmiana obu hello **liczba sekund bez odpowiedzi, zanim żądanie zostanie uznane za** i hello **liczba sekund między żądaniami, gdy serwer jest identyfikowany jako niedostępny** toobetween 30 i 60 Liczba sekund. (Jeśli okaże się, że na tym serwerze hello nadal upłynie limit czasu podczas uwierzytelniania, można potem wróć tutaj i zwiększyć hello liczbę sekund.)
5. Przejdź toohello **konto uwierzytelnianiaprogramu/** i sprawdź, czy porty RADIUS hello określony hello dopasowania porty tego hello nasłuchuje serwer Multi-Factor Authentication.

### <a name="prepare-nps-tooreceive-authentications-from-hello-mfa-server"></a>Przygotowanie serwera NPS tooreceive uwierzytelnienia z powitania serwera usługi MFA

1. Kliknij prawym przyciskiem myszy **klientów RADIUS** w obszarze klientów usługi RADIUS i serwerach w hello lewego kolumny i wybierz **nowy**.
2. Dodaj powitania serwera usługi Azure Multi-Factor Authentication jako klient usługi RADIUS. Wybierz przyjazną nazwę i określ wspólny klucz tajny.
3. Otwórz hello **zasady** w hello lewego kolumny i wybierz menu **zasady żądań połączeń**. Powinny zostać wyświetlone zasady o nazwie ZASADY AUTORYZACJI BRAMY USŁUG TERMINALOWYCH, które zostały utworzone podczas konfigurowania bramy usług pulpitu zdalnego. Ta zasada przesyła dalej toohello żądań RADIUS aplikacji serwer Multi-Factor Authentication.
4. Kliknij prawym przyciskiem pozycję **ZASADY AUTORYZACJI BRAMY USŁUG TERMINALOWYCH**, a następnie wybierz pozycję **Duplikuj zasady**. 
5. Otwórz nowe zasady, a następnie przejść toohello hello **warunki** kartę.
6. Dodaj warunek, który odpowiada powitania klienta przyjazną nazwę o przyjaznej nazwie hello w kroku 2 powitania klienta usługi Azure Multi-Factor Authentication serwera RADIUS. 
7. Przejdź toohello **ustawienia** i wybierz **uwierzytelniania**.
8. Zmień hello dostawcy uwierzytelniania za**uwierzytelniania żądań na tym serwerze**. Ta zasada zapewnia, że gdy NPS otrzymuje żądania RADIUS od powitania serwera usługi Azure MFA, uwierzytelnianie hello odbywa się lokalnie, zamiast wysyłać PROMIEŃ żądania wstecz toohello Azure aplikacji serwer Multi-Factor Authentication, co spowoduje warunek pętli. 
9. tooprevent warunek pętli, upewnij się, że hello nowe zasady porządkowania powyżej hello oryginalnymi zasadami w hello **zasady żądań połączeń** okienka.

## <a name="configure-azure-multi-factor-authentication"></a>Konfigurowanie usługi Azure Multi-Factor Authentication

powitania serwera usługi Azure Multi-Factor Authentication jest skonfigurowany jako serwer proxy RADIUS między bramą usług pulpitu zdalnego i serwera NPS.  Powinien być zainstalowany na serwerze przyłączonym do domeny, który różni się od powitania serwera bramy usług pulpitu zdalnego. Witaj użyj następującej procedury tooconfigure powitania serwera usługi Azure Multi-Factor Authentication.

1. Otwórz powitania serwera usługi Azure Multi-Factor Authentication i wybierz ikonę uwierzytelnianie usługi RADIUS hello. 
2. Sprawdź hello **Włącz uwierzytelnianie usługi RADIUS** wyboru.
3. Na karcie klientom Witaj, upewnij się, porty hello odpowiada elementom skonfigurowanym na serwerze NPS, a następnie wybierz **Dodaj**.
4. Dodaj adres IP serwera bramy usług pulpitu zdalnego hello, nazwy aplikacji (opcjonalnie) i wspólny klucz tajny. Hello udostępnionych tajny potrzeb toobe hello takie same na powitania serwera usługi Azure Multi-Factor Authentication i bramy usług pulpitu zdalnego.
3. Przejdź toohello **docelowej** kartę i wybierz hello **serwery RADIUS** przycisk radiowy.
4. Wybierz **Dodaj** , a następnie wprowadź adres IP hello, Wspólny klucz tajny i portów powitania serwera NPS. Jeśli przy użyciu centralnej serwera NPS, powitania klienta RADIUS i cel serwera RADIUS są hello tego samego. Witaj wspólny klucz tajny musi być zgodna hello jednej konfiguracji w powitania klienta RADIUS części powitania serwera NPS.

![Uwierzytelnianie usługi Radius](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a>Następne kroki

- Zintegruj usługę Azure MFA z [aplikacjami sieci Web usługi IIS](multi-factor-authentication-get-started-server-iis.md)

- Uzyskaj odpowiedzi w hello [Azure Multi-Factor Authentication — często zadawane pytania](multi-factor-authentication-faq.md)
