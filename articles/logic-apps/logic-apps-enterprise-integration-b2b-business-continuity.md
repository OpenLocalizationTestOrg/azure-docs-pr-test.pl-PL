---
title: "odzyskiwanie aaaDisaster dla konta integracji B2B — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: Odzyskiwanie po awarii B2B aplikacje logiki
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Odzyskiwanie po awarii między region B2B aplikacje logiki

Obciążeń B2B obejmują transakcje pieniężne jak zamówienia i faktury. Podczas zdarzenia po awarii jest krytyczne w hello toomeet Odzyskaj tooquickly biznesowych, które SLA biznesowej uzgodnione z ich partnerów. W tym artykule przedstawiono, jak zaplanować obciążeń B2B toobuild ciągłość prowadzenia działalności biznesowej. 

* Gotowość odzyskiwania po awarii 
* Tryb failover toosecondary region podczas zdarzenia po awarii 
* Rezerwowe tooprimary region po zdarzeniu po awarii

## <a name="disaster-recovery-readiness"></a>Gotowość odzyskiwania po awarii  

1. Określić region pomocniczy i utworzyć [konta integracji](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) w regionie pomocniczym hello.

2. Dodaj partnerów, schematów i umów dotyczących przepływów wiadomość hello wymagane gdy hello stan uruchomienia musi toobe replikowane toosecondary region integracji konta.

   > [!TIP]
   > Upewnij się, że istnieje spójności w konwencji nazewnictwa artefaktu hello integracji konta w regionach. 

3. Witaj toopull stan uruchomienia z hello regionu podstawowego, tworzenie aplikacji logiki w regionie pomocniczym hello. 

   Ta aplikacja logiki powinny mieć *wyzwalacza* i *akcji*. 
   Hello wyzwalacza należy łączyć konta integracji regionu tooprimary i hello akcji powinna łączyć toosecondary region integracji konta. 
   W oparciu o czas hello, wyzwalacz hello sonduje tabeli stanie hello regionu podstawowego, uruchom i pobiera nowe rekordy hello, jeśli istnieje. Witaj aktualizuje je toosecondary region integracji konta. 
   Dzięki temu stanu działania przyrostowe tooget z regionu toosecondary regionu podstawowego.

4. Ciągłość prowadzenia działalności biznesowej w aplikacjach logiki integracji konto jest zaprojektowana toosupport oparte na protokołach B2B - X12, AS2 i EDIFACT. kroki szczegółowe toofind, wybierz hello odpowiednich łącza.

5. Witaj zalecenie jest toodeploy za wszystkie zasoby w regionie podstawowym w regionie pomocniczym. 

   Zasoby regionu podstawowego obejmują bazy danych SQL Azure lub bazy danych rozwiązania Cosmos platformy Azure, Azure Service Bus i usługi Azure Event Hubs, używany do obsługi wiadomości, Azure API Management i hello funkcji usługi Azure Logic Apps w usłudze Azure App Service.   

6. Nawiąż połączenie z regionu pomocniczego tooa regionu podstawowego. Witaj toopull stan uruchomienia z regionu podstawowego, tworzenie aplikacji logiki w regionie pomocniczym. 

   Aplikacja logiki Hello powinien mieć wyzwalacza i akcji. 
   wyzwalacz Hello powinien łączyć tooa regionu podstawowego integracji konta. 
   Akcja Hello powinien łączyć tooa region pomocniczy integracji konta. 
   W oparciu o czas hello, wyzwalacz hello sonduje tabeli stanie hello regionu podstawowego, uruchom i pobiera nowe rekordy hello, jeśli istnieje. 
   Witaj aktualizuje je tooa region pomocniczy integracji konta. 
   Ten proces pomaga stanu działania przyrostowe tooget hello region pomocniczy toohello regionu podstawowego.

Ciągłość prowadzenia działalności biznesowej w ramach konta integracji usługa Logic Apps zapewnia obsługę oparte na AS2, EDIFACT i protokoły B2B hello X12. Aby uzyskać szczegółowe instrukcje na temat używania X12 i AS2, zobacz [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) i [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) w tym artykule.

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a>Tryb failover region pomocniczy tooa podczas zdarzenia po awarii

Podczas zdarzenie po awarii, gdy hello regionu podstawowego nie jest dostępna dla ciągłość prowadzenia działalności biznesowej, region pomocniczy toohello bezpośredniego ruchu. Pomaga region pomocniczy, toorecover biznesowych działa szybko toomeet powitalne uzgodnione RPO/czasu odzyskania przez ich partnerów. Zmniejsza on również toofail działań za pośrednictwem z jednego regionu tooanother. 

