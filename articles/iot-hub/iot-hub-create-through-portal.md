---
title: aaaUse hello toocreate portalu Azure IoT Hub | Dokumentacja firmy Microsoft
description: "Jak toocreate, zarządzania i usuwania centra Azure IoT za pośrednictwem hello portalu Azure. Zawiera informacje na temat warstw cenowych, skalowania, zabezpieczeń i konfiguracji do obsługi komunikatów."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a>Tworzenie Centrum IoT przy użyciu hello portalu Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

W tym artykule opisano:

* Jak toofind hello usługi Centrum IoT w hello portalu Azure.
* Jak toocreate i zarządzanie nimi centra IoT.

## <a name="where-toofind-hello-iot-hub-service"></a>Gdzie toofind hello usługi Centrum IoT

Hello usługi Centrum IoT można znaleźć w następującej lokalizacji w portalu hello hello:

* Wybierz **+ nowy**, a następnie wybierz **Internetu rzeczy**.
* Hello Marketplace, wybierz **Internetu rzeczy**.

## <a name="create-an-iot-hub"></a>Tworzenie centrum IoT

Można utworzyć Centrum IoT przy użyciu hello następujące metody:

* Witaj **+ nowy** opcji Otwiera blok hello pokazano powitania po zrzut ekranu. Witaj kroki tworzenia Centrum IoT hello za pomocą tej metody i za pośrednictwem portalu marketplace hello są identyczne.
* Hello Marketplace, wybierz **Utwórz** bloku hello tooopen pokazano powitania po zrzut ekranu.

Witaj poniższych sekcjach opisano hello kilka kroków toocreate Centrum IoT:

### <a name="choose-hello-name-of-hello-iot-hub"></a>Wybierz nazwę hello hello Centrum IoT

toocreate Centrum IoT można nazwać hello Centrum IoT. Ta nazwa musi być unikatowa w wszystkie centra IoT.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a>Wybierz warstwę cenową hello

Możesz wybrać spośród czterech warstw: **wolne**, **Standard 1** i **standardowy 2**, i **standardowa S3**. Warstwa bezpłatna Hello umożliwia tylko 500 toobe urządzenia połączone z Centrum IoT toohello oraz too8, 000 wiadomości na dzień.

**Standardowa S1**: Użyj hello S1 edition dla rozwiązania IoT z dużą liczbą urządzeń, że wygenerowany dla każdego niewielkich ilości danych. Umożliwia każdej jednostki edition hello S1 się too400, 000 wiadomości na dzień dla wszystkich połączonych urządzeń.

**Standardowa S2**: Użyj hello S2 edition dla rozwiązania IoT, w których urządzenie wygenerować dużych ilości danych. Każdej jednostki hello S2 edition umożliwia się too6 milionów wiadomości na dzień między wszystkich połączonych urządzeń.

**Standardowa S3**: Użyj hello S3 edition dla rozwiązania IoT, które generują dużych ilości danych. Każdej jednostki hello S3 edition umożliwia się too300 milionów wiadomości na dzień między wszystkich połączonych urządzeń.

![][4]

> [!NOTE]
> Centrum IoT umożliwia tylko koncentratorze wolne dla subskrypcji platformy Azure.

### <a name="iot-hub-units"></a>Jednostki Centrum IoT

Hello liczbę wiadomości dozwolonych dla jednej jednostki dziennie zależy od warstwy cenowej Twoje Centrum. Na przykład jeśli chcesz, aby hello wejściowych toosupport Centrum IoT 700 000 komunikatów, wybierz dwie jednostki warstwy S1.

### <a name="device-toocloud-partitions-and-resource-group"></a>Partycje toocloud urządzenia i grupy zasobów

Możesz zmienić hello liczba partycji dla Centrum IoT. Witaj domyślny numer partycji jest 4, z listy rozwijanej hello można wybrać inny numer.

Nie trzeba tooexplicitly utworzyć pustej grupy zasobów. Podczas tworzenia zasobu, można wybrać albo toocreate nowy lub użyć istniejącej grupy zasobów.

![][5]

### <a name="choose-subscription"></a>Wybierz subskrypcję

