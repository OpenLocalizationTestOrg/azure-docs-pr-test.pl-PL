---
title: aaaDefine strategii Mobile Engagement | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooonboard i zoptymalizować strategię Mobile Engagement z analizy i powiadomieniami wypychanymi."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7533e318-81b9-4360-aace-b7be8225985b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: afe32cb71019092eb28f2a8557404d60ad48ada4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="define-your-mobile-engagement-strategy"></a>Definiowanie strategii Mobile Engagement
*Twoja aplikacja powstała z powodu: toohave korzystają użytkownicy go!*

Mamy nadzieję wymagało doskonałym postępowania działań w trakcie toomake go wspaniałej aplikacji, którą pokochają użytkownicy. Ponadto zwykle zainwestowały duże ilości marketing użytkowników tooacquire budżetu. Jednak po hello początkowej radosnej fazie wielkiego zainteresowania użytkowników można napotkać powoli przestają oni przy użyciu aplikacji. *Jakie usługi Azure Mobile Engagement jest wszystko!* : poruszania się po ich toostick i pozwalają tooincrementally usprawniania aplikacji poprzez testowanie i Dowiedz się więcej.

Nasze podejście tooimproving przechowywania i użycia opiera się na angażowaniu użytkowników aplikacji przy użyciu powiadomień wypychanych i komunikatów w aplikacji, ale w sposób bardzo specjalne, wiadomości i toothem komunikacji dostosowane, każdy zgodnie z tootheir zachowania w aplikacji. Naszym celem jest toolet, które komunikują się z odpowiednimi odbiorcami hello w odpowiednich momentach hello i hello odpowiedniej lokalizacji.

Jednak w tym będziesz mieć toostart z *zrozumienia swoich użytkowników*, następnie utwórz grupy na podstawie ich działanie lub ich właściwości (nazywamy je segmentami), a następnie utworzyć segmentu tooeach odpowiedniej komunikacji.

## <a name="mobile-engagement-serves-your-objectives"></a>Strategia Mobile Engagement służy Twoim celom
*Wspomnieliśmy o przechowywaniu i użyciu, ale właściwie po co?*

Tworzenie strategii Mobile Engagement wymaga przyjrzenia się celom aplikacji i kluczowym wskaźnikom wydajności (KPI).

Rozpocznij od zdefiniowania hello celów i wskaźników KPI, które pomagają toodefine przypadki użycia zaangażowania z odpowiedniej perspektywy hello.

Przypadki użycia to prosta lista kampanii, które chcesz toocommunicate toomake z użytkownikami, od prostego powitania powitania, toohello bardzo zaawansowane użyteczne powiadomienia wyzwalane przez IT system. Dobrze skonstruowany przypadek użycia musi zawierać co najmniej Trójka hello *co, kto, kiedy*:

1. Bardzo krótka nazwa (np. „Kampania powitalna”).
2. **Co**: Przykładowy komunikat (na przykład "Cieszymy się, że toohave Ci przy dołączeniu! Należy pamiętać, toologin tooget Twojego 1 miesiąc za darmo! "). Ten komunikat jest w sposób, nie będziesz w stanie toochange końcowego chcesz za każdym razem, ale zazwyczaj pomaga toostart planowania jakie firma Microsoft ma toosay.
3. **Kto**: hello segment, który otrzyma ten komunikat (na przykład "wszyscy użytkownicy, którzy uruchomili aplikację hello hello najpierw czasu 3 dni temu, odwiedzających stronę logowania hello, ale ma nie zalogowali się").
   * Tak, możesz to zrobić bardzo łatwo przy użyciu usługi Azure Mobile Engagement :)
   * Ponownie, nie będzie to miało toobe końcowego, ponieważ możesz zdefiniować segmenty w dowolnym momencie, ale jest ważne toodefine wcześnie na Twojej tooensure kryteriów segmentacji zbierasz hello odpowiednich danych.
4. **Gdy**: hello czas wdrożenia kampanii. Może być to wybrany dzień lub czas po określonym działaniu (w oparciu o wyzwalacz). Usługa Mobile Engagement oferuje szeroką gamę możliwości toorightly czasu komunikacji.

