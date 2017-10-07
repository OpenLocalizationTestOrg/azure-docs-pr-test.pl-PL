---
title: aaaDeploy toohello Twojej oferty Azure Marketplace | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o i przeprowadzenie toodeploy instrukcje hello oferta — obraz maszyny wirtualnej, dewelopera usługi, Usługa danych itp.--toohello portalu Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 8f79b891-84e2-4f41-ba0d-66420e2c6b2e
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2016
ms.author: hascipio
ms.openlocfilehash: ab0bb7c78020187505c2d5f09c4de246987ecd97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-offer-toohello-azure-marketplace"></a>Wdrażanie toohello Twojej oferty Azure Marketplace
Po zakończeniu Twojej oferty (to znaczy zostały przetestowane scenariuszy, marketingu zawartości, itp.) i są gotowe toolaunch żądania **Push tooproduction** na powitania **publikowania** kartę.  

1. Witaj cztery kroki w obszarze strony wskazówki hello hello publikowania portalu powinien być została zakończona i zielony. W przypadku ofert maszyny wirtualnej upewnij się, że hello następujące wytyczne zostaną wykonane.
   
    ![Rysowanie][img-pubportal-walkthru-checked]
2. Wybierz hello **publikowania** kartę liście hello na powitania po lewej stronie.
   
    ![Rysowanie][img-pubportal-menu-publish]
3. Kliknij przycisk hello **żądania zatwierdzenia toopush tooproduction**. Po wysłaniu żądania hello, zespół zatwierdzenia hello wykonuje końcowej oceny, a następnie ofertę będą dostępne w portalu Azure Marketplace hello.
   
    ![Rysowanie][img-pubportal-publish-pushproduction]

> [!IMPORTANT]
> W przypadku maszyn wirtualnych po kliknięciu hello przycisk żądania zatwierdzenia toopush tooproduction hello następujące kroki są wykonywane za hello sceny. Będziesz w stanie tooview postęp hello każdego kroku karcie publikowania hello w hello publikowania portalu. Należy sprawdzić tę stronę w regularnych odstępach czasu (do czasu hello stanu wyświetlany jest "Lista") Aby uzyskać informacje o błędzie, który konieczne korekty użytkownika końcowego.
> 
> * Na początku żądanie produkcyjnej przechodzi toohello zespołu certyfikacji, który zweryfikować hello wirtualnego dysku twardego. Jednak aktualizujesz już wymienionych ofertę żądania hello otrzymano tylko marketingu zmiany, następnie hello certyfikacji krok zostanie pominięty.
> * W następnym krokiem hello hello żądania wejścia toohello zespołu weryfikacji zawartości, który Sprawdź hello marketingu zawartości hello oferty.
> * Jeśli hello powyżej kroki zostały wykonane pomyślnie, oferty hello jest zatwierdzona w środowisku produkcyjnym. W tej chwili stan hello stają się "na liście" hello portal publikowania. Jednak ten stan "Lista" oznacza o ukończeniu procesu hello. następujące kroki należy toobe ukończone przed oferta hello Hello jest dostępna w hello Azure Marketplace.
> * Oferta hello zatwierdzone w środowisku produkcyjnym w poprzednim kroku hello replikacji rozpoczęcia oferty hello we wszystkich hello centrach danych platformy Azure. Zazwyczaj zajmuje 24-48hours dla toocomplete replikacji hello ale może potrwać tooa tygodnia, w zależności od rozmiaru hello hello wirtualnego dysku twardego. Jednak Jeśli aktualizujesz już wymienionych ofertę i otrzymano tylko marketingu zmiany, następnie replikacji hello jest szybsze.
> * Po ukończeniu replikacji hello jest to oferta hello będą dostępne w hello Azure Marketplace.
> 
> Zawsze można usunąć oferta hello w **projekt** stanu (tj., nigdy nie **Push toostaging** lub **Push tooproduction**). Na powitania **historii** , kliknij pozycję hello **Odrzuć wersję roboczą** przycisk u dołu hello hello strony toodelete wersję roboczą.
> 
> 

## <a name="production-checklist-for-all-virtual-machine-offers"></a>Lista kontrolna produkcyjnych w przypadku wszystkich ofert maszyny wirtualnej
* Upewnij się, że jesteś partnerem certyfikowane systemu Microsoft Azure
* Karcie jednostki SKU hello hello opcję "Ukryj tej jednostki SKU z witryny Marketplace hello ponieważ zawsze powinna zostać zakupione za pośrednictwem szablon rozwiązania" powinno być oznaczone jako tak tylko jeśli hello jednostka SKU jest częścią szablonu rozwiązania. We wszystkich hello innych przypadkach, ta opcja zawsze powinien być oznaczony jako nie.
* Pamiętaj: Nie należy zmieniać ustawienie widoczności SKU hello gdy hello jednostka SKU jest wyświetlany. Ta funkcja nie jest obsługiwana.
* Upewnij się, że logo hello odpowiednia toohello: Azure Marketplace wytycznych dotyczących logo podane poniżej.
* Opis oferta, jednostka SKU nie powinny być takie same.
* W jednostce SKU tytuł i oferują długie podsumowanie nie powinna być taka sama.
* Tytuł jednostki SKU i Podsumowanie oferty nie powinna być taka sama.
* Jednostka SKU tytuły nie powinny być identyczne dla oferty z wielu jednostki SKU.

