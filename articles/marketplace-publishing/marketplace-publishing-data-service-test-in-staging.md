---
title: "aaaTesting oferty usługi danych dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootest usługi danych oferty dla hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a>Testowanie tej oferty usługi danych tymczasowych
> [!IMPORTANT]
> **W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.** Jeśli masz aplikacji biznesowej SaaS chcesz toopublish na AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners). Jeśli masz aplikacje IaaS lub dewelopera usługi będzie jak toopublish w witrynie Azure Marketplace więcej informacji można znaleźć [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Po zakończeniu hello dwa pierwsze kroki z [utworzenie konta Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) i [Tworzenie oferty usługi danych w portalu publikowania](marketplace-publishing-data-service-creation.md) możesz przystąpić do udostępnianie w hello ofertę Azure Marketplace. W tym temacie zostanie najpierw przeprowadzi użytkownika przez proces hello, pośrednie, krok o nazwie "tymczasowości"

Oznacza, że wdrażanie ofertę w prywatnej "piaskownicy", gdzie należy przetestować i sprawdzić jego działanie przed wypchnięciem go tooproduction przemieszczania. Oferta Hello będą wyświetlane w tymczasowej analogiczny, jak tooa klienta, który został wdrożony go.

## <a name="step-1-pushing-your-offer-toostaging"></a>Krok 1. Wypychanie toostaging Twojej oferty
Wypychanie toostaging Twojego oferta pozwala oferta hello tootest przed staje się dostępna toofuture subskrybentów.  Widać, jak pojawiają się i funkcji dla tych danych tooyour subskrypcji przez Twoją ofertę.  

  ![Rysowanie](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. Zaloguj się do hello [Portal publikowania](https://publish.windowsazure.com)
2. Wybierz **usług danych** hello nawigacji po lewej stronie okna
3. Wybierz ofertę ma toopush toostaging. Zostanie wyświetlone powitalne powyżej ekranu.
4. Kliknij przycisk **Push tooStaging** przycisku.  
5. Jeśli występują problemy z hello oferty, które potrzebne toobe ukończone toostaging wcześniejsze toopushing, zostanie wyświetlona lista wyświetlana.  Popraw te elementy, klikając każdego elementu listy hello. Po wszystkich poprawek wprowadzonych, kliknij przycisk **Push tooStaging** przycisk ponownie.

Jeśli nie występują problemy z Twoją ofertę zobaczysz oknie podręcznym hello poniżej.  

Jeśli nie masz planowania nie zatwierdzone toosurface Twojej oferty w portalu Azure (aktualnie ma ograniczoną pojemność), a następnie hello właśnie Zamknij okno podręczne.

tootest danych usługi w portalu Azure (w portalu DataMarket toohello dodanie), konieczne będzie tootest identyfikator subskrypcji platformy Azure z.  Ten identyfikator subskrypcji określi hello konta, które będą dozwolone tootest ofertę.  

Wyciąć i wkleić identyfikator subskrypcji, a następnie kliknij przycisk hello toocontinue znacznik wyboru.

  ![Rysowanie](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> Te identyfikatory subskrypcji platformy Azure są tylko wymaganych do testowania i przejściowych w hello [portalu zarządzania Azure](https://manage.windowsazure.com). Nie są one wymagane tootest w portalu Azure Marketplace.
> 
> 

Hello dalej ekran pokazuje czy publikowanie odbywa się za pomocą wyświetlania hello "w toku" ikona wyróżnione żółty poniżej. Wypychanie toostaging zajmuje od 10 minut too15.  Jeśli trwa dłużej, najpierw należy odświeżyć przeglądarkę (klawisz F5 w programie Internet Explorer).  W rzadkich przypadkach hello gdzie ofertę nadal jest wypychanie toostaging po upływie godziny kliknij przycisk hello skontaktuj się z nami link toolet nam znać, że występuje problem.

  ![Rysowanie](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

Zakończeniu tooStaging wypychania hello hello "w toku" ikony zostanie zatrzymane, przenoszenie, a hello stan zostanie zaktualizowany za "przemieszczane".  Użytkownik jest teraz gotowy tootest ofertę.  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a>Krok 2. Testowanie przemieszczanego ofertę w DataMarket
Kliknij łącze powitania po tekst hello **"Zobacz usługi oferują na..."** ekran hello toodisplay hello subskrybenta zobaczą, gdy ofertę przechodzi tooproduction i pojawi się w sekcji DataMarket witryny.

  ![Rysowanie](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

Test lub sprawdź każdy z elementów 12 hello oznaczone powyżej tooensure wszystkich logo, ceny/transakcji, tekst, obrazy, dokumentacji i łącza są poprawne i działają prawidłowo.  Jest to tooensure odpowiedni moment, w których wszystkie wartości testowe wprowadzona podczas tworzenia Twojej oferty zostały zastąpione rzeczywistymi wartościami.

1. Oferta logo
2. Nazwa oferty
3. Witryna sieci Web firmy wydawcy łącze/nazwy tooyour
4. Kategorie wyszukiwania dla danej oferty
5. Subskrybenci tooassist łącza pomocy technicznej Twojej oferty
6. Kontekstowe opis dla danej oferty
7. Plan oferta przedstawiające szczegółów rozliczeń
8. Kod tooimplementation powiązania
9. Przykładowe obrazy, które ilustrują korzystanie z danych oferty
10. Metadane wejścia/wyjścia dla każdej usługi w ramach hello oferty
11. Oferty warunki użytkowania
12. Podgląd danych hello oferty

Na koniec sprawdzenie, czy usługa hello będzie działać przez hello Datamarket, klikając łącze hello "EKSPLORUJ ten zestaw danych".  Zostanie otwarty w nowym oknie narzędzia hello nazywamy "Eksploratora usługi", można wyświetlić podgląd wyników zapytania hello wysyłane do usługi.  W tym oknie można wprowadzić hello parametry potrzebne i wyświetlić wyniki hello wyświetlony w wyniku zapytania względem usługi.   Wyświetlana jest również hello adres URL dla zapytania.  

> [!NOTE]
> Należy się tooreview hello opis tekstowy wyświetlany u góry hello usługi hello.  A jeśli ofertę składa się z więcej niż jedna usługa wywołania, kliknij karty hello na powitania dolnej tooswitch toohello dalej usługi tooreview i przetestowania.
> 
> 

## <a name="next-step"></a>Następny krok
Jeśli występują problemy dotyczące i potrzebujesz pomocy ich rozwiązywanie skontaktuj się z pomocą [techniczną wydawcy Azure](http://go.microsoft.com/fwlink/?LinkId=272975).

Jeśli są prawidłowe i gotowe toopublish ofertę przeczytaj hello [tooProduction tooPush zatwierdzenie żądania](marketplace-publishing-push-to-production.md) dokumentacji.

## <a name="see-also"></a>Zobacz też
* [Wprowadzenie: Jak toopublish toohello oferta portalu Azure Marketplace](marketplace-publishing-getting-started.md)