Po zdefiniowaniu przypadków użycia i segmentów daje danych hello toodefine wytyczne, które muszą być zbierane w aplikacji. To jest rola hello *"planu tagu"*. Plan tagu umożliwia deweloperom toohello określony tooensure użytkownik będący hello zbierania danych. W związku z tym Deweloperzy są możliwe tooembed Mobile Engagement z hello prawo Instalator toowork możesz z kampaniami przy hello odpowiednich danych. Konieczne będzie również bardzo ważne toorun testy tooensure hello Integracja jest prawidłowa i zbiera, co jest potrzebne.

Na podstawie integracji powitania po opublikowanych aplikacji, zgodnie z organizacji będą mogli toosee z analizy w czasie rzeczywistym, segmentowania odbiorców i następnie start inteligentnych toosend docelowej używasz tooengage powiadomień wypychanych z użytkowników końcowych do lub z aplikacji hello.

### <a name="use-cases-tooget-started"></a>Rozpoczęto tooget przypadków użycia
1. Strategia powitalna: Utwórz kilka kampanii powiadomień wypychanych na podstawie zachowania użytkowników końcowych hello podczas uruchamiania hello aplikacji hello w kolejności toore-zaangażować użytkowników w D + 2/5/10/15 po hello pierwszej sesji i zwiększyć pierwszego uruchomienia przechowywania.
2. Promuj nową zawartość (funkcję, artykuł/wideo lub produkt) na podstawie zachowania hello hello użytkownika końcowego toosend hello informacje tylko tooend-użytkowników, którzy są bardziej prawdopodobne tooengage.
3. Oceń aplikacji hello: docelowa mniej niż 1 procent bazy użytkowników, która jest najbardziej prawdopodobną toorate hello aplikację na 5 gwiazdek w sklepie hello.
4. Zwiększ wykorzystanie subskrypcji: wspierania cenną zawartość tooend użytkowników, którzy nie widzieli jeszcze tooincrease subskrypcji.
5. Samouczek: koniec obowiązkowych samouczków dla wszystkich. Zamiast tego możesz stworzyć wspaniałe samouczki wewnątrz aplikacji i wyzwalać je poprzez komunikaty w aplikacji tylko wtedy, gdy użytkownik hello wydaje toonot użycia aplikacji hello lub ma trudności przy użyciu funkcji?

## <a name="why-do-you-need-analytics-tooengage"></a>Dlaczego należy analytics tooengage?
Na tym etapie można już wywnioskować, że utworzenie jednego powiadomienia wypychanego do wszystkich użytkowników nie wystarczy. Hello kluczową ideą usługi Mobile Engagement jest toohelp marketingowcom i deweloperom współpracować z hello odpowiednich użytkowników końcowych w odpowiednich momentach hello i w prawo hello Umieść. tooknow te trzy główne pojęcia istotne toogather analytics z aplikacji, a następnie użyć go toosegment odbiorców. Takie rozwiązanie jest jeszcze bardziej skuteczne, jeśli segmenty oparte na zachowaniach uzupełniają dane pochodzące z innej bazy danych, systemu CRM lub rozwiązań opartych na wielu kanałach. Usługa Mobile Engagement umożliwia zbieranie danych z dowolnego miejsca i używa go tootarget hello odpowiednich odbiorców.

toobe hello najbardziej kontekstowe możliwe podczas angażowania swoich odbiorców, jest niezwykle istotne toohave hello wiedzy hello zachowania użytkowników końcowych, tooknow ich stan w czasie rzeczywistym. Gromadzenie danych umożliwia toofocus marketingu naprawdę na to, co ma znaczenie przypadki użycia tooplay i osiągnięcia ich celów strategię usługi mobile engagement. Osiąganie celów hello określonych wcześniej jest także Przyczyna hello Dlaczego hello najlepszym rozwiązaniem w rzeczywistości nie jest toogather cokolwiek, wszystko do hello analizy, a jedynie tych, które pozwalają toofocus na które mają toolearn i przypadki użycia. Jest toostart dobrze hello, spróbuj, przetestować i dowiedzieć się, jak toouse hello rozwiązania i adres inteligentnych powiadomień wypychanych i zwiększyć przechowywanie toobring aplikacji hello go na osiągnięcie sukcesu.

