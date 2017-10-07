---
title: aaaAzure pakiet IoT i Logic Apps | Dokumentacja firmy Microsoft
description: "Samouczek dotyczący toohook się tooAzure Logic Apps pakiet IoT dla procesów biznesowych."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>Samouczek: Łączenie aplikacji logiki tooyour Azure IoT pakiet monitorowania zdalnego wstępnie skonfigurowane rozwiązanie
Witaj [pakiet IoT Microsoft Azure] [ lnk-internetofthings] zdalnego wstępnie skonfigurowane rozwiązanie monitorujące tooget doskonały sposób uruchomieniu szybko z zestawem funkcji na trasie exemplifies rozwiązania IoT. W tym samouczku przedstawiono sposób tooadd aplikacji logiki tooyour pakiet IoT Microsoft Azure monitorowania zdalnego wstępnie skonfigurowane rozwiązanie. Te kroki pokazują, jak może potrwać jeszcze bardziej rozwiązania IoT łącząc tooa proces biznesowy.

*Jeśli szukasz przewodnik dotyczący sposobu tooprovision monitorowania zdalnego wstępnie skonfigurowane rozwiązanie, zobacz [samouczek: rozpoczynanie pracy z rozwiązania IoT wstępnie hello][lnk-getstarted].*

Przed rozpoczęciem tego samouczka, wykonaj następujące czynności:

