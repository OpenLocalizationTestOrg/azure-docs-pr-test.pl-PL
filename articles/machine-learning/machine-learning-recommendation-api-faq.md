---
title: "aaaSet się i użyj hello Machine Learning API zalecenia | Dokumentacja firmy Microsoft"
description: "Interfejs API zalecenia Microsoft skompilowanej za pomocą usługi Azure Machine Learning — często zadawane pytania"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>Konfigurowanie i używanie interfejsu API zaleceń usługi Machine Learning — często zadawane pytania
**Co to jest zalecenia?**

> [!NOTE]
> Należy rozpocząć za pomocą hello usługi kognitywnych zalecenia dotyczące interfejsu API, zamiast tej wersji. Hello kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną wszystkie hello nowe funkcje. Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.
> Dowiedz się więcej o [toohello Migrowanie nową usługę kognitywnych](http://aka.ms/recomigrate)
> 
> 

W przypadku organizacji i firm, które opierają się na sprzedaży toocross zalecenia i sprzedaje up produktów i usług tootheir klientów zalecenia w usłudze Azure Machine Learning zapewnia aparat samoobsługi zalecenia. Jest implementację współpracy filtrowania, która używa factorization macierzy jako jego algorytmu core. Deweloperzy aplikacji można uzyskać dostępu do zalecenia za pomocą interfejsów API REST. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Co można zrobić z ZALECENIAMI?**

Zalecenia dotyczące przyjmuje jako wejście element lub zbiór elementów i zwraca listę odpowiednich zaleceń. Na przykład: klient sklepie internetowym kliknie produktu. Hello online detalicznej tego produktu są wysyłane jako tooRECOMMENDATIONS wejściowych, pobiera listę produktów w zamian i decyduje o tym, które te produkty zostaną wyświetlone toohello klienta. Może mają toooptimize zalecenia toouse sklepu online lub nawet tooinform Twojego wewnątrz sprzedaży, działu lub wywołanie Centrum.

**Czy istnieją jakiekolwiek ograniczenia użycia?**

Zalecenia dotyczące ma hello następujące ograniczenia:

* Maksymalna liczba modeli dla subskrypcji: 10
* Maksymalna liczba elementów, które mogą zawierać wykaz: 100 000
* Maksymalna liczba punktów użycia, które są zachowane w Hello jest ~ 5,000,000. Hello najstarsze zostanie usunięte, gdy nowe zostanie przekazany lub zgłaszane.
* Maksymalny rozmiar danych, który można wysłać w wiadomości e-mail (na przykład importu wykazu danych, importowanie danych użycia) to 200 MB
* Liczba transakcji na sekundę (TPS) dla kompilacji modelu zalecenia, która nie jest aktywny jest TPS ~ 2. Zalecenia dotyczące kompilacji modelu, która jest aktywna mogą przechowywać się too20 TPS.

## <a name="purchase-and-billing"></a>Zakup i rozliczenia
**Ile kosztuje zalecenia w okresie uruchamiania hello?**

Zalecenia dotyczące jest usługą opartą na subskrypcję. Ładowanie opiera się na woluminie transakcji w miesiącu. Możesz sprawdzić hello [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations) w Microsoft Azure Marketplace w celu uzyskania informacji o cenach.

**Czy istnieją kosztów związanych z o zalecenia dotyczące śledzenia i przechowywania aktywności użytkownika?**

Nie w momencie hello.

**Zalecenia dotyczące ma bezpłatną wersję próbną?**

Brak wolnego dziennik, który jest ograniczony too10, 000 transakcji w miesiącu.

**Gdy zostanie I opłaty będą naliczane za zalecenia?**

Subskrypcja płatna jest żadnej subskrypcji, dla którego jest miesięcznej opłaty za. Jeśli kupisz subskrypcję płatną, możesz są natychmiast naliczane opłaty za hello najpierw użyj miesiącu. Naliczane są opłaty hello ilość, którą jest skojarzone z ofertą hello na stronę subskrypcji hello (oraz podatków). Opłata miesięczna utworzona na powitania sam kalendarza daty w postaci pierwotnego zakupu do momentu anulowania subskrypcji hello każdego miesiąca. 

**Jak uaktualnić tooa wyższej warstwy usługi?**

Możesz kupić lub zaktualizować subskrypcji hello [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations) strony w witrynie Microsoft Azure Marketplace.

Po uaktualnieniu subskrypcji:

* Transakcje, które pozostały w ramach starego subskrypcji nie są dodawane tooyour nową subskrypcję. 
* Płacisz pełną cenę hello nowej subskrypcji, nawet jeśli masz nieużywane transakcji na starym subskrypcji.

Proces tooupgrade subskrypcji:

* Nevigate toohello [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations).
* Zaloguj się w toohello Marketplace, jeśli nie jest już zalogowany.
* W okienku po prawej stronie powitania są wyświetlane wszystkie dostępne plany hello. Kliknij przycisk radiowy hello hello planu, który ma tooupgrade do.
* Jeśli chcesz tooupgrade, kliknij przycisk **OK**. Jeśli nie chcesz, aby tooupgrade, kliknij przycisk **anulować**.

**Ważne** okno dialogowe hello dokładnie Przeczytaj przed rozpoczęciem uaktualniania, ponieważ istnieją rozliczeń i użycia.

**Gdy zakończy się tooRecommendations mojej subskrypcji?**

Subskrypcja zakończy się po anulowaniu jej. Jeśli chcesz toocancel subskrypcji, zobacz hello, postępując zgodnie z instrukcjami.

**Jak anulować subskrypcję zalecenia?**

toocancel, które subskrypcji, użyj hello następujące kroki. Jeśli Twojej bieżącej subskrypcji płatnej subskrypcji, subskrypcji nadal obowiązują do końca hello hello bieżącego okresu rozliczeniowego. Jeśli należy natychmiast hello toobe anulowania skuteczne, skontaktuj się z nami pod adresem [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Uwaga** zwrot nie podano anulowanie przed zakończeniem hello okresie rozliczeniowym lub nieużywane transakcji w okresie rozliczeniowym.

* Przejdź toohello [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations).
* Zaloguj się w toohello Marketplace, jeśli nie jest już zalogowany.
* Kliknij przycisk **anulować** toohello rogu hello nazwę zestawu danych i stanu. Ta subskrypcja jest używana, aż do osiągnięcia końca hello hello bieżącego rozliczeń okres lub Twój limit transakcji (cokolwiek nastąpi najpierw).

Jeśli chcesz toocancel subskrypcji natychmiast, więc możesz kupić nową subskrypcję, założyć zgłoszenie w [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Wprowadzenie do zalecenia
**Zalecenia dotyczące jest dla mnie?** 

Zalecenia w uczeniu maszynowym jest przeznaczony dla organizacji i firm, które zależą od zaleceń toocross sprzedaży i sprzedaje up produktów lub usług tootheir klientów. Jeśli masz witryny sieci Web skierowane do klientów, pracownicy działu sprzedaży, wewnętrznej pracownicy działu sprzedaży lub biurem, oraz Jeśli oferujesz katalogu więcej niż kilka dozen produktów lub usług wyników firmy mogą korzystać z zalecenia. 

Eksperymentowanie z zaleceniami jest zaprojektowana toobe dość proste. Bieżąca wersja interfejsu API na podstawie Hello wymaga podstawowe umiejętności programowania. Jeśli potrzebujesz pomocy, skontaktuj się z dostawcą hello, która opracowała witryny sieci Web. Jeśli masz wewnętrzny dział IT lub lokalnego projektanta, powinny być możliwe tooget toowork zalecenia dla Ciebie. 

**Jakie są wymagania wstępne hello konfigurowania zalecenia?**

Zalecenia dotyczące wymaga dziennika opcji użytkownika pod kątem tooyour katalogu. Jeśli nie masz takiego dziennika i masz klienta witryna sieci Web, zalecenia mogą zbierać aktywność użytkowników dla Ciebie. 

Zalecenia dotyczące wymaga także katalog produktów i usług. Jeśli nie masz katalogu hello zalecenia można użyć danych użycia klienta rzeczywiste hello i przetwarzania wykazu. Dorozumiany katalogu nie będzie zawierać elementy, które nie zostały zgłoszone w ramach transakcji użytkownika.

**Jak skonfigurować zalecenia dla powitania po raz pierwszy?**

Po [subskrybującą](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, powinien użyć dokumentacji interfejsu API hello hello [Azure Machine Learning zalecenia — Przewodnik Szybki Start](machine-learning-recommendation-api-quick-start-guide.md) tooset hello usługi.

**Gdzie można znaleźć dokumentację interfejsu API?** 

Dokumentacja interfejsu API Hello jest [Azure Machine Learning zalecenia — Przewodnik Szybki Start](machine-learning-recommendation-api-quick-start-guide.md).

**Opcje czy mam tooRecommendations tooupload katalogu i użycia danych?**

Dostępne są dwie opcje do przekazywania danych katalogu i użycia: można wyeksportować hello dane systemu CRM lub inne dzienniki i przekaż go tooRecommendations lub można dodać tagów tooyour witryny sieci Web, który będzie śledzić działania użytkowników. Jeśli używasz hello druga metoda hello dane będą przechowywane na platformie Azure.

## <a name="maintenance-and-support"></a>Obsługi i pomocy technicznej
**Jak duży może być zestawu danych?**

Każdy zestaw danych może zawierać too100, 000 elementów katalogu i too2048 MB danych użycia.
Ponadto subskrypcja może zawierać zapasowej too10 zestawów danych (modeli).

**Gdzie można uzyskać pomoc techniczną dotyczącą zalecenia?**

Pomoc techniczna jest dostępna na powitania [Microsoft Azure obsługuje](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) lokacji.

**Gdzie można znaleźć hello warunki użytkowania?**

[Microsoft Azure Machine Learning zalecenia dotyczące interfejsu API warunków użytkowania usługi](https://datamarket.azure.com/dataset/amla/recommendations#terms).

