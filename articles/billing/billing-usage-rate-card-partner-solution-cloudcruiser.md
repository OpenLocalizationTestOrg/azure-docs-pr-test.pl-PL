---
title: "aaaCloud Cruiser i rozliczeń integracji interfejsu API programu Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Zawiera unikatowy perspektywy Microsoft Azure Billing partnera Cruiser chmury ich doświadczeń integrowanie hello interfejsów API usługi Azure rozliczeń ich produktu.  Jest to szczególnie przydatne dla platformy Azure i w chmurze Cruiser użytkowników, którzy chcą przy użyciu/próby Cruiser chmury dla pakietu Microsoft Azure Pack."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: 74cc19bdeed26c6684210736caa0cb365e8f8821
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a>Cruiser i rozliczeń integracji interfejsu API platformy Microsoft Azure w chmurze
W tym artykule opisano, jak hello informacje zebrane z hello nowe Microsoft rozliczeń interfejsów API usługi Azure może być używane w chmurze Cruiser przepływu pracy koszt symulacji i analizy.

## <a name="azure-ratecard-api"></a>Interfejs API Azure RateCard
Hello RateCard API informacje szybkość z platformy Azure. Po uwierzytelnieniu z właściwymi poświadczeniami hello można zbadać hello interfejsu API toocollect metadane dotyczące usług hello dostępnych na platformie Azure, wraz z hello stawek dotyczących identyfikatora oferty

Witaj poniżej znajduje się przykładowa odpowiedź z interfejsu API hello przedstawiający cen hello hello A0 (z systemem Windows) wystąpienie:

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-tooazure-ratecard-api"></a>W Cruiser tooAzure interfejsu RateCard API w chmurze
Cruiser chmury można wykorzystać informacje RateCard API hello na różne sposoby. W tym artykule pokazano, jak może być używana toomake IaaS obciążenia koszt symulacji i analizy.

toodemonstrate to przypadek użycia, Wyobraź sobie obciążeń uruchomionych na Microsoft Azure Pack (map) kilka wystąpień. Celem Hello jest toosimulate tego samego obciążenie platformy Azure i oszacowanie kosztów hello wykonywania takich migracji. W celu toocreate Ta symulacja, istnieją dwie toobe główne zadania wykonywane:

1. **Importowanie i procesu hello usługi informacje zebrane z interfejsu API RateCard hello.** To zadanie, również odbywa się na skoroszyty hello, gdzie hello wyodrębniania z interfejsu API RateCard hello jest nowy plan szybkość tooa przekształcone i opublikowane. Tego nowego planu szybkość zostaną użyte na powitania symulacje tooestimate hello cen platformy Azure.
2. **Normalizuj WAP usług i usług platformy Azure dla IaaS.** Domyślnie usługi WAP są oparte na poszczególnych zasobów (procesora CPU, pamięci, rozmiar dysku itp.), podczas gdy platforma Azure usługi są oparte na rozmiar wystąpienia (A0 A1, A2, itp.). To zadanie pierwszy można wykonywany przez aparat ETL Cruiser chmury, o nazwie skoroszytów, gdzie dołączone tych zasobów rozmiarów wystąpienia analogiczne tooAzure wystąpienia usługi.

### <a name="import-data-from-hello-ratecard-api"></a>Importuj dane z hello RateCard interfejsu API
Skoroszyty Cruiser chmury zawierają zautomatyzowany sposób proces i toocollect informacje z hello RateCard interfejsu API.  ETL (extract — przekształcenia obciążenia) skoroszyty pozwalają tooconfigure hello kolekcji, przekształcania i publikowania danych w chmurze Cruiser hello w bazie danych.

Każdy skoroszyt można zawiera jeden lub wiele kolekcji, umożliwiając toocorrelate informacji z różnych źródeł toocomplement lub rozszerzyć hello danych użycia. powitania po dwóch show zrzuty ekranu przedstawiające sposób toocreate nowy *kolekcji* w istniejącym skoroszycie i importowania informacji do hello *kolekcji* z hello RateCard interfejsu API:

![Rysunek 1 — Tworzenie nowej kolekcji][1]

