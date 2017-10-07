---
title: "Analiza strumienia: Obracanie poświadczenia logowania dla danych wejściowych i wyjściowych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupdate hello poświadczeń dla usługi analiza strumienia danych wejściowych i wyjściowych."
keywords: "poświadczenia logowania"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Obróć poświadczenia logowania dla wejścia i wyjścia w zadania usługi analiza strumienia
## <a name="abstract"></a>Abstrakcyjny
Usługa Azure Stream Analytics obecnie nie zezwala na zastępowanie hello poświadczeń na wejścia/wyjścia zadania hello jest uruchomiona.

Gdy Azure Stream Analytics obsługuje wznawianie zadania z ostatnich danych wyjściowych, możemy tooshare hello całego procesu dla minimalizując hello zwłokę między hello zatrzymywanie i uruchamianie zadania hello i obracanie hello poświadczenia logowania.

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>Część 1 — Przygotowanie hello nowy zestaw poświadczeń:
Ta część jest zastosowanie toohello po wejść/wyjść:

* Blob Storage
* Usługa Event Hubs
* SQL Database
* Table Storage

Dla innych wejść/wyjść przejdź do części 2.

### <a name="blob-storagetable-storage"></a>Magazyn obiektów blob magazynu/tabeli.
1. Przejdź toohello rozszerzenie magazynu w portalu zarządzania Azure hello:  
   ![graphic1][graphic1]
2. Zlokalizuj hello Magazyn używany przez zadanie, a następnie przejdź w niej:  
   ![graphic2][graphic2]
3. Kliknij polecenie Zarządzaj kluczami dostępu hello:  
   ![graphic3][graphic3]
4. Między hello podstawowy klucz dostępu i hello pomocniczy klucz dostępu **wybierz hello, co nie jest używany przez zadanie**.
5. Regenerate trafień:  
   ![graphic4][graphic4]
6. Skopiuj hello nowo wygenerować klucz:  
   ![graphic5][graphic5]
7. Nadal tooPart 2.

### <a name="event-hubs"></a>Centra zdarzeń
1. Przejdź toohello rozszerzenia usługi Service Bus w portalu zarządzania Azure hello:  
   ![graphic6][graphic6]
2. Zlokalizuj hello Namespace magistrali usługi używane przez zadanie, a następnie przejdź w niej:  
   ![graphic7][graphic7]
3. Jeśli zadanie używa zasady dostępu współużytkowanego na powitania Namespace magistrali usług, przejście toostep 6  
4. Przejdź na kartę usługi Event Hubs toohello:  
   ![graphic8][graphic8]
5. Zlokalizuj hello używane przez zadanie Centrum zdarzeń i przejdź do niej:  
   ![graphic9][graphic9]
6. Przejdź toohello kartę Konfiguracja:  
   ![graphic10][graphic10]
7. Na powitania listy rozwijanej nazwę zasady Znajdź zasad dostępu hello udostępnionych używanych przez zadania:  
   ![graphic11][graphic11]
8. Między hello klucz podstawowy i klucz pomocniczy hello **wybierz hello, co nie jest używany przez zadanie**.  
9. Regenerate trafień:  
   ![graphic12][graphic12]
10. Skopiuj hello nowo wygenerować klucz:  
   ![graphic13][graphic13]
11. Nadal tooPart 2.  

### <a name="sql-database"></a>SQL Database
> [!NOTE]
> Uwaga: należy toohello tooconnect usługi baza danych SQL. Za chwilę tooshow jak toodo to przy użyciu hello możliwości zarządzania na hello portalu zarządzania Azure, ale można wybrać toouse niektórych po stronie klienta narzędzia, takiego jak SQL Server Management Studio również.
>
> 

1. Przejdź toohello rozszerzenia bazy danych SQL w portalu zarządzania Azure hello:  
   ![graphic14][graphic14]
2. Zlokalizuj hello bazy danych SQL używane przez zadania i **kliknij na powitania serwera** łącze hello sam wiersza:  
   ![graphic15][graphic15]
3. Kliknij polecenie Zarządzaj hello:  
   ![graphic16][graphic16]
4. Typ główny bazy danych:  
   ![graphic17][graphic17]
5. Wpisz nazwę użytkownika, hasło i kliknij przycisk Zaloguj:  
   ![graphic18][graphic18]
6. Kliknij pozycję Nowa kwerenda:  
   ![graphic19][graphic19]
7. Typ w hello następującego zapytania, zastępując < login_name > z nazwą użytkownika i zastępowanie <enterStrongPasswordHere> przy użyciu nowego hasła:  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. Kliknij przycisk Uruchom:  
   ![graphic20][graphic20]
9. Wróć toostep 2 i tym razem kliknij hello bazy danych:  
   ![graphic21][graphic21]
10. Kliknij polecenie Zarządzaj hello:  
   ![graphic22][graphic22]
11. Wpisz nazwę użytkownika, hasło i kliknij przycisk logowania:  
   ![graphic23][graphic23]
