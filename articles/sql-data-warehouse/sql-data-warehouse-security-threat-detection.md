---
title: "aaaGet wprowadzenie wykrywanie zagrożeń magazynu danych SQL"
description: "Jak tooget pracę z wykrywanie zagrożeń"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a>Rozpoczynanie pracy z wykrywanie zagrożeń
> [!div class="op_single_selector"]
> * [Inspekcja](sql-data-warehouse-auditing-overview.md)
> * [Wykrywanie zagrożeń](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a>Omówienie
Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazujące toohello zagrożenia potencjalnych zabezpieczeń bazy danych. Wykrywanie zagrożeń jest w wersji zapoznawczej i jest obsługiwana dla usługi SQL Data Warehouse.

Wykrywanie zagrożeń udostępnia nową warstwę zabezpieczeń, co umożliwia klientom toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania, zapewniając alerty zabezpieczeń w nietypowych działań. Użytkownicy mogą Eksploruj hello zdarzenia podejrzane przy użyciu [inspekcję magazynu danych SQL Azure](sql-data-warehouse-auditing-overview.md) toodetermine, jeśli są one wynikiem tooaccess próby naruszenia lub wykorzystać hello magazynu danych programu.
Wykrywanie zagrożeń umożliwia proste tooaddress potencjalne zagrożenia danych toohello magazynu bez toobe potrzeby hello ekspert zabezpieczeń lub zarządzać zabezpieczeniami zaawansowanymi, monitorowanie systemów.

Na przykład wykrywanie zagrożeń wykrywa niektóre działania nietypowych bazy danych, które wskazują potencjalne prób iniekcji kodu SQL. Iniekcja kodu SQL jest jednym z hello typowych problemów sieci Web aplikacji zabezpieczeń na powitania internetowe, aplikacje używane tooattack opartych na danych. Osoby atakujące korzystać z aplikacji tooinject luk w zabezpieczeniach złośliwego instrukcji SQL do pola wejścia aplikacji, naruszenia i modyfikacji danych w bazie danych hello.

## <a name="set-up-threat-detection-for-your-database"></a>Skonfiguruj wykrywanie zagrożeń dla bazy danych
1. Uruchom hello portalu Azure pod adresem [https://portal.azure.com](https://portal.azure.com).
2. Przejdź bloku konfiguracji toohello hello ma toomonitor usługi SQL Data Warehouse. W bloku ustawienia hello, wybierz **Inspekcja i wykrywanie zagrożeń**.
   
    ![Okienko nawigacji][1]
3. W hello **Inspekcja i wykrywanie zagrożeń** Włącz bloku konfiguracji **ON** inspekcji, które będzie wyświetlane ustawienia wykrywania zagrożeń hello.
   
    ![Okienko nawigacji][2]
4. Włącz **ON** wykrywanie zagrożeń.
5. Skonfiguruj listę hello wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowych danych magazynu działań.
6. Kliknij przycisk **zapisać** w hello **Inspekcja i wykrywanie zagrożeń** toosave bloku konfiguracji hello nowych lub zaktualizowanych inspekcji i zagrożeń zasady wykrywania.
   
    ![Okienko nawigacji][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a>Eksplorowanie danych nietypowych działań magazynu po wykryciu podejrzanych zdarzeń
1. Otrzymasz wiadomość e-mail z powiadomieniem po wykryciu nietypowe działania bazy danych. <br/>
   e-mail Hello dostarcza informacji o zdarzeń zabezpieczeń podejrzane hello tym rodzaj hello hello nietypowych działań, nazwa bazy danych, server name i hello czas trwania zdarzenia. Ponadto zawierają informacje dotyczące możliwe przyczyny i zalecane akcje tooinvestigate i ograniczyć hello potencjalne zagrożenie toohello w bazie danych.<br/>
   
    ![Okienko nawigacji][4]
2. W wiadomości powitania kliknij hello **dziennik inspekcji SQL Azure** łącza, co spowoduje uruchomienie hello klasycznego portalu Azure i wyświetlić odpowiednie rekordy inspekcji hello wokół czasu hello hello podejrzane zdarzenia.
   
    ![Okienko nawigacji][5]
3. Polecenie tooview rekordów inspekcji hello więcej szczegółów na powitania bazy danych podejrzane działania, takie jak instrukcji SQL, Niepowodzenie IP Przyczyna i klienta.
   
    ![Okienko nawigacji][6]
4. W bloku rekordów inspekcji powitania kliknij **Otwórz w programie Excel** tooopen wstępnie skonfigurowane w programie excel tooimport szablonu i wykonywania dokładniejszej analizy dziennika inspekcji hello wokół czasu hello hello podejrzane zdarzenia.<br/>
   **Uwaga:** programu Excel 2010 lub nowszej, dodatku Power Query i hello **szybkie łączenie** ustawienie jest wymagane
   
    ![Okienko nawigacji][7]
5. Witaj tooconfigure **szybkie łączenie** ustawienie - hello **dodatku POWER QUERY** karty wstążki, wybierz opcję **opcje** toodisplay hello opcje w oknie dialogowym. Zaznacz hello sekcji prywatności i wybierz opcję drugi hello — "Ignoruj hello poziomów prywatności i potencjalne poprawianie wydajności":
   
    ![Okienko nawigacji][8]
6. tooload dzienników inspekcji SQL, upewnij się, że parametry hello na karcie Ustawienia hello są poprawnie ustawione i wybierz wstążki "Dane" hello i kliknij przycisk "Odśwież wszystko" hello.
   
    ![Okienko nawigacji][9]
7. Witaj wyniki są wyświetlane na powitania **dzienników inspekcji SQL** arkusza, co pozwala toorun dokładniejszej analizy hello nietypowych działań, które zostały wykryte i ograniczyć wpływ hello hello zdarzeń zabezpieczeń w aplikacji.

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