![Rysunek 2 — importowanie danych z hello nowej kolekcji][2]

Po zaimportowaniu danych hello do skoroszytu hello, jest możliwe toocreate wielu kroków i procesy przetwarzania, toomodify i modelu hello danych. W tym przykładzie ponieważ tylko Dbamy o infrastruktury jako — usługa (IaaS), możemy użyć hello przekształcania kroki tooremove zbędne wiersze lub rekordy, związanych z tooservices innych niż IaaS.

Witaj Poniższy zrzut ekranu przedstawia kroki przekształcania hello używane dane hello tooprocess zebrane z interfejsu API RateCard:

![Rysunek 3 – przekształcania kroki tooprocess zbierane dane z interfejsu API RateCard][3]

### <a name="defining-new-services-and-rate-plans"></a>Definiowanie nowych usług i szybkość plany
Istnieją różne sposoby toodefine usług w chmurze Cruiser. Jedną z opcji hello jest tooimport hello usług z hello danych użycia. Ta metoda jest często używana podczas pracy z chmur publicznych, gdzie usług hello są już zdefiniowane przez dostawcę hello.

Planie taryfowym to zestaw stawki lub cen, które mogą być zastosowane toodifferent usługi, na podstawie daty obowiązywania lub grupy odbiorców, między innymi opcjami. Szybkość planów można również w symulacji toocreate Cruiser chmury lub scenariuszy "Co jeśli", toounderstand wpływ hello całkowity koszt obciążeń zmian w usługach.

W tym przykładzie używamy hello informacji o usłudze z interfejsu API RateCard hello toodefine nowych usług w chmurze Cruiser. W hello takie same, możemy użyć hello stawek toohello usług toocreate nowego planu szybkość na Cruiser chmury.

Na końcu hello proces przekształcania hello jest możliwe toocreate nowy krok i publikowania danych hello hello RateCard API jako nowe usługi i szybkości.

![Rysunek 4 - publikowanie danych hello z hello RateCard API nowych usług i szybkości][4]

### <a name="verify-azure-services-and-rates"></a>Sprawdź usług platformy Azure i szybkości
Po opublikowaniu usługi hello i stawki, można sprawdzić hello listę importowanych usług w chmurze Cruiser *usług* karty:

![Rysunek 5. Sprawdzanie hello nowych usług][5]

Na powitania *plany szybkość* kartę, można sprawdzić hello nowy plan szybkość o nazwie "AzureSimulation" hello szybkości przetwarzania zaimportowane z hello RateCard interfejsu API.

![Rysunek 6 - weryfikowanie hello nowe planie taryfowym i skojarzone stawki][6]

### <a name="normalize-wap-and-azure-services"></a>Normalizuj WAP i usług Azure
Domyślnie WAP informacje użycia na podstawie zastosowania hello obliczeniowych, pamięci i zasobów sieciowych. W chmurze Cruiser można zdefiniować z usług oparty bezpośrednio na alokacji hello lub naliczane użycia tych zasobów. Na przykład można ustawić podstawowe szybkości dla każdej godziny użycia procesora CPU lub opłata hello GB pamięci przydzielonej tooan wystąpienia.

Na przykład w kolejności toocompare kosztów między WAP i platformą Azure potrzebujemy tooaggregate powitania od użycia zasobów na WAP na pakietów, które następnie mogą być mapowane tooAzure usług. Ta transformacja można zaimplementować łatwe w skoroszytach hello:

![Rysunek 7 - Przekształcanie usługi toonormalize danych WAP][7]

Ostatnim krokiem Hello w skoroszycie hello jest toopublish hello danych do bazy danych chmury Cruiser hello. W tym kroku dane użycia hello jest obecnie połączone w usługi (które mapują toohello usług Azure) i powiązane toodefault stawki toocreate hello opłat.

Po zakończenia hello skoroszytu można zautomatyzować hello przetwarzania danych hello, Dodawanie zadania na powitania harmonogramu i określając hello częstotliwość i godzinę dla hello toorun skoroszytu.

![Rysunek 8 - planowania skoroszytu][8]

