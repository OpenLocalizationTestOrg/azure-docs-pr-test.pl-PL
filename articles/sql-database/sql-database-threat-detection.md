---
title: "aaaThreat wykrywania — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazujące toohello zagrożenia potencjalnych zabezpieczeń bazy danych."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a>Wykrywanie zagrożeń bazy danych SQL

SQL wykrywanie zagrożeń wykrywa nietypowe działania wskazują nietypowe i potencjalnie szkodliwe prób tooaccess lub wykorzystać baz danych.

## <a name="overview"></a>Omówienie

Wykrywanie zagrożeń SQL zawiera nową warstwę zabezpieczeń, co umożliwia klientom toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania, zapewniając alerty zabezpieczeń w nietypowych działań.  Użytkownicy będą otrzymywać alert po bazy danych podejrzanych działań, potencjalnych luk i ataki, a także bazy danych nietypowe wzorce dostępu. Wykrywanie zagrożeń SQL alerty zawierają szczegółowe informacje o podejrzanych działaniach i zalecane działania dotyczące tooinvestigate i uniknięcie hello zagrożenia. Użytkownicy mogą Eksploruj hello zdarzenia podejrzane przy użyciu [SQL Database Auditing](sql-database-auditing.md) toodetermine, jeśli są one wynikiem tooaccess próby naruszenia lub wykorzystania danych w bazie danych hello. Wykrywanie zagrożeń umożliwia proste tooaddress potencjalne zagrożenia toohello bazy danych bez toobe potrzeby hello ekspert zabezpieczeń lub zarządzać zabezpieczeniami zaawansowanymi, monitorowanie systemów.

Na przykład iniekcja kodu SQL jest jednym z hello typowych problemów sieci Web aplikacji zabezpieczeń na powitania internetowe, aplikacje używane tooattack opartych na danych. Osoby atakujące korzystać z tooinject luk w zabezpieczeniach aplikacji złośliwego instrukcji SQL do pola wejścia aplikacji, mogą spowodować lub modyfikowanie danych w bazie danych hello.

Wykrywanie zagrożeń SQL integruje alerty z [Centrum zabezpieczeń Azure](https://azure.microsoft.com/en-us/services/security-center/), a każdy chroniony serwer bazy danych SQL zostanie rozliczony na powitania same ceny warstwy standardowa Centrum zabezpieczeń Azure, w $15 węzła/miesięcznie, gdzie każdy chronione SQL Serwer bazy danych jest liczone jako jeden węzeł. Zachęcamy tootry go przez 60 dni do zwolnienia. 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a>Skonfiguruj wykrywanie zagrożeń dla bazy danych w hello portalu Azure
1. Uruchamianie hello Azure w portalu [https://portal.azure.com](https://portal.azure.com).
2. Przejdź bloku konfiguracji toohello hello ma toomonitor bazy danych SQL. W bloku ustawienia hello, wybierz **Inspekcja i wykrywanie zagrożeń**. 
    ![Okienko nawigacji][1]
3. W hello **Inspekcja i wykrywanie zagrożeń** Włącz bloku konfiguracji **ON** inspekcji, w którym będą wyświetlane ustawienia wykrywania zagrożeń hello.
  
    ![Okienko nawigacji][2]
4. Włącz **ON** wykrywanie zagrożeń.
5. Skonfiguruj listę hello wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowe działania bazy danych.
6. Kliknij przycisk **zapisać** w hello **Inspekcja i wykrywanie zagrożeń** toosave bloku hello nowych lub zaktualizowanych inspekcji i zagrożeń ustawienia wykrywania.
       
    ![Okienko nawigacji][3]

## <a name="set-up-threat-detection-using-powershell"></a>Skonfiguruj wykrywanie zagrożeń przy użyciu programu PowerShell

Na przykład skryptu, zobacz [konfigurowania inspekcji i wykrywania zagrożeń przy użyciu programu PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a>Eksploruj nietypowe działania bazy danych w przypadku wykrycia podejrzanych zdarzeń
1. Otrzymasz wiadomość e-mail z powiadomieniem po wykryciu nietypowe działania bazy danych. <br/>
   Hello poczty e-mail będzie zawierał informacje w tym rodzaj hello hello nietypowych działań, nazwa bazy danych, nazwę serwera, nazwa aplikacji i czas trwania zdarzenia hello zdarzenia zabezpieczeń podejrzane hello. Ponadto hello poczty e-mail zawierają informacje dotyczące przyczyny i zalecane akcje tooinvestigate i ograniczyć hello potencjalne zagrożenie toohello w bazie danych.<br/>
     
    ![Okienko nawigacji][4]
2. alerty e-mail Hello zawiera dziennik inspekcji SQL toohello bezpośredniego łącza. Kliknięcie tego łącza spowoduje uruchomienie hello Azure portal i otwiera hello SQL rekordów inspekcji wokół czasu hello hello podejrzane zdarzenia. Polecenie tooview rekordów inspekcji więcej szczegółów na powitania podejrzane bazy danych działań, dzięki czemu można łatwiej toofind hello instrukcji SQL, które zostały wykonane (kto uzyskiwał dostęp do, co zostało i kiedy) i określenie, czy zdarzenie hello uzasadnionych lub złośliwymi (np. aplikacji wydaniem iniekcji tooSQL luki w zabezpieczeniach, kogoś naruszone poufnych danych itp.).<br/>
   ![Okienko nawigacji][5]


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a>Eksploruj alertów wykrywania zagrożeń dla bazy danych w hello portalu Azure

Wykrywanie zagrożeń bazy danych SQL integruje się jego alerty z [Centrum zabezpieczeń Azure](https://azure.microsoft.com/en-us/services/security-center/). Na żywo Kafelek zabezpieczenia SQL w bloku bazy danych hello hello Azure śledzi portalu hello stan active zagrożeń. 

   ![Okienko nawigacji][6]
   
1. Kliknięcie kafelka zabezpieczeń SQL hello uruchamia blok alerty Centrum zabezpieczeń Azure hello i zawiera omówienie active zagrożeń SQL wykryte na powitania bazy danych. 

  ![Okienko nawigacji][7]

2. Kliknij określony alert zawiera dodatkowe szczegóły oraz do badania tego zagrożenia i korygowania przyszłych zagrożenia.

  ![Okienko nawigacji][8]


## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o wykrywanie zagrożeń, odwiedź hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/) 
* Dowiedz się więcej o [inspekcja bazy danych SQL Azure](sql-database-auditing.md)
* Dowiedz się więcej o [Centrum zabezpieczeń Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)
* Aby uzyskać więcej informacji o cenach, zobacz hello [stronie cennika bazy danych SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)  
* Na przykład skryptu programu PowerShell, zobacz [konfigurowania inspekcji i wykrywania zagrożeń przy użyciu programu PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


