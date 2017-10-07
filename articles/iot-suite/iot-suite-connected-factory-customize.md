---
title: "Fabryka połączenia aaaCustomize pakiet IoT Azure | Dokumentacja firmy Microsoft"
description: "Opis sposób zachowania hello toocustomize hello połączenia fabryki wstępnie skonfigurowane rozwiązanie."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Dostosuj sposób hello połączenia fabryki rozwiązania wyświetla dane z serwerów OPC UA

## <a name="introduction"></a>Wprowadzenie

Hello połączonych fabryki rozwiązanie agreguje i wyświetla dane z hello OPC UA serwerów połączonych toohello rozwiązania. Można wybrać i wysyłać polecenia toohello OPC UA serwerów w rozwiązaniu. Aby uzyskać więcej informacji na temat OPC UA Zobacz hello [połączone fabryki — często zadawane pytania](iot-suite-faq-cf.md).

Przykładami zagregowane dane w rozwiązaniu hello hello ogólną wydajność sprzętu (OEE) i kluczowych wskaźników wydajności (KPI) widoczne na pulpicie nawigacyjnym hello na poziomach stacji, wiersza i hello fabryki. Witaj Poniższy zrzut ekranu przedstawia hello OEE i KPI wartości hello **zestawu** stacji na **wiersza produkcyjnym 1**, w hello **we Wrocławiu** fabryki:

![Przykładowe wartości OEE i wskaźnika KPI w rozwiązaniu hello][img-oee-kpi]

umożliwia rozwiązanie Hello możesz tooview szczegółowych informacji z elementów określonych danych z hello OPC UA serwery, nazywane *stacji*. Witaj Poniższy zrzut ekranu przedstawia powierzchni hello liczba wyprodukowanych elementów z określonym stacji:

![Liczba elementów wyprodukowanych wykresy][img-manufactured-items]

Kliknięcie wykresy hello można eksplorować danych hello za pomocą czasu serii Insights (TSI):

![Eksploruj dane przy użyciu czasu serii Insights][img-tsi]

W tym artykule opisano:

- Jak hello danych następuje toohello dostępne różne widoki w rozwiązaniu hello.
- Jak można dostosować hello sposób hello rozwiązanie przedstawia hello dane.

## <a name="data-sources"></a>Źródła danych

Witaj rozwiązania połączonych fabryki wyświetlane dane z hello OPC UA serwerów połączonych toohello rozwiązania. Witaj domyślna instalacja obejmuje kilka serwerów OPC UA systemem symulacji fabryki. Można dodać serwery OPC UA który [łączenie się za pośrednictwem bramy] [ lnk-connect-cf] tooyour rozwiązania.

Możesz przeglądać elementy danych hello podłączony serwer OPC Agent użytkownika może wysyłać rozwiązania tooyour na pulpicie nawigacyjnym hello:

1. Przejdź toohello **wybierz serwer OPC UA** widoku:

    ![Przejdź toohello wybierz Widok serwera OPC UA][img-select-server]

1. Wybierz serwer i kliknij przycisk **Connect**. Kliknij przycisk **Kontynuuj** gdy pojawi się ostrzeżenie o zabezpieczeniach hello.

    > [!NOTE]
    > To ostrzeżenie występuje raz dla każdego serwera i tylko ustanawia relację zaufania między hello pulpit nawigacyjny rozwiązania i powitania serwera.

1. Możesz teraz elementów danych hello przeglądania hello serwer może wysyłać toohello rozwiązania. Elementy, które są wysyłane toohello rozwiązania mają zielony znacznik wyboru:

    ![Opublikowane elementy][img-published]

1. Jeśli jesteś *administratora* hello rozwiązania, można wybrać toopublish toomake elementu danych ich w hello połączone fabryki rozwiązania. Jako Administrator możesz zmienić wartość hello elementów danych i wywoływać metod w hello OPC UA serwera.

## <a name="map-hello-data"></a>Dane mapy hello

Hello połączone fabryki rozwiązania map i hello zagregowanych danych elementy opublikowanych danych z hello toohello serwera OPC UA różne widoki w rozwiązaniu hello. Hello rozwiązania połączonych fabryki wdraża tooyour konta Azure podczas obsługi administracyjnej hello rozwiązania. Plik JSON w hello Visual Studio połączone fabryki rozwiązania przechowuje informacje o mapowaniu. Można wyświetlać i modyfikować tego pliku konfiguracji JSON w fabryce połączonych hello rozwiązania Visual Studio. Po wprowadzeniu zmiany można wdrożyć ponownie hello rozwiązania.

Program hello pliku konfiguracji:

- Edytowanie istniejącego fabryki symulowane hello, linii produkcyjnych i stacji.
- Mapowanie danych z rzeczywistego serwerów OPC UA połączyć z toohello rozwiązania.

tooclone kopię hello połączone fabryki rozwiązania Visual Studio, hello Użyj następujących poleceń git:

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

Plik Hello **ContosoTopologyDescription.json** definiuje hello elementów toohello widoki na pulpicie nawigacyjnym rozwiązania połączonych fabryki hello mapowania z hello OPC UA danych serwera. Ten plik konfiguracji można znaleźć w hello **Contoso\Topology** folderu w hello **aplikacji sieci Web** projektu w hello rozwiązania Visual Studio.