### <a name="create-reports-for-workload-cost-simulation-analysis"></a>Tworzenie raportów analizy kosztów symulacji obciążenia
Po hello użycia są zbierane i opłaty są ładowane do bazy danych chmury Cruiser hello, możemy wykorzystać hello Insights Cruiser chmury modułu toocreate hello obciążenia koszt symulacji który konieczna jest firma Microsoft.

W kolejności toodemonstrate tego scenariusza, utworzono hello następującego raportu:

![Porównanie kosztów][9]

Witaj top wykres przedstawia porównania kosztów przez usługi porównanie ceny hello obciążenie pracą powitania dla każdej określonej usługi między WAP (ciemny niebieski) i Azure (niebieski światła).

Witaj dolnej wykres przedstawia hello tych samych danych, ale według działów. Oznacza to, hello kosztów dla każdego działu toorun swoje obciążeń na WAP i na platformie Azure, wraz z hello różnica między nimi w pasku oszczędności hello (zielony).

## <a name="azure-usage-api"></a>Interfejs API użycia platformy Azure
### <a name="introduction"></a>Wprowadzenie
Firma Microsoft wprowadziła ostatnio hello Azure użycia interfejsu API, stosowanie subskrybentów ściągania tooprogrammatically w użycia danych toogain wgląd w ich użycia. Jest to doskonały wiadomości dla klientów Cruiser chmury, które można wykorzystać hello bogaty zestaw danych dostępnych za pośrednictwem tego interfejsu API.

Cruiser chmury można wykorzystać hello integracji z hello użycia interfejsu API na kilka sposobów. Witaj szczegółowości (co godzinę informacje o użyciu) i zasobu metadane dostępne za pośrednictwem hello interfejsu API zapewnia hello niezbędne dataset toosupport elastyczne ogólnej analizy kosztów lub obciążenia zwrotnego modeli. 

W tym samouczku będziemy przedstawia przykład metody Cruiser chmury mogą korzystać z hello informacji użycia interfejsu API. W szczególności firma Microsoft będzie Utwórz grupę zasobów na platformie Azure, skojarzyć tagi dla struktury konta hello, a następnie opisują proces hello ściąganie i przetwarzania informacji znacznika hello w chmurze Cruiser.

Celem końcowego Hello jest raporty o stanie toocreate toobe powitania po jednej, takich jak i stanie tooanalyze kosztów i zużycia na podstawie struktury konta hello wypełnione według znaczników hello.

![Na rysunku nr 10 - raport o awarii przy użyciu tagów][10]

### <a name="microsoft-azure-tags"></a>Tagi platformy Microsoft Azure
Hello danych dostępne za pośrednictwem hello Azure API użycia obejmuje nie tylko informacje o, ale także w tym wszystkie znaczniki skojarzone z nim metadane zasobu. Tagi zapewniają prosty sposób tooorganize zasobów, ale w kolejności toobe skuteczne, potrzebujesz tooensure który:

* Tagi są poprawnie zastosowane toohello zasobów w czasie udostępniania
* Tagi prawidłowo są używane w strukturze konta hello ogólnej analizy kosztów/opłaty zwrotne procesu tootie hello użycia toohello organizacji.

Oba te wymagania może być trudne, szczególnie w przypadku ręczny proces udostępniania hello lub ładowania strony. Błędnie, nieprawidłowe lub niekompletne nawet tagi są typowych utrudnień klientów po przy użyciu tagów i błędy te mogą być wykonywane życia na powitania ładowania strony bardzo trudne.

Z hello nowy interfejs API użycia usługi Azure, Cruiser chmury można ściągnąć zasobów znakowanie informacji i za pomocą zaawansowanej ETL narzędzie skoroszytów, usunąć te typowe błędy znakowania. Za pomocą przekształcania za pomocą wyrażeń regularnych i korelacji danych Cruiser chmury można zidentyfikować niepoprawnie oznakowanych zasobów i zastosować hello poprawne tagów, zapewnienie skojarzenie poprawne hello hello zasobów z powitania klienta.