12. Kliknij pozycję Nowa kwerenda:  
   ![graphic24][graphic24]
13. Wpisz hello następującego zapytania, zastępując < nazwa_użytkownika > o nazwie, przez którą ma tooidentify tej nazwy logowania w kontekście hello tej bazy danych (możesz podać tę samą wartość nadana < login_name >, na przykład Witaj) i zastępowanie < login_name > Nowa nazwa użytkownika:  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. Kliknij przycisk Uruchom:  
   ![graphic25][graphic25]
15. Teraz należy zapewnić nowego użytkownika z hello tego samego ról oraz uprawnień miał oryginalny użytkownika.
16. Nadal tooPart 2.

## <a name="part-2-stopping-hello-stream-analytics-job"></a>Część 2: Hello zatrzymywania zadania usługi analiza strumienia
1. Przejdź toohello rozszerzenia usługi Stream Analytics w portalu zarządzania Azure hello:  
   ![graphic26][graphic26]
2. Znajdź swoją pracę i przejdź do niej:  
   ![graphic27][graphic27]
3. Przejdź toohello danych wejściowych karty lub hello wyniki według tego, czy są obracanie hello poświadczeń na danych wejściowych lub wyjściowych.  
   ![graphic28][graphic28]
4. Kliknij polecenie zatrzymania hello i upewnij się, że zadanie powitania przestał:  
   ![graphic29][graphic29] poczekaj, aż hello toostop zadania.
5. Zlokalizuj hello wejścia/wyjścia ma poświadczenia toorotate na i przejdź do niej:  
   ![graphic30][graphic30]
6. Kontynuować tooPart 3.

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>Część 3: Edytowanie hello poświadczeń na powitania zadania usługi analiza strumienia
### <a name="blob-storagetable-storage"></a>Magazyn obiektów blob magazynu/tabeli.
1. Znajdź pole klucz konta magazynu hello i wkleić klucz wygenerowanym:  
   ![graphic31][graphic31]
2. Kliknij polecenie Zapisz hello i Potwierdź zapisywania zmian:  
   ![graphic32][graphic32]
3. Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, to znaczy został pomyślnie przekazany.
4. Kontynuować tooPart 4.

### <a name="event-hubs"></a>Centra zdarzeń
1. Znajdź pole klucza zasad Centrum zdarzeń hello i wkleić klucz wygenerowanym:  
   ![graphic33][graphic33]
2. Kliknij polecenie Zapisz hello i Potwierdź zapisywania zmian:  
   ![graphic34][graphic34]
3. Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, że został przekazany pomyślnie.
4. Kontynuować tooPart 4.

### <a name="power-bi"></a>Power BI
1. Kliknij hello odnawiania autoryzacji:  

   ![graphic35][graphic35]
2. Otrzymasz powitania po potwierdzeniu:  

   ![graphic36][graphic36]
3. Kliknij polecenie Zapisz hello i Potwierdź zapisywania zmian:  
   ![graphic37][graphic37]
4. Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, że jej został pomyślnie przekazany.
5. Kontynuować tooPart 4.

### <a name="sql-database"></a>SQL Database
1. Znajdź hello pola Nazwa użytkownika i hasło i Wklej nowo utworzonego zestawu poświadczeń do nich:  
   ![graphic38][graphic38]
2. Kliknij polecenie Zapisz hello i Potwierdź zapisywania zmian:  
   ![graphic39][graphic39]
3. Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, że został przekazany pomyślnie.  
4. Kontynuować tooPart 4.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>Część 4: Uruchamianie zadania od ostatniego zatrzymania
1. Opuścić hello wejścia/wyjścia:  
   ![graphic40][graphic40]
2. Kliknij polecenie Start hello:  
   ![graphic41][graphic41]
3. Wybierz hello czas ostatniego zatrzymania, a następnie kliknij przycisk OK:  
   ![graphic42][graphic42]
4. Kontynuować tooPart 5.  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>Część 5: Usuwanie hello stary zestaw poświadczeń
Ta część jest zastosowanie toohello po wejść/wyjść:

* Blob Storage
* Usługa Event Hubs
* SQL Database
* Table Storage

### <a name="blob-storagetable-storage"></a>Magazyn obiektów blob magazynu/tabeli.
Powtórz część 1 dla hello klucz dostępu, który był wcześniej używany przez zadanie toorenew hello teraz nieużywane klucz dostępu.

### <a name="event-hubs"></a>Centra zdarzeń
Powtórz część 1 dla hello klucz, który był wcześniej używany przez zadanie toorenew hello teraz nieużywane klucza.

### <a name="sql-database"></a>SQL Database
1. Przejdź wstecz toohello oknie zapytania z część 1 krok 7 i wpisz hello następującego zapytania, zastępując < previous_login_name > hello nazwę użytkownika, który był wcześniej używany przez zadania:  
   `DROP LOGIN <previous_login_name>`  
2. Kliknij przycisk Uruchom:  
   ![graphic43][graphic43]  

Należy pobrać powitania po potwierdzeniu: 

    Command(s) completed successfully.

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

