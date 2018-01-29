---
title: "Dostosowywanie rozwiązania połączonych fabryki - Azure | Dokumentacja firmy Microsoft"
description: "Opis sposobu dostosowywania zachowanie połączonych fabryki wstępnie skonfigurowane rozwiązanie."
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
ms.date: 12/14/2017
ms.author: dobett
ms.openlocfilehash: 48c8036d0bc9534ce94529b96d32b004769246c1
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Dostosuj sposób rozwiązania połączonych fabryki wyświetlania danych z serwerów OPC UA

Rozwiązanie połączonych fabryki agreguje i wyświetla dane z serwerów OPC UA nawiązaniu połączenia z rozwiązaniem. Można wybrać i wysyłać polecenia do serwerów OPC UA w rozwiązaniu. Aby uzyskać więcej informacji na temat OPC UA, zobacz [Connected factory FAQ (Połączona fabryka — często zadawane pytania)](iot-suite-faq-cf.md).

Przykładami zagregowane dane w rozwiązaniu ogólną wydajność sprzętu (OEE) oraz kluczowych wskaźników wydajności (KPI) widoczne na pulpicie nawigacyjnym poziomie fabryki, wiersza i stacji. Poniższy zrzut ekranu przedstawia wartości OEE i KPI **zestawu** stacji na **wiersza produkcyjnym 1**w **we Wrocławiu** fabryki:

![Przykładowe wartości OEE i wskaźnika KPI w rozwiązaniu][img-oee-kpi]

Rozwiązanie umożliwia wyświetlenie szczegółowych informacji z elementów określonych danych z serwerów OPC UA, nazywany *stacji*. Poniższy zrzut ekranu przedstawia powierzchni liczba wyprodukowanych elementów z określonym stacji:

![Liczba elementów wyprodukowanych wykresy][img-manufactured-items]

Kliknięcie wykresy można eksplorować danych za pomocą czasu serii Insights (TSI):

![Eksploruj dane przy użyciu czasu serii Insights][img-tsi]

W tym artykule opisano:

- Jak danych ma zostać udostępnione różne widoki w rozwiązaniu.
- Jak można dostosować sposób rozwiązania wyświetla dane.

## <a name="data-sources"></a>Źródła danych

Rozwiązanie połączonych fabryki wyświetla dane z serwerów OPC UA nawiązaniu połączenia z rozwiązaniem. Domyślna instalacja obejmuje kilka serwerów OPC UA systemem symulacji fabryki. Można dodać serwery OPC UA który [łączenie się za pośrednictwem bramy] [ lnk-connect-cf] do rozwiązania.

Możesz przejść elementów danych, które połączony serwer OPC Agent użytkownika może wysłać do rozwiązania na pulpicie nawigacyjnym:

1. Wybierz **przeglądarki** można przejść do **wybierz serwer OPC UA** widoku:

    ![Przejdź do wybierz Widok serwera OPC UA][img-select-server]

1. Wybierz serwer i kliknij przycisk **Connect**. Kliknij przycisk **Kontynuuj** gdy pojawi się ostrzeżenie o zabezpieczeniach.

    > [!NOTE]
    > To ostrzeżenie występuje raz dla każdego serwera i tylko ustanawia relację zaufania między pulpit nawigacyjny rozwiązania i serwer.

1. Możesz teraz przeglądać elementów danych, które serwer może wysłać do rozwiązania. Zaznaczono elementów, które są wysyłane do rozwiązania:

    ![Opublikowane elementy][img-published]

1. Jeśli jesteś *administratora* w rozwiązaniu, możesz opublikować element danych, aby była ona dostępna w rozwiązaniu fabryka połączenia. Jako Administrator możesz zmienić wartości elementów danych i wywołanie metody Server OPC UA.

## <a name="map-the-data"></a>Mapowania danych

Rozwiązanie połączonych fabryki mapuje i agreguje elementy opublikowanych danych z serwera OPC UA do różnych widoków w rozwiązaniu. Podczas obsługi administracyjnej rozwiązania rozwiązania połączonych fabryki wdraża się do konta platformy Azure. Plik JSON w rozwiązaniu Visual Studio połączone fabryki przechowuje informacje o mapowaniu. Można wyświetlać i modyfikować tego pliku konfiguracji JSON w fabryce połączonych rozwiązania Visual Studio. Po wprowadzeniu zmiany można ponownie wdrożyć rozwiązanie.

Możesz użyć pliku konfiguracji do:

- Edytowanie istniejącego fabryki symulowane, linii produkcyjnych i stacji.
- Mapowanie danych rzeczywistych serwerów OPC UA, których połączenia z rozwiązaniem.

Aby uzyskać więcej informacji dotyczących mapowania i agregowanie danych do własnych wymagań, zobacz [Konfigurowanie połączonych fabryki wstępnie skonfigurowane rozwiązanie ](iot-suite-connected-factory-configure.md).

## <a name="deploy-the-changes"></a>Wdrażanie zmiany

Po zakończeniu wprowadzania zmian do **ContosoTopologyDescription.json** pliku, należy ponownie wdrożyć rozwiązanie fabryki podłączonej do konta platformy Azure.

**Azure iot — połączony fabryka** repozytorium zawiera **build.ps1** skrypt programu PowerShell, można użyć, aby ponownie skompilować i wdrożyć rozwiązanie.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o rozwiązaniu połączonych fabryki wstępnie przeczytaj następujące artykuły:

* [Przewodnik po wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][lnk-rm-walkthrough]
* [Wdrażanie bramy dla połączonych fabryki][lnk-connect-cf]
* [Uprawnienia w witrynie azureiotsuite.com][lnk-permissions]
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
[lnk-permissions]: iot-suite-v1-permissions.md
[lnk-faq]: iot-suite-v1-faq.md