Na powitania ładowania strony Cruiser chmury automatyzuje hello procesu ogólnej analizy kosztów/opłaty zwrotne i można wykorzystać hello tag tootie hello użycia toohello odpowiednie konsumenta informacji (działu dzielenia, Project, itp.). Ta Automatyzacja zapewnia ogromny poprawy jakości i zapewnia spójne i podlegającą inspekcji procesu ładowania.

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a>Tworzenie grupy zasobów z tagami w systemie Microsoft Azure
Witaj pierwszy krok w tym samouczku jest toocreate grupy zasobów w hello portalu Azure, a następnie utworzyć nowe tagi tooassociate toohello zasobów. Na przykład możemy zostanie utworzony hello następujące znaczniki: działu, środowisko, właściciel projektu.

Hello Poniższy zrzut ekranu przedstawia przykład grupy zasobów z hello skojarzonych tagów.

![Rysunek 11 — grupa zasobów o znacznikach w portalu Azure][11]

Witaj następnym krokiem jest toopull hello informacje z hello użycia interfejsu API w chmurze Cruiser. Witaj użycia interfejsu API zawiera obecnie odpowiedzi w formacie JSON. Oto przykładowe dane hello pobrane:

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-hello-usage-api-into-cloud-cruiser"></a>Importuj dane z hello użycia interfejsu API w chmurze Cruiser
Skoroszyty Cruiser chmury zawierają zautomatyzowany sposób proces i toocollect informacje z hello użycia interfejsu API. Skoroszyt ETL (extract — przekształcenia obciążenia) umożliwia tooconfigure hello kolekcji, przekształcania i publikowania danych w chmurze Cruiser hello w bazie danych.

Każdego skoroszytu mogą mieć jeden lub wiele kolekcji. Dzięki temu toocorrelate informacje z różnych źródeł toocomplement lub rozszerzyć hello użycia danych. W tym przykładzie zostanie utworzony nowy arkusz w skoroszycie szablonu Azure hello (*UsageAPI)* i ustaw nowy *kolekcji* tooimport informacji z hello użycia interfejsu API.

![Rysunek 3 – zaimportowane do arkusza UsageAPI hello danych użycia interfejsu API][12]

Powiadomienie, że ten skoroszyt już zawiera inne arkusze tooimport usług z platformy Azure (*ImportServices*) i przetwarzania informacji o użyciu hello z hello rozliczeń interfejsu API (*PublishData*).

Następnie użyjemy hello użycia interfejsu API toopopulate hello *UsageAPI* arkusza i informacje korelowanie hello hello zużycie danymi z hello rozliczeń interfejsu API na powitania *PublishData* arkusza.

### <a name="processing-hello-tag-information-from-hello-usage-api"></a>Przetwarzanie informacji dotyczących tag hello z hello użycia interfejsu API
Po zaimportowaniu danych hello do skoroszytu hello, utworzymy kroki transformacji w hello *UsageAPI* arkusza w kolejności tooprocess hello informacji z hello interfejsu API. Pierwszym krokiem jest toouse "Podział JSON" hello tooextract procesora tagów z jednego pola, a następnie utwórz pól dla jednej z nich (działu, projektu właściciela i środowiska).

![Rysunek 4. Utwórz nowe pola informacji tag hello][13]

Witaj powiadomienia usługi "Sieć" brakuje informacji tag hello (żółty pole), ale można sprawdzić, czy jest ona częścią hello tej samej grupie zasobów, analizując hello *ResourceGroupName* pola. Ponieważ hello tagów hello będziemy mieć inne zasoby z tej grupy zasobów, możemy użyć tego hello tooapply informacji Brak tagów toothis zasobu w dalszej części procesu hello.

Witaj następnym krokiem jest toocreate wyszukiwania tabeli kojarzenia hello informacji z hello tagi toohello *ResourceGroupName*. Ta tabela odnośników będą używane w hello następny krok tooenrich hello zużycie danych za pomocą informacji znacznika.