Brak oczekiwanego opóźnienia podczas kopiowania numery kontroli z regionu pomocniczego tooa regionu podstawowego. tooavoid wysyłania zduplikowane kontroli wygenerowanego numery toopartners podczas zdarzenia po awarii, hello zaleca numery kontroli hello tooincrement w umowach region pomocniczy hello przy użyciu [poleceń cmdlet programu PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a>Zdarzenia po awarii regionu podstawowego tooa rezerwowe

regionu podstawowego wstecz tooa toofall gdy jest ona dostępna, wykonaj następujące kroki:

1. Akceptować komunikatów z partnerami w regionie pomocniczym hello.  

2. Zwiększenie liczby kontroli hello wygenerowany dla wszystkich umów regionu podstawowego hello przy użyciu [poleceń cmdlet programu PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).  

3. Bezpośrednie ruch z regionu podstawowego toohello hello regionie pomocniczym.

4. Sprawdź, czy jest włączone, aplikacja logiki hello utworzona w dodatkowej regionie hello ściąganie stan uruchomienia z hello regionu podstawowego.

## <a name="x12"></a>X12 

Ciągłość prowadzenia działalności biznesowej dla EDI X 12 dokumenty są oparte na numery kontroli:

> [!TIP]
> Można również użyć hello [X12 szybki start szablonu](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps. Tworzenie konta integracji podstawowe i pomocnicze są wymagania wstępne toouse hello szablonu. Witaj szablonu pomaga toocreate dwie aplikacje logiki, jeden dla kontroli odebranej liczby i drugi dla numery wygenerowanego kontroli. Odpowiednich wyzwalacze i akcje są tworzone w aplikacjach logiki hello, łączenie hello wyzwalacza toohello integracji podstawowego konta i hello akcji toohello dodatkowej integracji.

**Wymagania wstępne**

odzyskiwanie po awarii tooenable dla wiadomości przychodzących, wybierz hello zduplikowane Sprawdź ustawienia w ustawieniach odbierania hello X12 umowy.

![Wybierz ustawienia sprawdzania duplikatów](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. Utwórz [aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) w regionie pomocniczym.    

2. Wyszukaj **X12**i wybierz **X12-modyfikacji numer formantu**.   

   ![Wyszukaj X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   wyzwalacz Hello monituje tooestablish konto połączenia tooan integracji. 
   wyzwalacz Hello powinny być połączone konta integracji regionu podstawowego tooa.

3. Wpisz nazwę połączenia, wybierz użytkownika *regionie podstawowym konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.   

   ![Nazwa konta integracji regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. Witaj **DateTime toostart kontroli numer synchronizacji** ustawienie jest opcjonalne. Witaj **częstotliwość** można ustawić za**dzień**, **godzina**, **minutę**, lub **drugi** interwał.   

   ![Daty i godziny i częstotliwość](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. Wybierz **nowy krok** > **Dodaj akcję**.

   ![Nowy krok, Dodaj Action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. Wyszukaj **X12**i wybierz **X12-dodania lub zaktualizowania numery kontroli**.   

   ![Dodaj lub zaktualizuj numery kontroli](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. Wybierz tooconnect konto akcji tooa region pomocniczy integracji **zmienić połączenie** > **Dodaj nowe połączenie** listę hello integracji dostępnych kont. Wpisz nazwę połączenia, wybierz użytkownika *regionu pomocniczego konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**. 

   ![Nazwa konta integracji regionu pomocniczego](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. Przełącz tooraw wejść, klikając ikonę hello w prawym górnym rogu.

   ![Dane wejściowe tooraw przełącznika](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. Wybierz treść z selektora zawartości dynamicznej hello, a następnie zapisz hello aplikacji logiki.

   ![Pola zawartości dynamicznej](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   W oparciu o czas hello, wyzwalacz hello sonduje hello regionu podstawowego Odebrano kontroli numer tabeli i ściąga hello nowych rekordów. 
   Witaj aktualizuje rekordów hello hello region pomocniczy integracji konta. 
   Jeśli nie ma żadnych aktualizacji, stan wyzwalacza hello jest wyświetlany jako **pomijane**.   

   ![Kontrola numeru tabeli](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

W oparciu o czas hello, stan czasu wykonywania przyrostowych hello są replikowane z regionu pomocniczego tooa regionu podstawowego. Podczas zdarzenie po awarii, gdy hello regionu podstawowego nie jest dostępna, bezpośrednie ruchu toohello region pomocniczy dla ciągłość prowadzenia działalności biznesowej. 

## <a name="edifact"></a>EDIFACT 

Ciągłość prowadzenia działalności biznesowej dla dokumentów EDI EDIFACT opiera się na numery kontroli.

**Wymagania wstępne**

odzyskiwanie po awarii tooenable dla wiadomości przychodzących, wybierz hello zduplikowane Sprawdź ustawienia w ustawieniach odbierania umowy EDIFACT.

![Wybierz ustawienia sprawdzania duplikatów](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. Utwórz [aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) w regionie pomocniczym.    

2. Wyszukaj **EDIFACT**i wybierz **EDIFACT - modyfikacji numer formantu**.

   ![Wyszukaj EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   wyzwalacz Hello monituje tooestablish konto połączenia tooan integracji. 
   wyzwalacz Hello powinny być połączone konta integracji regionu podstawowego tooa. 

3. Wpisz nazwę połączenia, wybierz użytkownika *regionie podstawowym konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.    

   ![Nazwa konta integracji regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. Witaj **DateTime toostart kontroli numer synchronizacji** ustawienie jest opcjonalne. Witaj **częstotliwość** można ustawić za**dzień**, **godzina**, **minutę**, lub **drugi** interwał.    

   ![Daty i godziny i częstotliwość](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. Wybierz **nowy krok** > **Dodaj akcję**.    

   ![Nowy krok, Dodaj Action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. Wyszukaj **EDIFACT**i wybierz **EDIFACT - dodania lub zaktualizowania numery kontroli**.   

   ![Dodaj lub zaktualizuj numery kontroli](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. Wybierz tooconnect konto akcji tooa region pomocniczy integracji **zmienić połączenie** > **Dodaj nowe połączenie** listę hello integracji dostępnych kont. Wpisz nazwę połączenia, wybierz użytkownika *regionu pomocniczego konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.

   ![Nazwa konta integracji regionu pomocniczego](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. Przełącz tooraw wejść, klikając ikonę hello w prawym górnym rogu.

   ![Dane wejściowe tooraw przełącznika](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. Wybierz treść z selektora zawartości dynamicznej hello, a następnie zapisz hello aplikacji logiki.   

   ![Pola zawartości dynamicznej](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   W oparciu o czas hello, wyzwalacz hello sonduje hello regionu podstawowego Odebrano kontroli numer tabeli i ściąga hello nowych rekordów.
   Witaj aktualizuje hello rekordów toohello region pomocniczy integracji konta. 
   Jeśli nie ma żadnych aktualizacji, stan wyzwalacza hello jest wyświetlany jako **pomijane**.

   ![Kontrola numeru tabeli](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

W oparciu o czas hello, stan czasu wykonywania przyrostowych hello są replikowane z regionu pomocniczego tooa regionu podstawowego. Podczas zdarzenie po awarii, gdy hello regionu podstawowego nie jest dostępna, bezpośrednie ruchu toohello region pomocniczy dla ciągłość prowadzenia działalności biznesowej. 

## <a name="as2"></a>AS2 

Ciągłość prowadzenia działalności biznesowej dla dokumentów, które używają protokołu AS2 hello jest na podstawie Identyfikatora wiadomości powitania i hello Micznych wartości.

> [!TIP]
> Można również użyć hello [szablonów szybki start AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps. Tworzenie konta integracji podstawowe i pomocnicze są wymagania wstępne toouse hello szablonu. Szablon Hello ułatwia tworzenie aplikacji logiki wyzwalacza i akcji. Aplikacja logiki Hello tworzy połączenie z kontem podstawowym integracji tooa wyzwalacza i konto akcji tooa dodatkowej integracji.

1. Utwórz [aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) w regionie pomocniczym hello.  

2. Wyszukaj **AS2**i wybierz **AS2 — wartość Micznych po utworzeniu**.   

   ![Wyszukaj AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   Wyzwalacz monituje tooestablish konto połączenia tooan integracji. 
   wyzwalacz Hello powinny być połączone konta integracji regionu podstawowego tooa. 
   
3. Wpisz nazwę połączenia, wybierz użytkownika *regionie podstawowym konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.

   ![Nazwa konta integracji regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. Witaj **DateTime toostart Micznych wartość synchronizacji** ustawienie jest opcjonalne. Witaj **częstotliwość** można ustawić za**dzień**, **godzina**, **minutę**, lub **drugi** interwał.   

   ![Daty i godziny i częstotliwość](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. Wybierz **nowy krok** > **Dodaj akcję**.  

   ![Nowy krok, Dodaj Action](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. Wyszukaj **AS2**i wybierz **AS2 - dodania lub zaktualizowania zawartości Micznych**.  

   ![Dodawanie Mikrofon lub aktualizacji](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. Wybierz tooconnect konto akcji tooa dodatkowej integracji **zmienić połączenie** > **Dodaj nowe połączenie** listę hello integracji dostępnych kont. Wpisz nazwę połączenia, wybierz użytkownika *regionu pomocniczego konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.

   ![Nazwa konta integracji regionu pomocniczego](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. Przełącz tooraw wejść, klikając ikonę hello w prawym górnym rogu.

   ![Dane wejściowe tooraw przełącznika](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. Wybierz treść z selektora zawartości dynamicznej hello, a następnie zapisz hello aplikacji logiki.   

   ![Zawartość dynamiczna](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   W oparciu o czas hello, wyzwalacz hello sonduje hello regionu podstawowego tabeli i ściąga hello nowych rekordów. Witaj aktualizuje je toohello region pomocniczy integracji konta. 
   Jeśli nie ma żadnych aktualizacji, stan wyzwalacza hello jest wyświetlany jako **pomijane**.  

   ![Tabela regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

W oparciu o czas hello, stan czasu wykonywania przyrostowych hello są replikowane z regionu pomocniczego toohello hello regionu podstawowego. Podczas zdarzenie po awarii, gdy hello regionu podstawowego nie jest dostępna, bezpośrednie ruchu toohello region pomocniczy dla ciągłość prowadzenia działalności biznesowej. 

## <a name="next-steps"></a>Następne kroki

[Monitorowanie komunikatów B2B](logic-apps-monitor-b2b-message.md)