Centrum IoT Azure automatycznie hello list konta użytkownika hello subskrypcji platformy Azure jest połączony. Można wybrać hello Centrum IoT hello tooassociate subskrypcji platformy Azure do.

### <a name="choose-hello-location"></a>Wybierz lokalizację hello

Opcja lokalizacji Hello zawiera listę regionów hello, w którym Centrum IoT jest dostępna.

### <a name="create-hello-iot-hub"></a>Tworzenie Centrum IoT hello

Po zakończeniu wszystkich poprzednich kroków, można utworzyć hello Centrum IoT. Kliknij przycisk **Utwórz** toostart hello toocreate procesu zaplecza i wdrażanie hello Centrum IoT z opcjami hello została wybrana opcja.

Jako zajmuje trochę czasu toorun wdrożenia zaplecza hello na serwerach odpowiednią lokalizację hello może potrwać kilka minut toocreate hello Centrum IoT.

## <a name="change-hello-settings-of-hello-iot-hub"></a>Zmień ustawienia hello hello Centrum IoT

Ustawienia hello istniejących Centrum IoT można zmienić po jego utworzeniu z hello blok Centrum IoT.

![][8]

**Zasady dostępu do udostępnionych**: te zasady definiują hello uprawnienia do urządzeń i usług tooIoT tooconnect koncentratora. Te zasady można uzyskać, klikając **zasady dostępu współużytkowanego** w obszarze **ogólne**. W tym bloku należy modyfikowania istniejących zasad lub Dodaj nowe zasady.

### <a name="create-a-policy"></a>Tworzenie zasad

* Kliknij przycisk **Dodaj** tooopen bloku. Tutaj można wprowadzić hello nową nazwę zasady i uprawnienia hello mają tooassociate z tymi zasadami, jak pokazano poniżej hello rysunek:

    Istnieje kilka uprawnienia, które mogą być skojarzone z tych zasad udostępnionych. Witaj **odczytać rejestru** i **zapisu rejestru** zasady przyznać odczytu i zapisu prawa toohello tożsamości rejestru. Wybranie opcji zapisu hello automatycznie wybiera hello odczytu opcji.

    Witaj **połączenia usługi** zasad punktów końcowych usługi tooaccess uprawnienia są daje takie jak **odbierania urządzenia do chmury**. Witaj **urządzenie połączyć** zasad przyznaje uprawnienia do wysyłania i odbierania wiadomości za pomocą punktów końcowych powitania po stronie urządzenia IoT Hub.

* Kliknij przycisk **Utwórz** tooadd tym nowo utworzone zasady toohello istniejącej listy.

![][10]

## <a name="endpoints"></a>Punkty końcowe

Kliknij przycisk **punkty końcowe** toodisplay listę punktów końcowych dla Centrum IoT hello, która jest modyfikowana. Istnieją dwa typy punktów końcowych: punkty końcowe wbudowanych w Centrum IoT hello i dodaj Centrum IoT toohello po jego utworzeniu.

![][11]

### <a name="built-in-endpoints"></a>Wbudowane punkty końcowe

Istnieją dwa punkty końcowe wbudowanych: **chmury opinii toodevice** i **zdarzenia**.

* **Chmury opinii toodevice** ustawienia: to ustawienie nie ma dwa subsettings: **chmury tooDevice TTL** (time-to-live) i **czas przechowywania** (w godzinach) dla wiadomości powitania. Podczas pierwszego tworzenia Centrum IoT, oba te ustawienia mają wartość hello jedną godzinę. tooadjust te ustawienia za pomocą suwaków hello, lub wpisz hello wartości.
* **Zdarzenia** ustawienia: to ustawienie nie ma kilka subsettings, niektóre z nich są tylko do odczytu. następujące listy Hello opisano te ustawienia:

  * **Partycje**: ustawiono wartość domyślną, podczas tworzenia Centrum IoT hello. Hello liczby partycji za pomocą tego ustawienia można zmienić.

  * **Nazwa zgodnych z Centrum zdarzeń i punktu końcowego**: podczas tworzenia Centrum IoT hello, że może muszą uzyskać dostęp toounder pewnych okolicznościach wewnętrznie tworzenia Centrum zdarzeń. Nie można przypisać wartości nazwy i punktu końcowego hello zgodnego Centrum zdarzeń, ale można je skopiować, klikając **kopiowania**.

  * **Czas przechowywania**: domyślnie ustawiony dzień tooone, ale można zmienić za pomocą listy rozwijanej hello. Ta wartość jest w dniach hello ustawienia urządzenia do chmury.

  * **Grupy konsumentów**: wiele komunikatów tooread czytników niezależnie od centrum IoT hello włączyć grupy odbiorców. Każdy Centrum IoT tworzona jest domyślna grupa odbiorców. Jednak można dodać lub usunąć konsumenta grup tooyour centra IoT za pomocą tego ustawienia.

  > [!NOTE]
  > Domyślna grupa odbiorców Hello nie można edytować ani usunąć.

