---
title: wprowadzenie do skalowania automatycznego na platformie Azure aaaGet | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooscale zasobu na platformie Azure."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a>Wprowadzenie do skalowania automatycznego na platformie Azure
W tym artykule opisano sposób tooset zapasową ustawień automatycznego skalowania dla zasobu w portalu Microsoft Azure hello.

Azure Monitor skalowania automatycznego ma zastosowanie tylko zestawy skalowania maszyny toovirtual, usługi w chmurze planów usługi aplikacji Azure i środowiska usługi aplikacji. 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a>Wykryj ustawienia skalowania automatycznego hello w ramach subskrypcji
Umożliwia odnalezienie wszystkich zasobów hello, dla których ma zastosowanie w monitorze Azure skalowania automatycznego. Użyj hello następujące kroki, aby uzyskać wskazówki krok po kroku:

1. Otwórz hello [portalu Azure.][1]
2. Kliknij ikonę monitora Azure hello w okienku po lewej stronie powitania.
  ![Otwórz Monitor Azure][2]
3. Kliknij przycisk **skalowania automatycznego** tooview wszystkie zasoby hello, dla których skalowania automatycznego ma zastosowanie, wraz z ich bieżący stan automatycznego skalowania.
  ![Odnajdywanie automatycznego skalowania w Monitorze systemu Azure][3]

Okienko filtru hello można użyć w hello tooscope top w dół hello listy tooselect zasoby w określonej grupy zasobów, określonych typów zasobów ani konkretnego zasobu.

Dla każdego zasobu można znaleźć hello bieżącą liczbę wystąpień i hello skalowania automatycznego stanu. Witaj stanu automatycznego skalowania może być:

- **Nieskonfigurowane**: nie włączono automatycznego skalowania jeszcze dla tego zasobu.
- **Włączone**: funkcja automatycznego skalowania zostało włączone dla tego zasobu.
- **Wyłączone**: funkcja automatycznego skalowania zostało wyłączone dla tego zasobu.

## <a name="create-your-first-autoscale-setting"></a>Tworzenie pierwszego Ustawienia skalowania automatycznego

Umożliwia teraz przejść przez toocreate proste wskazówki krok po kroku pierwszego Ustawienia skalowania automatycznego.

1. Otwórz hello **skalowania automatycznego** bloku Azure Monitor i wybierz zasób, które mają tooscale. (hello następujące kroki Użyj planu usługi aplikacji skojarzone z aplikacją sieci web. Możesz [tworzenie pierwszej aplikacji sieci web platformy ASP.NET na platformie Azure w ciągu 5 minut.] [4])
2. Należy pamiętać, że bieżąca liczba wystąpień hello 1. Kliknij przycisk **Włączanie automatycznego skalowania**.
  ![Ustawienia skalowania dla nowej aplikacji sieci web][5]
3. Podaj nazwę dla ustawienia skalowania hello, a następnie kliknij przycisk **dodać regułę**. Zwróć uwagę, opcje reguły skalowania hello Otwórz okienko kontekstu hello prawej strony. Domyślnie to ustawienie tooscale opcji hello wystąpienia liczba 1, jeśli hello procent użycia procesora CPU zasobu hello przekracza 70 procent. Pozostaw wartości domyślne, a następnie kliknij przycisk **Dodaj**.
  ![Utwórz ustawienie skali dla aplikacji sieci web][6]
4. Został już utworzony pierwszej reguły skalowania. Należy pamiętać, że hello UX zaleca najlepszych rozwiązań i stanów "zalecane jest toohave co najmniej jeden skali w regule." toodo tak:
  
    a. Kliknij przycisk **dodać regułę**. 

    b. Ustaw **Operator** za**mniej niż**.

    c. Ustaw **próg** za**20**.

    d. Ustaw **operacji** za**zmniejszyć liczbę przez**.

   Teraz powinna mieć ustawienia skalowania czy skale poza/możliwość skalowania w oparciu o użycie procesora CPU.
   ![Oparte na Procesorze skali][8]
5. Kliknij pozycję **Zapisz**.

