---
title: "Konfigurowanie i używanie Machine Learning zalecenia API | Dokumentacja firmy Microsoft"
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
redirect_document_id: TRUE
ms.openlocfilehash: 3851589818bb8f4309bf3c65f17b115e0dcd27fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>Konfigurowanie i używanie interfejsu API zaleceń usługi Machine Learning — często zadawane pytania
**Co to jest zalecenia?**

> [!NOTE]
> Należy rozpocząć korzystanie z usługi kognitywnych interfejsu API zalecenia zamiast tej wersji. Kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną nowe funkcje. Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.
> Dowiedz się więcej o [migracji do nowej usługi kognitywnych](http://aka.ms/recomigrate)
> 
> 

W przypadku organizacji i firm, które zależą od zaleceń dotyczących sprzedaży i sprzedaje up produktów i usług klientom zalecenia w usłudze Azure Machine Learning zapewnia aparat samoobsługi zalecenia. Jest implementację współpracy filtrowania, która używa factorization macierzy jako jego algorytmu core. Deweloperzy aplikacji można uzyskać dostępu do zalecenia za pomocą interfejsów API REST. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Co można zrobić z ZALECENIAMI?**

Zalecenia dotyczące przyjmuje jako wejście element lub zbiór elementów i zwraca listę odpowiednich zaleceń. Na przykład: klient sklepie internetowym kliknie produktu. Online detalicznej wysyła tego produktu jako dane wejściowe zalecenia, pobiera listę produktów w zamian i decyduje o tym, które z tych produktów będzie wyświetlana dla klienta. Może zajść potrzeba użycia zaleceń w celu zoptymalizowania sklepu online lub nawet powiadomienia użytkownika wewnątrz sprzedaży, działu lub wywołanie Centrum.

**Czy istnieją jakiekolwiek ograniczenia użycia?**

Zalecenia dotyczące ma następujące ograniczenia użycia:

* Maksymalna liczba modeli dla subskrypcji: 10
* Maksymalna liczba elementów, które mogą zawierać wykaz: 100 000
* Maksymalna liczba punktów użycia, które są zachowane jest ~ 5,000,000. Najstarszych zostanie usunięte, gdy nowe zostanie przekazany lub zgłaszane.
* Maksymalny rozmiar danych, który można wysłać w wiadomości e-mail (na przykład importu wykazu danych, importowanie danych użycia) to 200 MB
* Liczba transakcji na sekundę (TPS) dla kompilacji modelu zalecenia, która nie jest aktywny jest TPS ~ 2. Zalecenia kompilacji modelu, który jest aktywny może przechowywać maksymalnie 20 TPS.

## <a name="purchase-and-billing"></a>Zakup i rozliczenia
**Jaki jest koszt zalecenia w okresie uruchamiania?**

Zalecenia dotyczące jest usługą opartą na subskrypcję. Ładowanie opiera się na woluminie transakcji w miesiącu. Możesz sprawdzić [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations) w Microsoft Azure Marketplace w celu uzyskania informacji o cenach.

**Czy istnieją kosztów związanych z o zalecenia dotyczące śledzenia i przechowywania aktywności użytkownika?**

Nie w tej chwili.

**Zalecenia dotyczące ma bezpłatną wersję próbną?**

Brak wolnego dziennik, który jest ograniczony do 10 000 transakcji w miesiącu.

**Gdy zostanie I opłaty będą naliczane za zalecenia?**

Subskrypcja płatna jest żadnej subskrypcji, dla którego jest miesięcznej opłaty za. Po zakupie subskrypcji płatnej, natychmiast są naliczane do użytku w pierwszym miesiącu. Naliczane są opłaty kwotę, która jest skojarzona z ofertą na stronę subskrypcji (oraz podatków). Opłata miesięczna następuje co miesiąc, w tym samym dniu kalendarza jako pierwotnego zakupu do momentu anulowania subskrypcji. 

**Jak uaktualnić usługą wyższej warstwy**

Możesz kupić lub zaktualizować subskrypcji [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations) strony w witrynie Microsoft Azure Marketplace.

Po uaktualnieniu subskrypcji:

* Transakcje, które pozostały w ramach starego subskrypcji nie są dodawane do nowej subskrypcji. 
* Płać pełną cenę nowej subskrypcji, nawet jeśli masz nieużywane transakcji na starym subskrypcji.

Proces uaktualniania subskrypcji:

* Nevigate do [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations).
* Zaloguj się do witryny Marketplace, jeśli nie jest już zalogowany.
* W okienku po prawej stronie są wyświetlane wszystkie dostępne plany. Kliknij przycisk radiowy planu, który chcesz uaktualnić do wersji.
* Jeśli chcesz uaktualnić, kliknij przycisk **OK**. Jeśli nie chcesz uaktualnić, kliknij przycisk **anulować**.

**Ważne** należy dokładnie zapoznać się okno dialogowe przed rozpoczęciem uaktualniania, ponieważ istnieją rozliczeń i użycia.

**Kiedy skończy się subskrypcję zalecenia**

Subskrypcja zakończy się po anulowaniu jej. Jeśli chcesz anulować subskrypcji, zobacz poniższe instrukcje.

**Jak anulować subskrypcję zalecenia?**

Aby anulować subskrypcję, wykonaj następujące kroki. Jeśli Twojej bieżącej subskrypcji płatnej subskrypcji, subskrypcji nadal obowiązują do końca bieżącego okresu rozliczeniowego. Anulowania do obowiązywać natychmiast, należy skontaktować się z nami pod adresem [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Uwaga** zwrot nie podano anulowanie przed zakończeniem okresu rozliczeniowego lub nieużywane transakcji w okresie rozliczeniowym.

* Przejdź do [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations).
* Zaloguj się do witryny Marketplace, jeśli nie jest już zalogowany.
* Kliknij przycisk **anulować** z prawej strony nazwy zestawu danych i stanu. Możesz użyć tej subskrypcji do końca bieżącego okresu rozliczeniowego lub osiągnięto limit transakcji (cokolwiek nastąpi najpierw).

Jeśli chcesz anulować subskrypcję, natychmiast, więc możesz kupić nową subskrypcję, założyć zgłoszenie w [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Wprowadzenie do zalecenia
**Zalecenia dotyczące jest dla mnie?** 

Zalecenia w uczeniu maszynowym jest przeznaczony dla organizacji i firm, które zależą od zaleceń dotyczących sprzedaży i sprzedaje up produktów lub usług klientom. Jeśli masz witryny sieci Web skierowane do klientów, pracownicy działu sprzedaży, wewnętrznej pracownicy działu sprzedaży lub biurem, oraz Jeśli oferujesz katalogu więcej niż kilka dozen produktów lub usług wyników firmy mogą korzystać z zalecenia. 

Eksperymentowanie z zaleceniami ma być stosunkowo proste. Bieżąca wersja interfejsu API na podstawie wymaga podstawowe umiejętności programowania. Jeśli potrzebujesz pomocy, skontaktuj się z dostawcą, która opracowała witryny sieci Web. Jeśli masz wewnętrzny dział IT lub lokalnego projektanta, należy uzyskać zalecenia do działania. 

**Jakie są wymagania wstępne dotyczące konfigurowania zalecenia?**

Zalecenia dotyczące wymaga dziennika opcji użytkownika w odniesieniu do katalogu. Jeśli nie masz takiego dziennika i masz klienta witryna sieci Web, zalecenia mogą zbierać aktywność użytkowników dla Ciebie. 

Zalecenia dotyczące wymaga także katalog produktów i usług. Jeśli nie masz katalogu zalecenia można użyć klienta rzeczywiste dane użycia i przetwarzania wykazu. Dorozumiany katalogu nie będzie zawierać elementy, które nie zostały zgłoszone w ramach transakcji użytkownika.

**Sposób konfigurowania zalecenia po raz pierwszy**

Po [subskrybującą](https://datamarket.azure.com/dataset/amla/recommendations) zaleceń, należy używać w dokumentacji interfejsu API w [Azure Machine Learning zalecenia — Przewodnik Szybki Start](machine-learning-recommendation-api-quick-start-guide.md) do skonfigurowania usługi.

**Gdzie można znaleźć dokumentację interfejsu API?** 

Dokumentacja interfejsu API jest [Azure Machine Learning zalecenia — Przewodnik Szybki Start](machine-learning-recommendation-api-quick-start-guide.md).

**Jakie opcje czy mają przekazywać dane katalogu i użycia do zalecenia?**

Dostępne są dwie opcje do przekazywania danych katalogu i użycia: można eksportować dane z tego systemu CRM lub inne dzienniki i przekaż go do zalecenia lub można dodać tagów do witryny sieci Web, który będzie śledzić działania użytkowników. Jeśli używasz druga metoda, dane będą przechowywane na platformie Azure.

## <a name="maintenance-and-support"></a>Obsługi i pomocy technicznej
**Jak duży może być zestawu danych?**

Każdy zestaw danych może zawierać maksymalnie 100 000 elementów katalogu i 2048 MB danych użycia.
Ponadto subskrypcja może zawierać maksymalnie 10 zestawów danych (modeli).

**Gdzie można uzyskać pomoc techniczną dotyczącą zalecenia?**

Pomoc techniczna jest dostępna na [Microsoft Azure obsługuje](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) lokacji.

**Gdzie można znaleźć warunki użytkowania?**

[Microsoft Azure Machine Learning zalecenia dotyczące interfejsu API warunków użytkowania usługi](https://datamarket.azure.com/dataset/amla/recommendations#terms).

