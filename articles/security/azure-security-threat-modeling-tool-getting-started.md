---
title: "aaaGetting uruchomiono — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
description: "Jest to bardziej Przegląd wyróżnianie hello narzędzie modelowania zagrożeń w akcji."
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
ms.openlocfilehash: 75ef139071e8abd0e743aa17b443a6e353f29372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-threat-modeling-tool"></a>Wprowadzenie do narzędzia do modelowania zagrożeń hello

Witaj Cloud i Enterprise zabezpieczeń narzędzia team wydane hello narzędzia do modelowania zagrożeń w wersji zapoznawczej wcześniej w tym roku jako wolną  **[kliknij do pobierania](https://aka.ms/tmtpreview)**. Zmiana Hello mechanizm dostarczania pozwala nam toopush hello najnowszych ulepszeń i poprawek usterek toocustomers każdym otwarciu narzędzia hello, łatwiejsze toomaintain i użyj co.
W tym artykule przeprowadza użytkownika przez proces hello wprowadzenie hello Microsoft SDL threat modelowania podejścia i pokazuje, jak zagrożeń doskonałe narzędzie toodevelop toouse hello modeli szkieletu procesu zabezpieczeń.

W tym artykule opiera się na wiedzy na temat zagrożenia SDL hello modelowania podejście. Szybki przegląd, można znaleźć zbyt**[aplikacji sieci Web modelowania zagrożeń](https://msdn.microsoft.com/library/ms978516.aspx)**  i zarchiwizowaną wersję  **[hello odkrywanie zabezpieczeń mogą przy użyciu podejścia STRIDE](https://docs.google.com/viewer?a=v&pid=sites&srcid=ZGVmYXVsdGRvbWFpbnxzZWN1cmVwcm9ncmFtbWluZ3xneDo0MTY1MmM0ZDI0ZjQ4ZDMy)**  Opublikowany artykuł w witrynie MSDN w 2006 roku.

Podsumuj tooquickly, podejście hello obejmuje tworzenie diagramu, identyfikowania zagrożeń, zmniejszenia ich i sprawdzanie poprawności każdej środki zaradcze. Poniżej przedstawiono diagram, który prezentuje ten proces:

![Proces SDL](./media/azure-security-threat-modeling-tool/sdlapproach.png)

## <a name="starting-hello-threat-modeling-process"></a>Uruchamianie procesu modelowania zagrożeń hello

Po uruchomieniu narzędzia do modelowania zagrożeń hello można zauważyć kilka rzeczy, jak pokazano na rysunku hello:

![Strona początkowa pusta](./media/azure-security-threat-modeling-tool/tmtstart.png)

### <a name="threat-model-section"></a>Sekcja modelu zagrożeń

| Składnik                                   | Szczegóły                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Opinie, sugestie i przycisk problemów** | Przyjmuje możesz hello  **[MSDN Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sdlprocess)**  dla wszystkich elementów SDL. Udostępnia możliwość tooread za pośrednictwem co inne robią użytkownicy, a także rozwiązania i zalecenia. Jeśli nadal nie możesz znaleźć co, czego szukasz, Wyślij wiadomość e-mail tmtextsupport@microsoft.com dla naszych toohelp zespołu pomocy technicznej możesz                                                                                                                            |
| **Tworzenie modelu**                          | Otwiera pustej kanwy dla toodraw możesz diagramu. Upewnij się, że tooselect szablon, który chcesz toouse dla modelu                                                                                                                                                                                                                                                                                                                                                                       |
| **Szablon dla nowych modeli**                 | Należy wybrać toouse szablonu, który przed utworzeniem modelu. Nasze główne szablon jest hello Azure zagrożeń modelu szablonu, który zawiera wzorników specyficzne dla platformy Azure, zagrożenia i metody ich rozwiązywania. Dla ogólnego modeli wybierz hello SDL TM wiedzy z menu rozwijanego hello. Mają toocreate własny szablon lub Prześlij nową dla wszystkich użytkowników? Zapoznaj się z naszym  **[repozytorium szablonu](https://github.com/Microsoft/threat-modeling-templates)**  więcej toolearn stronie GitHub                              |
| **Otwieranie modelu**                            | <p>Zostanie otwarta wcześniej zapisany modeli zagrożeń. Funkcja ostatnio otworzyć modeli Hello stanowi doskonałe rozwiązanie, jeśli potrzebujesz tooopen najnowszych plików. Po umieszczeniu na wybór hello, można znaleźć metody 2 modele tooopen:</p><p><ul><li>Otwórz z tego komputera — klasyczny sposób otwierania pliku przy użyciu lokalnej pamięci masowej</li><li>Otwórz z usługi OneDrive — zespołów może korzystać z folderów w usłudze OneDrive toosave i udostępnianie ich modeli zagrożeń w jednej lokalizacji toohelp zwiększenie produktywności i współpracy</li></ul></p> |
| **Wprowadzenie — przewodnik**                   | Zostanie otwarta hello  **[narzędzia do modelowania zagrożeń Microsoft](./azure-security-threat-modeling-tool.md)**  strony głównej                                                                                                                                                                                                                                                                                                                                                                                            |

### <a name="template-section"></a>Sekcja szablonu

| Składnik               | Szczegóły                                                                                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Utwórz nowy szablon** | Pusty szablon do toobuild użytkownik otwiera na. Jeśli nie masz doskonałej znajomości tworzenia szablonów od początku, zalecamy toobuild z istniejących |
| **Otwórz szablon**       | Otwiera zbyt istniejących szablonów dla Ciebie zmiany toomake                                                                                                             |

Hello narzędzie modelowania zagrożeń zespołu działa stale tooimprove narzędzie funkcjonalność i obsługi. Kilka drobne zmiany może mieć miejsce za pośrednictwem hello ciągu roku hello, ale wszystkie istotne zmiany wymagają modyfikacji oprogramowania w przewodniku hello. Zobacz tooit często tooensure pobrać najnowsze anonsów hello.

## <a name="building-a-model"></a>Tworzenie modelu

W tej sekcji możemy wykonaj następujące czynności:

- Cristina (Deweloper)
- Ricardo (Menedżer programu) i
- Ashish (tester)

Są one pośrednictwa hello procesu tworzenia ich pierwszym modelu zagrożeń.

> Ricardo: Cześć Cristina, pracowano diagramu modelu zagrożeń hello i chce się toomake dotarliśmy szczegóły hello prawo. Proszę o pomoc go przejrzeć?
> Cristina: absolutnie. Spójrzmy.
> Ricardo zostanie otwarte narzędzie hello i udostępnia jego ekranu Cristina.

![Podstawowe zagrożenia modelu](./media/azure-security-threat-modeling-tool/basictmt.png)

> Cristina: Ok wygląda prostego, ale należy zapoznać się z mnie przy jego użyciu?
> Ricardo: się! Oto podział hello:
> - Nasze człowieka użytkownika jest rysowane jako jednostka poza — kwadrat
> - Wysyłasz one serwera sieci Web tooour poleceń — hello okręgu
> - serwer sieci Web Hello jest konsultacji bazy danych (dwie linie)

Co Ricardo tylko wykazało Cristina jest DPD, skrót  **[Diagram przepływu danych](https://en.wikipedia.org/wiki/Data_flow_diagram)**. Narzędzia do modelowania zagrożeń Hello umożliwia granice zaufania toospecify użytkowników, wskazują linie przerywana hello czerwony, tooshow, w którym są różne jednostki w formancie. Na przykład Administratorzy IT wymaga systemu usługi Active Directory na potrzeby uwierzytelniania, dzięki czemu hello usługi Active Directory znajduje się poza ich kontroli.

> Cristina: Wygląda toome prawo. Jakie zagrożenia hello?
> Ricardo: Chcę wyświetlić.

## <a name="analyzing-threats"></a>Analizowanie zagrożeń

Po klika na powitania analitycznego z hello ikonę menu wyboru (plik z Lupa), jest on zajęty tooa listę zagrożeń wygenerowanego hello znaleziono narzędzie modelowania zagrożeń na podstawie szablonu domyślnego hello, używający podejście SDL hello o nazwie  **[ STRIDE (Spoofing naruszeniu ujawnienie informacji, odmowę usługi i podniesienie uprawnień)](https://en.wikipedia.org/wiki/STRIDE_(security))**. pomysł Hello jest, że oprogramowania objęty przewidywalną zbiór zagrożenia, które można znaleźć przy użyciu tych kategorii 6.

Ta metoda działa jak zabezpieczanie domu w celu zapewnienia każdego drzwi i okno ma mechanizm blokowania w miejscu przed dodaniem system alarmu lub sklejek po złodziej hello.

![Podstawowe zagrożenia](./media/azure-security-threat-modeling-tool/basicthreats.png)

Ricardo rozpoczyna się po wybraniu hello pierwszy element na liście hello. Oto, co się stanie:

Po pierwsze została rozszerzona o hello interakcji między dwa wzorników hello

![Interakcji](./media/azure-security-threat-modeling-tool/interaction.png)

Drugi, dodatkowych informacji na temat zagrożeń hello jest wyświetlany w oknie właściwości zagrożeń hello

![Informacje o interakcji](./media/azure-security-threat-modeling-tool/interactioninfo.png)

zagrożenia Hello wygenerowany pomaga go zrozumieć potencjalne wady projektowe. kategoryzacji krok Hello pozwala mu pomysł na potencjalnych ataków, podczas hello dodatkowy opis zawiera informacje mu dokładnie, co ma zły, wraz z potencjalnych toomitigate sposoby go. On za pomocą pola edytowalne toowrite uwag w szczegółach uzasadnienie hello, lub Zmień priorytet oceny w zależności od jego organizacji usterki paska.

Szablony usługi Azure niektórzy użytkownicy toohelp dodatkowe szczegóły zrozumienia nie tylko na czym polega problem, ale także sposób toofix go przez dodanie dokumentacji specyficzne dla tooAzure opisy, przykłady i hiperłącza.

Opis Hello wprowadzone mu zrealizować znaczenie hello dodania użytkowników tooprevent mechanizmu uwierzytelniania z fałszowania, ujawniania hello pierwszy zagrożeń toobe pracowano. Kilka minut do dyskusji hello z Cristina, ich zrozumienie znaczenie hello wdrażanie kontroli dostępu i role. Ricardo wypełnione niektórych toomake szybkich notatek się, że te zostały wprowadzone.

Jak Ricardo przeszła do hello zagrożeń w obszarze ujawnienie informacji, zrealizowane on plan kontroli dostępu hello wymaganych niektóre konta tylko do odczytu do generowania inspekcji i raportów. On zastanawiasz się, czy powinien to być nowych zagrożeń, ale hello, które zostały środki zaradcze hello takie same, więc on odpowiednio hello zagrożeń.
On również traktować o ujawnienie informacji bit więcej i rozumieją, że hello taśm z kopiami zapasowymi były będzie tooneed szyfrowania, zadania dla zespołu operacyjnego hello.

Zagrożenia gwarantuje projektu nie dotyczy toohello środki zaradcze tooexisting lub zabezpieczeń można zmienić za "Nie dotyczy" z hello stan listy rozwijanej. Istnieją trzy inne opcje: nie rozpoczęto — wybór domyślny, konieczne badanie — zużył toofollow zapasów i Mitigated — po pełni jest praca nad.

## <a name="reports--sharing"></a>Udostępnianie & raportów

Po Ricardo przechodzi przez hello listy z Cristina i dodaje ważne uwagi, środki zaradcze/uzasadnienie, priorytet i stan zmieni się, wybiera on Raporty -> Utwórz pełny raport -> Zapisz raport, który drukuje nieuprzywilejowany raportu dla niego toogo za pośrednictwem z współpracownicy tooensure hello właściwe zabezpieczenia pracy jest zaimplementowana.

![Informacje o interakcji](./media/azure-security-threat-modeling-tool/report.png)

Jeśli Ricardo chce zamiast tego pliku hello tooshare, on łatwo to zrobić przez zapisywanie w jego organizacji konta usługi OneDrive. Po on robi to on skopiuj łącze do dokumentu hello i udostępniać jego współpracowników. 

## <a name="threat-modeling-meetings"></a>Spotkań modelowania zagrożeń

Po wysłaniu jego współpracowników toohis modelu zagrożeń przy użyciu usługi OneDrive, Ashish, hello tester Ricardo został underwhelmed. Sprawiał, takich jak Ricardo i Cristina pominiętych kilka ważnych sytuacjach wyjątkowych, które można łatwo złamać. Jego skepticism jest modele toothreat dopełnienia.

W tym scenariuszu po Ashish przejął hello modelu zagrożeń, kontaktował się w dwóch spotkań modelowania zagrożeń: toosynchronize jednego spotkania na powitania procesu i krokach związanych z diagramów hello, a następnie drugiego spotkania przeglądu zagrożeń i podpisywania.

W pierwszym spotkania hello, Ashish poświęcony na 10 minut wszyscy za pośrednictwem procesu modelowania zagrożeń SDL hello przejście. Następnie on skierowana w górę diagramu modelu zagrożeń hello i uruchomić wyjaśniający, szczegółowo. W ciągu pięciu minut gdyby zostały zidentyfikowane ważne brakuje składnika.

Kilka minut później, Ashish i Ricardo uzyskano w rozszerzonej omówienie sposobu powitania serwera sieci Web został skompilowany. Nie było hello idealny tooproceed spotkania, ale uzgodnione wszyscy ostatecznie, że wcześniej odnajdywania rozbieżność hello został będzie toosave przez czas ich w przyszłości hello.

W hello drugiego spotkania, zespołu hello udał za pośrednictwem zagrożenia hello omówione niektóre tooaddress sposobów ich i podpisany zniżki na powitania modelu zagrożeń. Wyewidencjonowany hello dokumentu do kontroli źródła, a nadal rozwoju.

## <a name="thinking-about-assets"></a>Analiza zasobów

Niektóre użytkownikom, którzy mają zagrożeń modelowane mogą pojawić się czy nie zostało to jeszcze wspomnieliśmy o zasobach w ogóle. Firma Microsoft już odnaleziony wielu inżynierów oprogramowania lepsze niż ich zrozumienie pojęcia hello zasobów i zasoby, które osoba atakująca może być zainteresowany zrozumienie ich oprogramowania.

Jeśli chcesz zacząć toothreat modelu DOM, może rozpocząć planowanie o Twoich zdjęć rodziny, niemożliwych lub cenne kompozycji. Prawdopodobnie może uruchomić krokiem jest wybranie hello bieżącego systemu zabezpieczeń i który mogą przestać działać w. Lub może rozpocząć się hello fizycznych funkcje, takie jak pula hello lub hello front porch. Są to podobne toothinking o zasoby, osoby atakujące lub oprogramowanie — projekt. Z tych trzech metod pracę.

Hello podejście toothreat modelowania, które firma Microsoft zostały przedstawione w tym miejscu jest znacznie prostsze niż Microsoft przeprowadził w przeszłości hello. Znaleziono czy podejście do projektowania oprogramowania hello dobrze się sprawdza liczbę zespołów. Mamy nadzieję, że zawierające należy do Ciebie.

## <a name="next-steps"></a>Następne kroki

Wyślij Twoje pytania, komentarze i uwagi tootmtextsupport@microsoft.com. **[Pobierz](https://aka.ms/tmtpreview)**  tooget narzędzie modelowania zagrożeń hello uruchomiona.