**Wytycznych dotyczących logo Azure Marketplace**

* Hello Azure projekt ma paletę kolorów proste. Zachowaj hello liczba podstawowy i pomocniczy kolory na logo niski.
* motyw kolorów Hello hello portalu Azure są białe i czarne. Dlatego należy unikać kolorów te jako kolor tła hello swoje logo. Użyj niektórych koloru, która swoje logo widocznym w hello portalu Azure. Zaleca się proste kolorów podstawowych. Jeśli używasz przezroczyste tło, upewnij się, że logo hello/tekst nie jest białe lub czarny.
* Nie używaj gradientu tła na powitania logo.
* Należy unikać wprowadzania tekstu, nawet Twoja firma lub marką, na powitania logo.
* Hello wygląd i działanie logo powinno być "prosty" i unikać gradienty.
* nie powinny być skalowane Hello logo.

**Dodatkowe wskazówki dotyczące hello bohater logo:**

* logo bohater Hello jest opcjonalna. Wydawca Hello można nie tooupload logo bohater. **Jednak raz przekazane ikona bohater hello nie można usunąć z hello publikowania portalu. W tym czasie partnera hello wykonaj hello Azure Marketplace wytyczne dla ikony bohater else oferta hello nie będą tooproduction zatwierdzone.**
* Witaj wyświetlaną nazwę wydawcy, nazwa jednostki SKU i hello oferują długie podsumowanie są wyświetlane w kolorze białym znakiem. Dlatego należy unikać zachowuje żadnych jasny kolor hello tło hello bohater ikony. Czarne, białe i przezroczystego tła ikon bohater jest niedozwolone.
* Hello wydawcy, nazwa wyświetlana, jednostki SKU tytuł oferty hello długie Podsumowanie i hello utworzyć przycisk są programowo osadzone wewnątrz logo bohater powitania po oferta hello przejdzie do listy. Nie należy więc wprowadzić dowolny tekst, podczas projektowania hello bohater logo. Pozostawienia puste miejsce po prawej stronie powitania, ponieważ tekst hello (tj. wydawcy, nazwa wyświetlana, nazwa jednostki SKU, długie Podsumowanie oferty hello) zostanie uwzględniona programowo przez nas nad nim. puste miejsce Hello hello tekstu powinno być 415 x 100 na powitania prawym (i przesunięty 370px od lewej hello).

## <a name="additional-production-checklist-for-already-listed-virtual-machine-offers"></a>Oferuje dodatkowe produkcji Lista kontrolna już wymienionych maszyny wirtualnej
* Sprawdź, jeśli istnieje już ofertę z hello oferują takie same nazwy w firmie. Jeśli tak, należy dodać nową wersję hello jednostki SKU w istniejących oferta hello zamiast tworzenia nowej oferty zduplikowane.
* Dysk danych nie należy zmieniać między dwoma wersjami hello same jednostki SKU.
* Hello Azure Marketplace nie obsługuje zmiany hello cennika wymienionych jednostki SKU ma wpływ na rozliczenia hello hello istniejących odbiorców. Upewnij się, że nie zmienisz hello cen jednostki SKU hello wymienionych w hello regionach, gdzie dostępna jest opcja hello jednostki SKU. Możesz jednak dodawać nowe jednostki SKU lub Dodaj nowe tooan regionów istniejący jednostce SKU.

## <a name="next-steps"></a>Następne kroki
Gdy oferta hello odbywa się na żywo, testowanie hello klienta scenariusze toovalidate, że wszystkie kontrakty hello i funkcje działają poprawnie w środowisku produkcyjnym hello jako hello przetestowane i zatwierdzone w środowisku przemieszczania.

## <a name="see-also"></a>Zobacz też
* [Wprowadzenie: jak toopublish toohello oferta portalu Azure Marketplace](marketplace-publishing-getting-started.md)

[img-pubportal-walkthru-checked]:media/marketplace-publishing-push-to-production/pubportal-walkthru-checked.png
[img-pubportal-menu-publish]:media/marketplace-publishing-push-to-production/pubportal-menu-publish.png
[img-pubportal-publish-pushproduction]:media/marketplace-publishing-push-to-production/pubportal-publish-pushproduction.png