Hello zawartość pliku JSON hello jest zorganizowana jako hierarchię fabryki, wiersza produkcyjnym i węzły stacji. Ta hierarchia definiuje hierarchii nawigacji hello hello fabryki połączonych w pulpicie nawigacyjnym. Wartości w każdym węźle hierarchii hello określają hello informacje wyświetlane na pulpicie nawigacyjnym hello. Na przykład plik JSON hello zawiera hello następujące wartości hello fabryki we Wrocławiu:

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

Hello nazwę, opis oraz lokalizację są wyświetlane w tym widoku na pulpicie nawigacyjnym hello:

![Dane we Wrocławiu na pulpicie nawigacyjnym hello][img-munich]

Każdej fabryki wiersza produkcyjnym i stacji mają właściwość obrazu. Te pliki JPEG można znaleźć w hello **Content\img** folderu w hello **aplikacji sieci Web** projektu. Te pliki obrazów wyświetlane na pulpicie nawigacyjnym połączonych fabryki hello.

Każda stacja obejmuje kilka szczegółowe właściwości, które definiują hello mapowanie z hello OPC UA elementów danych. Te właściwości są opisane w hello następujące sekcje:

### <a name="opcuri"></a>OpcUri

Witaj **OpcUri** wartość jest hello OPC UA aplikacji URI, który unikatowo identyfikuje hello OPC UA serwera. Na przykład Witaj **OpcUri** wartość dla stacji zestawu hello wiersza produkcyjnym 1 w we Wrocławiu wygląda hello: **urn: scada2194:ua:munich:productionline0:assemblystation**.

Hello identyfikatorów URI hello połączone OPC UA serwerów można wyświetlić na pulpicie nawigacyjnym rozwiązania hello:

![Wyświetl OPC UA serwer identyfikatorów URI][img-server-uris]

### <a name="simulation"></a>Symulacja

informacje zawarte w hello Hello **symulacji** węzeł jest określonych toohello symulacji OPC UA, uruchomionego na powitania OPC UA serwerów, które są udostępniane domyślnie. Nie służy do rzeczywistego serwera OPC UA.

### <a name="kpi1-and-kpi2"></a>Kpi1 i Kpi2

Te węzły opisano, jak dane ze stacji hello wspiera toohello dwóch wartości wskaźnika KPI w hello pulpitu nawigacyjnego. We wdrożeniu domyślne wartości tych wskaźników KPI są jednostki na godzinę i kWh na godzinę. rozwiązanie Hello oblicza vales wskaźnik KPI na poziomie hello stacji i agregowanie ich na poziomie wiersza produkcyjnym hello i fabryki.

Każdy wskaźnik KPI ma minimum, maksimum i wartości docelowej. Każda wartość wskaźnika KPI można również zdefiniować akcje alertu dla tooperform rozwiązania fabryki hello połączony. Hello poniższy fragment kodu przedstawia hello KPI definicje dla stacji zestawu hello wiersza produkcyjnym 1 w we Wrocławiu:

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

Witaj Poniższy zrzut ekranu przedstawia hello KPI dane na pulpicie nawigacyjnym hello.

![Informacje dotyczące KPI na pulpicie nawigacyjnym hello][lnk-kpi]

### <a name="opcnodes"></a>OpcNodes

Hello **OpcNodes** zidentyfikować węzłów hello elementy opublikowanych danych z hello OPC UA serwera i określ sposób tooprocess tych danych.

Witaj **ID. węzła** wartość identyfikuje hello określonych ID. UA OPC węzła z hello OPC UA serwera. Witaj pierwszego węzła w stacji zestawu hello wiersza produkcyjnym 1 w we Wrocławiu ma wartość **ns = 2; i = 385**. A **ID. węzła** wartość określa hello danych elementu tooread z hello OPC UA serwera i hello **SymbolicName** zapewnia toouse przyjazną dla użytkownika nazwę, na pulpicie nawigacyjnym hello tych danych.

Witaj w poniższej tabeli przedstawiono inne wartości skojarzone z każdym węźle:

| Wartość | Opis |
| ----- | ----------- |
| Trafność  | wartości wskaźnika KPI i OEE Hello wspiera tych danych. |
| Kod operacji     | Jak hello są agregowane. |
| Jednostki      | Witaj toouse jednostki hello w pulpicie nawigacyjnym.  |
| Widoczne    | Czy toodisplay, ta wartość w hello pulpitu nawigacyjnego. Niektóre wartości są używane w obliczeniach, ale nie wyświetlany.  |
| Maksymalna    | Witaj maksymalna wartość wyzwalania alertu na pulpicie nawigacyjnym hello. |
| MaximumAlertActions | Tootake akcji w odpowiedzi tooan alertu. Na przykład wysyłać polecenia tooa stacji. |
| ConstValue | Stała wartość używana w obliczeniach. |

## <a name="deploy-hello-changes"></a>Wdrażanie hello zmiany

Po zakończeniu wprowadzania zmian toohello **ContosoTopologyDescription.json** pliku, należy ponownie wdrożyć hello połączone fabryki rozwiązania tooyour konto platformy Azure.

Witaj **azure iot — połączony fabryka** repozytorium zawiera **build.ps1** skrypt programu PowerShell, można użyć toorebuild i wdrożyć rozwiązanie hello.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o hello połączone fabryki wstępnie skonfigurowane rozwiązanie przez hello czytania następujących artykułów:

* [Przewodnik po wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][lnk-rm-walkthrough]
* [Wdrażanie bramy dla połączonych fabryki][lnk-connect-cf]
* [Uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions]
* [Często zadawane pytania dotyczące połączonej fabryki](iot-suite-faq-cf.md)
* [FAQ][lnk-faq]


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md