Gratulacje! Pierwszy tooautoscale w Ustawienia skalowania aplikacji sieci web oparta na użycie procesora CPU teraz została pomyślnie utworzona.

> [!NOTE] 
> Witaj te same kroki są stosowane tooget wprowadzenie do skalowania maszyny wirtualnej zestawu lub w chmurze usługi roli.

## <a name="other-considerations"></a>Inne zagadnienia
### <a name="scale-based-on-a-schedule"></a>Skala zgodnie z harmonogramem
Ponadto tooscale oparte na Procesorze, można ustawić na skalę inaczej określone dni tygodnia hello.

1. Kliknij przycisk **Dodaj warunek skali**.
2. Skala hello reguły trybu i hello jest sama hello jako hello domyślnego warunku.
3. Wybierz **Powtórz określone dni** hello harmonogramu.
4. Wybierz hello dni i godziny rozpoczęcia i zakończenia hello stosowania hello Skala warunkiem.

![Skala warunkiem na podstawie harmonogramu][9]
### <a name="scale-differently-on-specific-dates"></a>Skalowanie inaczej w określonym dniu
Ponadto tooscale oparte na Procesorze, można ustawić na skalę inaczej dla określonej daty.

1. Kliknij przycisk **Dodaj warunek skali**.
2. Skala hello reguły trybu i hello jest sama hello jako hello domyślnego warunku.
3. Wybierz **określ daty rozpoczęcia i zakończenia** hello harmonogramu.
4. Wybierz hello rozpoczęcia i zakończenia daty i godziny rozpoczęcia i zakończenia hello stosowania hello Skala warunkiem.

![Warunek skali na podstawie dat][10]

### <a name="view-hello-scale-history-of-your-resource"></a>Wyświetl historię skali hello zasobu
Zawsze, gdy zasób jest skalowana w górę lub w dół, zdarzenie jest rejestrowane w dzienniku aktywności hello. Można wyświetlić historię skali hello zasobu dla hello ostatnich 24 godzin przełączając toohello **Historia uruchomień** kartę.

![Historia uruchomień][11]

Jeśli chcesz, aby tooview hello skali pełną historię (dla too90 dni w górę), wybierz pozycję **kliknij tutaj toosee szczegółowe**. Umożliwia otwarcie dziennika aktywności Hello z automatycznego skalowania jest wstępnie zaznaczona dla zasobu i kategorii.

### <a name="view-hello-scale-definition-of-your-resource"></a>Witaj skali definicji zasobu
Skalowania automatycznego jest zasobem usługi Azure Resource Manager. Hello definicji skali można wyświetlić w formacie JSON, przełączając toohello **JSON** kartę.

![Definicja skali][12]

Należy wprowadzić zmiany w formacie JSON, jeśli jest to wymagane. Te zmiany zostaną uwzględnione po ich zapisaniu.

### <a name="disable-autoscale-and-manually-scale-your-instances"></a>Wyłączanie automatycznego skalowania i ręcznie skalować swoich wystąpień
Może być razy podczas mają toodisable bieżące ustawienia skali i ręcznie skalować zasób.

Kliknij przycisk hello **wyłączanie automatycznego skalowania** przycisk u góry hello.
![Wyłączanie automatycznego skalowania][13]

> [!NOTE] 
> Ta opcja powoduje wyłączenie konfiguracji. Jednak możesz odzyskać tooit po włączeniu skalowania automatycznego ponownie. 

Można teraz ustawić hello liczba wystąpień, które mają tooscale toomanually.

![Zestaw skali ręczne][14]

Możesz zawsze wrócić, klikając tooAutoscale **Włączanie automatycznego skalowania** , a następnie **zapisać**.

## <a name="next-steps"></a>Następne kroki
- [Utwórz Alert dziennika aktywności toomonitor wszystkie operacje aparat skalowania automatycznego na subskrypcję](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Tworzenie alertów dziennika aktywności toomonitor wszystkie nieudane operacje w/skali skalowalnych w poziomie skalowania automatycznego na subskrypcję](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

