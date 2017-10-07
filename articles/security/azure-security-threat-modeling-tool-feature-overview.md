---
title: "aaaMicrosoft narzędzia do modelowania zagrożeń - Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat wszystkich hello funkcje dostępne w hello narzędzie modelowania zagrożeń"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>Omówienie funkcji narzędzia do modelowania zagrożeń

Jesteśmy Cieszymy się, że wybrano hello toouse narzędzie modelowania zagrożeń dla Twojego zagrożeń modelowania musi! Jeśli nie zostało to jeszcze zrobione, odwiedź stronę  **[wprowadzenie do narzędzia do modelowania zagrożeń hello](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn hello podstawy.

> Naszego narzędzia są często aktualizowane, więc to przewodnik często toosee naszych najnowsze funkcje i ulepszenia.

Klikając przycisk "Utwórz nowy Model" hello otwiera stronę początkową puste, podobne toohello obraz poniżej:

![Strona początkowa pusta](./media/azure-security-threat-modeling-tool/tmtstart.png)

Przy użyciu modelu zagrożeń hello utworzone przez nasz zespół w hello  **[wprowadzenie](./azure-security-threat-modeling-tool-getting-started.md)**  przykład, załóżmy dzisiaj wyewidencjonowania w narzędziu hello wszystkie funkcje hello.

![Podstawowe zagrożenia modelu](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>Nawigacji

Przed rozpoczęciem pracy hello wbudowanych funkcji, przejdź na powitania główne składniki znaleziono w narzędziu hello

### <a name="menu-items"></a>Elementy menu

środowisko Hello powinny być podobne tooother produkty firmy Microsoft. Zacznijmy od zapoznania hello elementów menu najwyższego poziomu:

![Elementy menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| Etykieta                               | Szczegóły      |
| --------------------------------------- | ------------ |
| **Plik** | <ul><li>Otwórz, Zapisz i zamknij pliki</li><li>Konta logowania jednoportowej OneDrive</li><li>Udostępnij linki (Wyświetl i Edytuj)</li><li>Wyświetlanie informacji o pliku</li><li>Zastosuj nowy szablon tooExisting modeli</li></ul> |
| **Edytuj** | Cofnij/ponów akcji, jak również kopię, paste i delete |
| **Widok** | <ul><li>Przełączanie między **analizy** i **projekt** widoków</li><li>Zamkniętego okna (e.g.stencils i właściwości elementu wiadomości)</li><li>Zresetuj ustawienia toodefault układu</li></ul> |
| **Diagram** | Dodaj lub usuń diagramy i nawigowania "karty" diagramów |
| **Raporty** | Utwórz tooshare raporty HTML z innymi użytkownikami |
| **Pomoc** | Za pomocą narzędzia hello toohelp prowadnic |

ikony Hello są skróty do menu najwyższego poziomu hello:

| Ikona                               | Szczegóły      |
| --------------------------------------- | ------------ |
| **Otwórz** | Zostanie otwarty nowy plik |
| **Zapisz** | Zapisuje bieżący plik |
| **Projekt** | Przechodzi w widoku Projekt, w którym można utworzyć modeli |
| **Analiza** | Pokazuje wygenerowany zagrożeń i ich właściwości |
| **Dodawanie diagramu** | Dodaje nowy diagram (podobne toonew karty w programie Excel) |
| **Usuń diagramu** | Usuwa bieżącego diagramu |
| **Wycinanie/kopiowanie/wklejanie** | Elementy kopii/części/past |
| **Cofnij/ponów** | Cofa/ponowi wykonanie akcji |
| **Powiększ / pomniejszyć** | Zmienia powiększenie i diagram hello lepszego widoku |
| **Opinia** | Otwiera hello MSDN Forum |

### <a name="canvas"></a>Kanwy

Hello miejsce gdzie przeciąganie i upuszczanie elementów do. Przeciąganie i upuszczanie jest hello najszybsze i najbardziej efektywny sposób toobuild modeli. Możesz również kliknij prawym przyciskiem myszy i wybierz z menu hello dodaje ogólnego wersje elementów hello, którego używasz, jak pokazano poniżej.

#### <a name="dropping-hello-stencil-on-hello-canvas"></a>Porzucanie wzornika hello na powitania kanwy

![Upuść kanwy](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a>Kliknięcie wzornika hello

![Właściwości elementu](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>Wzorników

Gdzie można znaleźć wszystkie wzorników toouse dostępne na podstawie szablonu hello wybrane. Jeśli nie możesz znaleźć elementy prawo hello, spróbuj użyć innego szablonu, lub zmodyfikuj jeden toofit potrzeb. Ogólnie rzecz biorąc powinien być stanie toofind kombinacją kategorii, takich jak hello widocznych poniżej:

| Nazwa wzornika                               | Szczegóły      |
| --------------------------------------- | ------------ |
| **Proces** | Aplikacje, wtyczek przeglądarki wątków, maszyny wirtualne |
| **Zewnętrzny** | Dostawców uwierzytelniania, przeglądarek, użytkownicy, aplikacje sieci Web |
| **Magazyn danych** | Rejestr pliki, bazy danych, konfiguracji pamięci podręcznej, przechowywania, |
| **Przepływ danych** | Binarny, ALPC, HTTP, HTTPS/protokoły TLS/SSL, IOCTL, IPSec, o nazwie potoku, RPC i modelu DCOM, SMB, UDP |
| **Obramowanie/granic zaufania** | Sieci firmowe, Internet, maszyny, piaskownicy, trybu jądra/użytkownika |

### <a name="notesmessages"></a>Uwagi dotyczące/wiadomości

| Składnik                               | Szczegóły      |
| --------------------------------------- | ------------ |
| **Komunikaty** | Logiki wewnętrzne narzędzie, które generuje alerty dla użytkownika przy każdym wystąpieniu błędu, takie jak Brak przepływów danych między elementami |
| **Uwagi** | Ręczne uwagi pliku toohello dodanych przez zespoły inżynieryjne w całości w hello projektu i przegląd procesu |

### <a name="element-properties"></a>Właściwości elementu

Te różnią się zależnie od elementów hello wybrane. Oprócz granice zaufania wszystkie inne elementy zawierają 3 Opcje ogólne:

| Właściwości elementu                               | Szczegóły      |
| --------------------------------------- | ------------ |
| **Nazwa** | Przydatne w przypadku nazw toobe Twojego procesów, magazynów i obiektów interakcji przepływów czytelna |
| **Poza zakresem** | Jeśli zaznaczone, hello elementu jest pobierana poza macierzy generacji zagrożeń hello (niezalecane) |
| **Przyczyna poza zakresem** | Justowanie pola toolet użytkownicy wiedzieli, dlaczego poza zakresem wybrano |

Właściwości zostały zmienione w każdej kategorii elementu. Kliknij każdy element tooinspect hello dostępnych opcji lub Otwórz toolearn szablonu hello więcej. Załóż na powitania funkcji.

## <a name="welcome-screen"></a>Ekran powitalny

ekran powitalny Hello jest hello najpierw zostanie wyświetlony po otwarciu aplikacji hello.

### <a name="open-a-model"></a>Otwieranie modelu

Ustawiając kursor nad przycisk "Otwórz w modelu" zawiera opcje ukryta 2: "Otwórz w tym komputerze" i "Otwieranie z poziomu usługi OneDrive." Hello otwierania hello Otwieranie pliku ekranu, gdy hello drugi prezentująca hello logowania procesu dla usługi OneDrive, umożliwiając toopick folderów i plików po pomyślnym uwierzytelnieniu.

![Otwieranie modelu](./media/azure-security-threat-modeling-tool/openmodel.png)

![Otwórz z komputera lub usługi OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>Opinie i sugestie problemów

Wybranie tej opcji spowoduje przejście toohello fora MSDN dla narzędzi do tworzenia oprogramowania. To doskonały sposób toocheck się inne osoby mówią o narzędziu hello, w tym rozwiązania i nowe pomysły.

![Opinia](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>Widok projektu

Przy każdym otwarciu lub utworzyć nowy model spowoduje przekierowanie toohello widoku Projekt.

### <a name="adding-elements"></a>Dodawanie elementów

Istnieją 2 metody tooadd elementów siatki hello:

- **Przeciągnij i upuść** — przeciągnij hello żądany element toohello siatki, a następnie użyj hello elementu właściwości tooprovide dodatkowe informacje.
- **Kliknij prawym przyciskiem myszy** — prawym przyciskiem myszy kliknij w dowolnym miejscu na powitania siatki i wybierz z menu rozwijanego hello. Ogólny reprezentacja elementu będą wyświetlane na ekranie powitania.

### <a name="connecting-elements"></a>Łączenie elementów

Istnieją 2 metody tooconnect elementów w narzędziu hello:

- **Przeciągnij i upuść** — przeciągnij hello żądaną przepływu danych toohello siatki i połączyć z obu końców toohello odpowiednich elementów.
- **Kliknij pozycję + Shift** — kliknięcie pierwszego elementu hello (wysyłanie danych), naciśnij i przytrzymaj klawisz Shift hello, a następnie wybierz hello drugiego elementu (odbieranie danych). Kliknij prawym przyciskiem myszy i wybierz opcję "Połącz". Jeśli używasz przepływu danych dwukierunkowe hello kolejność nie jest równie ważne.

### <a name="properties"></a>Właściwości

Zawiera wszystkie właściwości hello, które mogą być modyfikowane wzorników hello umieszczone na diagramie hello. właściwości hello toosee, wystarczy kliknąć wzornika hello i hello informacje zostaną odpowiednio wypełnione. przykład Witaj poniżej przedstawia przed i po "Bazy danych" wzornika jest przeciągnięto hello diagramu:

#### <a name="before"></a>Przed

![Przed](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>Po

![Po](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>Komunikaty

Tworzenie modelu zagrożeń, pamiętaj, że dane tooconnect przepływają tooelements okna wiadomość hello powiadamia tooact. Możesz wybrać tooignore go lub wykonaj hello instrukcje toofix hello problem. 

![Komunikaty](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>Uwagi

Przełączanie kart z tooNotes wiadomości umożliwia możesz tooadd uwagi tooyour diagram toocapture Twoje opinie

## <a name="analysis-view"></a>Analityczny

Po zakończeniu tworzenia diagramu, przełączyć widoku tooanalysis przechodząc toohello opcji menu u góry i wybieranie hello Lupa dalej toohello paint palety.

![Analityczny](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>Wybór wygenerowanego zagrożeń

Po kliknięciu zagrożenia można wykorzystać trzy unikatowe funkcje:

| Funkcja                               | Info      |
| --------------------------------------- | ------------ |
| **Wskaźnik do odczytu** | <p>Zagrożenie jest teraz oznaczona jako odczytu, które łatwo może pomóc Ci śledzić hello elementy, które już nawiązaniem</p><p>![Odczyt/nieprzeczytana wskaźnika](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **Fokus interakcji** | <p>Zostanie wyróżniona interakcji na diagramie hello należących toothat zagrożeń</p><p>![Fokus interakcji](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **Właściwości zagrożeń** | <p>Dodatkowe informacje na temat zagrożeń hello jest wypełniana w oknie właściwości hello zagrożeń</p><p>![Właściwości zagrożeń](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>Priorytet zmian

Poziom priorytetu hello każde zagrożenie wygenerowanego także zmiana ich toomake kolory go łatwo tooidentify zagrożenia wysoki, średni i niski priorytet.

![Priorytet zmian](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>Pola można edytować właściwości zagrożeń

Jak pokazano w powyższy obraz powitania, użytkownicy mogą zmieniać informacji hello wygenerowany przez narzędzie hello również dodać pola toocertain informacje, takie jak uzasadnienie. Te pola są generowane przez szablon hello, więc jeśli potrzebujesz więcej informacji na każde zagrożenie jest zachęca toomake modyfikacje.

![Właściwości zagrożeń](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>Raporty

Po zakończeniu zmieniania priorytetów i aktualizowania stanu hello każdego wygenerowany zagrożeń, można zapisać plik hello lub wydrukować raport będzie zbyt "raport", a następnie "Utwórz pełny raport." Użytkownik zostanie zapytany tooname hello raportu, a gdy to zrobisz, powinny pojawić się coś podobnego toohello obraz poniżej:

![Raport](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>Następne kroki

toocontribute szablonu dla społeczności hello Przejdź tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  strony. **[Pobierz](https://aka.ms/tmtpreview)**  tooget narzędzie hello obecnie uruchomiona.