### <a name="adding-hello-tag-information-toohello-consumption-data"></a>Dodawanie hello tag informacji toohello dane dotyczące zużycia
Teraz możemy przejść toohello *PublishData* arkuszu, które procesy hello informacji o użyciu z hello rozliczeń interfejsu API, a następnie dodaj pola hello wyodrębnione ze znaczników hello. Ten proces odbywa się przez wyszukiwanie w tabeli odnośników hello utworzony na powitania poprzedniego kroku, przy użyciu hello *ResourceGroupName* jako klucz hello hello wyszukiwań.

![Rysunek 5 - wypełnianie hello strukturę hello informacje z hello wyszukiwań][14]

Zwróć uwagę, że zostały zastosowane hello odpowiednie konto struktury pól dla usługi "Sieć" hello, naprawienie problemu hello z hello Brak tagów. Możemy również wypełnione pola struktury konta hello zasobów niż naszych docelowej grupy zasobów "Inne", w kolejności toodifferentiate je na powitania raporty.

Teraz potrzebujemy tooadd krok toopublish hello użycia danych. W tym kroku hello odpowiednie szybkości dla każdej usługi zdefiniowane w naszym planie taryfowym będzie zastosowanych toohello informacje dotyczące użycia z opłatą wynikowy hello ładowane do hello bazy danych.

najlepsze w Hello jest tylko toogo w tym procesie raz. Po zakończeniu hello skoroszytu, wystarczy tooadd on toohello harmonogramu i będzie uruchamiane co godzinę lub codziennie hello zaplanowana godzina. Jest to jedynie tworzenie nowych raportów lub dostosowywanie istniejących w kolejności tooanalyze hello danych tooget wgląd w istotne dane z użycie w chmurze.

### <a name="next-steps"></a>Następne kroki
* Dla szczegółowe instrukcje dotyczące tworzenia chmury Cruiser skoroszyty i raportów, zobacz tooCloud Cruiser obiektu online [dokumentacji](http://docs.cloudcruiser.com/) (nieprawidłowa jest wymagana nazwa logowania).  Aby uzyskać więcej informacji na temat Cruiser chmury, skontaktuj się z [ info@cloudcruiser.com ](mailto:info@cloudcruiser.com).
* Zobacz [uzyskać wgląd w Microsoft Azure użycia zasobów](billing-usage-rate-card-overview.md) omówienie API RateCard i hello użycia zasobów Azure.
* Zapoznaj się z hello [dokumentacja interfejsu API REST rozliczenia Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) uzyskać więcej informacji na obu interfejsów API, które są częścią hello zestaw interfejsów API dostarczonych przez hello Azure Resource Manager.
* Jeśli chcesz toodive bezpośrednio w hello przykładowy kod, wyewidencjonuj naszych Microsoft Azure Billing interfejsu API przykłady kodu na [przykłady kodu Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

### <a name="learn-more"></a>Dowiedz się więcej
* Zobacz hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) więcej informacji na temat usługi Azure Resource Manager hello toolearn artykułu.

<!--Image references-->

[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Rysunek 1 — Tworzenie nowej kolekcji"
[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Rysunek 2 — importowanie danych z hello nowej kolekcji"
[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Rysunek 3 – przekształcania kroki tooprocess zbierane dane z interfejsu API RateCard"
[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Rysunek 4 - publikowanie danych hello z hello RateCard API nowych usług i szybkości"
[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Rysunek 5. Sprawdzanie hello nowych usług"
[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Rysunek 6 - weryfikowanie hello nowe planie taryfowym i skojarzone stawki"
[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Rysunek 7 - Przekształcanie usługi toonormalize danych WAP"
[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Rysunek 8 - planowania skoroszytu"
[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Rysunek 9 — przykładowy raport dla scenariusza porównania kosztów obciążenia hello"
[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Na rysunku nr 10 - raport o awarii przy użyciu tagów"
[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Rysunek 11 — grupa zasobów o znacznikach w portalu Azure"
[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Rysunek 12 — zaimportowane do arkusza UsageAPI hello danych użycia interfejsu API"
[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Rysunek 13 — Utwórz nowe pola informacji tag hello"
[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Rysunek 14 - wypełnianie hello strukturę hello informacje z hello wyszukiwań"