### <a name="custom-endpoints"></a>Niestandardowe punkty końcowe

Można dodać niestandardowe punkty końcowe Centrum IoT przy użyciu portalu hello. Z hello **punkty końcowe** bloku, kliknij przycisk **Dodaj** na powitania top tooopen hello **dodać punkt końcowy** bloku. Wprowadź informacje wymagane hello, a następnie kliknij przycisk **OK**. Niestandardowe punktu końcowego zostanie wyświetlony w głównym hello **punkty końcowe** bloku.

![][13]

Więcej informacje niestandardowe punkty końcowe w [odwołanie — punkty końcowe Centrum IoT][lnk-devguide-endpoints].

## <a name="routes"></a>Trasy

Kliknij przycisk **tras** toomanage jak Centrum IoT wysyła wiadomości urządzenia do chmury.

![][14]

Centrum IoT tooyour tras można dodać, klikając **Dodaj** u góry hello hello **tras*** bloku wprowadzania informacji hello wymagane, a następnie klikając polecenie **OK**. Twoje trasy następnie znajduje się w głównym hello **tras** bloku. Można edytować trasę, klikając go na liście hello tras. tooenable trasy, kliknij go na liście hello tras i ustaw hello **włączone** Przełącz zbyt**poza**. toosave hello zmiany, kliknij przycisk **OK** u dołu hello hello bloku.

![][15]

## <a name="pricing-and-scale"></a>Ceny i skala

Hello cen istniejących Centrum IoT można zmienić, modyfikując hello **cennik** ustawienia z hello następujące wyjątki:

* W hello bieżąca implementacja Centrum IoT z bezpłatnej wersji nie można zmienić warstwy tooone z hello płatnej jednostki SKU, albo na odwrót.
* Może istnieć tylko jeden Centrum IoT warstwę bezpłatna w hello subskrypcji platformy Azure.

![][12]

Można przenosić z wyższego poziomu toolower tylko wtedy, gdy hello liczbę komunikatów wysłanych tego dnia przekracza hello przydziału hello dolnej warstwy. Na przykład jeśli hello liczbę wiadomości na dzień przekracza 400 000, hello warstwę hello IoT hub można zmienić. Jednak w przypadku zmiany warstwy S1 toohello Centrum IoT hello jest ograniczany do danego dnia.

## <a name="delete-hello-iot-hub"></a>Usuń hello Centrum IoT

Możesz przeglądać Centrum IoT toohello ma toodelete klikając **Przeglądaj**, i wybierając hello toodelete odpowiedniego koncentratora. toodelete hello Centrum IoT, kliknij przycisk hello **usunąć** znajdujący się poniżej nazwę Centrum IoT hello.

## <a name="next-steps"></a>Następne kroki

Wykonaj te toolearn łącza więcej informacji na temat zarządzania Centrum IoT Azure:

* [Zbiorcze zarządzania urządzeniami IoT][lnk-bulk]
* [Metryki Centrum IoT][lnk-metrics]
* [Operacje monitorowania][lnk-monitor]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]
* [Symuluje urządzenia IoT krawędzi][lnk-iotedge]
* [Zabezpieczanie rozwiązania IoT z hello tła w][lnk-securing]

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