> [!NOTE]
> Pamiętaj: Za dużo danych to złe rozwiązanie hello danych!
> 
> 

### <a name="use-cases-and-best-practices"></a>Przypadki użycia i najlepsze praktyki
W hello następnych sekcjach omówiono pokrótce niektóre kluczowe przypadki użycia, które firma Microsoft został pochodzą od tooget naszych klientów, należy uruchomić.

#### <a name="media"></a>Multimedia
Zbieranie hello typu zawartości, który jest używany przez użytkownika końcowego hello, a następnie segmentuj odbiorców hello na podstawie tego zachowania tootarget określonych typów zawartości tylko odbiorców tooan, który ma być tooconsume częściej. Takie rozwiązanie pomaga uniknąć spamowania całej bazy użytkowników i zapewnia lepsze przechowywanie.

#### <a name="m-commerce"></a>M-commerce
Zbierać hello kategorie produktów najczęściej odwiedzanych w toopromote odbiorców aplikacji i nakieruj hello rabat lub nowe produkty w danej kategorii, co hello użytkownika końcowego będzie toopurchase częściej. Celem tooboost przychodów. Ponownie hello cel nie jest toospam!

#### <a name="gaming"></a>Gry
Zbieraj hello o poziomie gry dla użytkownika końcowego i hello czas działania odbiorców hello danego okresu tootarget, którzy utknęli i będą bardziej prawdopodobne tooa toojump obok poziomu przy użyciu oferty bonusowej.

Komunikować się informacje o konkretnych zdarzeniach z motywacji toothose użytkowników, którzy nie grali niektórych tooencourage tootry czas ich tooreturn.

#### <a name="retail"></a>Sprzedaż detaliczna
Zbieraj hello produktach i markach, które grupy odbiorców powinien być bardziej prawdopodobne tooconsume na podstawie Ulubione lub zachowania i dysku hello odbiorców tooyour magazynu tooincrease swoje przychody z zakupów.

#### <a name="banking"></a>Bankowość
Zbieranie danych od użytkowników końcowych, którzy utworzyli konto podczas pierwszego uruchomienia hello aplikacji hello. Toodeploy strategię powitalną z nakierowanymi powiadomieniami wypychanymi na celu i zwiększyć hello liczbę subskrypcji kont.

### <a name="how-toocreate-a-great-tag-plan"></a>Jak plan toocreate dużą tag?
Plan tagu musi być swoistym opisem ścieżki użytkownika hello lub rodzajem przepływu pracy aplikacji hello, podając wszystkie hello niezbędne tagi (dane), które muszą być zbierane toohave za mało zachowania użytkowników toounderstand analytics i poprawnie bazy użytkowników hello segmentu. Nie jest to proces techniczny. W związku z tym marketingowcy są toospecify stanie hello dane toocollect w oparciu o strategię Mobile Engagement.

Hello minimalna tootag jest co najmniej wszystkich ekranów powitalnych (nazywane *działania* w usłudze Mobile Engagement) aplikacji. Dzięki temu można ustalić ścieżkę użytkownika hello.

Działanie może zawierać osadzone *zdarzenia*, które zbierają informacje o działaniu, np. kliknięcie przycisku. Dzięki temu hello zbieranie danych o interakcji w aplikacji hello. W związku z tym marketingowcy mogą tooknow co użytkownicy ekranu są wizytę i co robią.

`Jobs`to działania o czasie trwania. Jest to bardzo przydatna dla marketingowca toounderstand, jak długo trwa dla toocreate użytkownika konta lub toologin dla wystąpienia. Ponadto może to być przydatne w przypadku toomonitor deweloperów, jak długo trwa toocall usługi sieci web.

`Errors`można też monitorowanych tooknow Jeśli użytkownicy mają problemy w aplikacji. Na przykład częste problemy z nawiązywaniem połączenia.