* Monitorowania zdalnego hello należy wstępnie skonfigurowane rozwiązanie w Twojej subskrypcji platformy Azure.
* Utwórz tooenable konta SendGrid toosend wiadomości e-mail, które wyzwala procesów biznesowych. Użytkownik może Załóż bezpłatne konto próbne w [SendGrid](https://sendgrid.com/) klikając **spróbuj bezpłatnie**. Po zarejestrowaniu bezpłatne konto próbne należy toocreate [klucz interfejsu API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) w SendGrid przyznająca uprawnienia toosend poczty. Należy ten klucz interfejsu API w dalszej części samouczka hello.

toocomplete tego samouczka, potrzebujesz programu Visual Studio 2015 lub Visual Studio 2017 toomodify hello akcji zaplecza hello wstępnie skonfigurowanego rozwiązania.

Zakładając, że została już przydzielona zdalne monitorowanie wstępnie skonfigurowane rozwiązanie, przejdź toohello grupy zasobów dla rozwiązania w hello [portalu Azure][lnk-azureportal]. Witaj grupa zasobów ma hello sama nazwa hello rozwiązania nazw można wybrać podczas obsługi administracyjnej rozwiązania monitorowania zdalnego. W grupie zasobów hello widać hello wszystkie udostępnione zasoby platformy Azure dla rozwiązania z wyjątkiem hello aplikacji usługi Azure Active Directory, która znajduje się w hello klasycznego portalu Azure. Witaj Poniższy zrzut ekranu przedstawia przykład **grupy zasobów** bloku zdalnego monitorowania wstępnie skonfigurowane rozwiązanie:

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin, skonfiguruj hello logiki aplikacji toouse z hello wstępnie skonfigurowane rozwiązanie.

## <a name="set-up-hello-logic-app"></a>Konfigurowanie hello aplikacji logiki
1. Kliknij przycisk **Dodaj** u góry bloku grupy zasobów, korzystając z portalu Azure hello hello.
2. Wyszukaj **aplikacji logiki**, zaznacz go, a następnie kliknij przycisk **Utwórz**.
3. Wypełnianie hello **nazwa** i użyj hello sam **subskrypcji** i **grupy zasobów** użyto podczas przydzielania zdalnego rozwiązanie monitorowania. Kliknij przycisk **Utwórz**.
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. Po zakończeniu wdrożenia widać hello jest wyświetlana logiki aplikacji jako zasób w grupie zasobów.
5. Kliknij przycisk bloku aplikacji logiki toonavigate toohello hello aplikacji logiki, wybierz hello **pustą aplikację logiki** hello tooopen szablonu **projektanta aplikacji logiki**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. Wybierz **żądania**. Ta akcja określa, czy przychodzące żądanie HTTP o określonych JSON w formacie ładunku czynności wyzwalacza.
7. Wklej powitania po kodu na powitania żądania schematu JSON treści:
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > Po zapisaniu hello aplikacji logiki, ale najpierw należy dodać akcję, możesz skopiować adres URL hello hello HTTP post.
   > 
   > 
8. Kliknij przycisk **+ nowy krok** w obszarze ręczne wyzwalacz. Następnie kliknij przycisk **Dodaj akcję**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. Wyszukaj **SendGrid — wysyłanie wiadomości e-mail** i kliknij ją.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. Wprowadź nazwę połączenia hello, takich jak **SendGridConnection**, wprowadź hello **klucz interfejsu API SendGrid** zostały utworzone podczas konfiguracji konta SendGrid i kliknij przycisk **Utwórz**.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. Dodaj e-mail adresy hello własnych tooboth **z** i **do** pola. Dodaj **zdalnego alert monitorowania [DeviceId]** toohello **podmiotu** pola. W hello **treść wiadomości E-mail** pól, Dodaj **urządzenia [DeviceId] zgłosił [measurementName] o wartości [measuredValue].** Możesz dodać **[DeviceId]**, **[measurementName]**, i **[measuredValue]** , klikając w hello **można wstawić danych z poprzednich kroków**sekcji.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. Kliknij przycisk **zapisać** w menu u góry hello.
13. Kliknij przycisk hello **żądania** hello wyzwalacza i skopiuj **adres URL toothis Http Post** wartość. Ten adres URL jest potrzebne w dalszej części tego samouczka.

> [!NOTE]
> Aplikacje logiki włączyć toorun [wiele różnych typów akcji] [ lnk-logic-apps-actions] łącznie z działaniami w usłudze Office 365. 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>Konfigurowanie hello EventProcessor zadanie sieci Web
W tej sekcji można podłączyć toohello Twoje wstępnie skonfigurowane rozwiązanie tworzenia aplikacji logiki. toocomplete to zadanie, musisz dodać hello adresu URL tootrigger hello aplikacji logiki toohello akcję, która generowane, gdy wartość czujnik urządzenia przekracza próg.

1. Użyj programu git klienta tooclone hello najnowszą wersję hello [azure iot — zdalnego monitorowania repozytorium github][lnk-rmgithub]. Na przykład:
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. W programie Visual Studio Otwórz hello **RemoteMonitoring.sln** z hello lokalną kopię hello repozytorium.
3. Otwórz hello **ActionRepository.cs** pliku w hello **infrastruktury\\repozytorium** folderu.
4. Aktualizacja hello **actionIds** słownik z hello **adres URL toothis Http Post** zanotowane aplikację logiki w następujący sposób:
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. Zapisz zmiany hello w rozwiązaniu i zamknij Visual Studio.

## <a name="deploy-from-hello-command-line"></a>Wdrażanie z wiersza polecenia hello
W tej sekcji możesz wdrożyć aktualizowaną wersję hello zdalnego monitorowania tooreplace hello wersja rozwiązania aktualnie uruchomione na platformie Azure.

1. Następujące hello [konfiguracji deweloperów] [ lnk-devsetup] instrukcje tooset Twojego środowiska do wdrożenia.
2. Postępuj zgodnie z lokalnie, toodeploy hello [lokalnego wdrożenia] [ lnk-localdeploy] instrukcje.
3. toodeploy toohello w chmurze i aktualizowanie istniejącego wdrożenia chmury, wykonaj hello [wdrożenie w chmurze] [ lnk-clouddeploy] instrukcje. Użyj nazwy hello oryginalnego wdrożenia jako nazwa wdrożenia hello. Na przykład jeśli została wywołana hello oryginalnego wdrożenia **demologicapp**, użyj następującego polecenia hello:
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   Podczas hello utworzyć skrypt będzie uruchamiany, należy upewnić się, toouse hello same konta Azure, subskrypcji, regionu i wystąpienie usługi Active Directory, używane podczas przydzielania hello rozwiązania.

## <a name="see-your-logic-app-in-action"></a>Wyświetlanie aplikacji logiki w akcji
zdalne monitorowanie wstępnie skonfigurowane rozwiązanie Hello ma dwie reguły konfigurowane domyślnie podczas obsługi administracyjnej rozwiązania. Obie zasady są na powitania **SampleDevice001** urządzenia:

* Temperatury > 38.00
* Wilgotność > 48.00

zasada temperatury Hello wyzwala hello **podnieść Alarm** akcji i hello zasada wilgotności wyzwala hello **SendMessage** akcji. Zakładając, że użyto hello tego samego adresu URL dla obu hello akcje **ActionRepository** klasy z wyzwalaczy aplikacji logiki dla każdej reguły. Obie reguły użyj toosend SendGrid toohello e-mail **do** adres ze szczegółami alertu hello.

> [!NOTE]
> tootrigger Hello aplikacji logiki będzie nadal występować, za każdym razem, gdy zostały spełnione warunki progowe hello. tooavoid niepotrzebnych wiadomości e-mail, możesz wyłączyć reguły hello w Twoje rozwiązanie portalu lub wyłącz hello aplikacji logiki w hello [portalu Azure][lnk-azureportal].
> 
> 

Ponadto tooreceiving wiadomości e-mail, zostanie również wyświetlony po uruchomieniu hello aplikacji logiki w portalu hello:

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>Następne kroki
Teraz, gdy proces biznesowy aplikacji logiki tooconnect hello wstępnie skonfigurowane rozwiązanie tooa była używana, można dowiedzieć się więcej o hello opcje dostosowywania hello wstępnie rozwiązań:

* [Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorujące hello][lnk-dynamic]
* [Urządzenie informacji metadanych w hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-devinfo]

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