Wszystkie dane tego typu można rozszerzyć za pomocą parametrów (*informacji dodatkowych* w usłudze Mobile Engagement) pozwala toogather dynamicznych danych z aplikacji hello. Jest to ważne tooallow precyzyjnej segmentacji. Przykładowo marketingowcy mogą segmentować oparty na typie hello zawartości zajmowany przez użytkownika. Witaj typu zawartości będzie hello dynamiczne informacje działania lub zdarzenia.

*Informacje o aplikacji* się dane, które umożliwia tooconfirm hello stan aplikacji hello lub hello użytkownika w czasie rzeczywistym. To również pomaga toocategorize bazy odbiorców i szybkim nakierowywaniu działań. Na przykład go użyć stanu PRAWDA/FAŁSZ, czy rejestrowanie użytkowników hello lub nie lub daty wygaśnięcia subskrypcji.

#### <a name="example-of-tags"></a>Przykład tagów
*Przypadek użycia: Segment odbiorców zachowanie tootarget hello odpowiednich użytkowników końcowych z zawartości powiadomienia wypychanego hello*

1. Wyślij toopromote powiadomień wypychanych kategorię lub produkt: zebrać zachowanie danych toosegment odbiorców w oparciu hello kategorii produktów odwiedzili x razy w danym okresie czasu lub konkretny element dodali do koszyka. zebrane dane Hello będzie pozwalają toosegment, a następnie wyślij wypychania powiadomień toohello odpowiednich odbiorców.
2. Szybkość aplikacji hello: zbieranie danych oparte na powitania zawartość udostępnioną przez odbiorców hello w sieciach społecznościowych. Ma toosegment hello odbiorców poprzez określenie hello *Ambasadorów* aplikacji. Za pomocą wypychania powiadomień w aplikacji, hello ambasadorzy będą najlepszymi odbiorcami toorate tooask Twojej aplikacji, aplikację na 5 gwiazdek w sklepie hello hello.
   
   ![][1]

*Przypadek użycia: dane deklaratywne*

1. Segment wiadomości w formie alertu: Zbieraj dane deklaratywne toosegment odbiorców na podstawie swoich preferencji. Dzięki temu możesz wysyłać powiadomienia wypychane na dany temat do odbiorców, którzy będą naprawdę zainteresowani.
2. Segmentuj odbiorców w oparciu o stan logowania. Zbieranie danych tooknow, jeśli użytkownik jest połączony lub utworzył konto. Umożliwia użytkownikom końcowym docelowych, które nie zostały jeszcze zalogowany i wysyła wypychania powiadomień tooencourage użytkownika końcowego tooconvert.
   ![][2]

### <a name="next-steps"></a>Następne kroki
* Odwiedź stronę [Mobile Engagement pojęcia] toolearn więcej o podstawowych pojęciach Mobile Engagement.
* Odwiedź stronę [tworzenie aplikacji Mobile Engagement](mobile-engagement-create.md) toocreate nową kolekcję aplikacji usługi Engagement Mobile w usłudze Azure i rozpocząć zarządzanie aplikacjami za pomocą portalu Mobile Engagement hello.
* Odwiedź stronę [najlepsze rozwiązania](mobile-engagement-getting-started-best-practices.md) toogo uzyskać szczegółowe informacje.
* Odwiedź stronę [scenariusz aplikacji do grania](mobile-engagement-gaming-scenario.md) toolearn o implementacji usługi Mobile Engagement z prostej aplikacji do grania. 
* Odwiedź stronę [scenariusza aplikacji nośnika](mobile-engagement-media-scenario.md) toolearn o implementacji usługi Mobile Engagement z przykładową aplikację nośnika. 
* Odwiedź stronę [samouczki] toolearn więcej informacji na temat hello implementacji.

<!-- Images. -->
[1]: ./media/mobile-engagement-define-your-mobile-engagement-strategy/use-case1.png
[2]: ./media/mobile-engagement-define-your-mobile-engagement-strategy/use-case2.png

<!-- URLs. -->
[Mobile Engagement pojęcia]: http://azure.microsoft.com/documentation/articles/mobile-engagement-concepts/
[samouczki]: http://azure.microsoft.com/documentation/articles/mobile-engagement-ios-get-started/

