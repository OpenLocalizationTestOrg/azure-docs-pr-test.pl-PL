---
title: "aaaAdvanced skalowania automatycznego przy użyciu usługi Azure Virtual Machines | Dokumentacja firmy Microsoft"
description: "Używa usługi Resource Manager i zestawy skalowania maszyny Wirtualnej z wielu zasad i profilów, które wysyłania wiadomości e-mail i Wywołaj adresy URL elementu webhook z akcji skalowania."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a>Zestawy skalowania maszyny Wirtualnej za pomocą szablonów usługi Resource Manager konfiguracji zaawansowanej skalowania automatycznego
Można w skali i skalowalnego w poziomie w zestawy skalowania maszyny wirtualnej w oparciu metryki progów wydajności, zgodnie z cyklicznym harmonogramem lub w określonym dniu. Można również skonfigurować powiadomienia e-mail i elementu webhook dla akcji skalowania. W tym przewodniku przedstawiono przykład konfigurowania tych obiektów przy użyciu szablonu usługi Resource Manager dla zestawu skalowania maszyny Wirtualnej.

> [!NOTE]
> Gdy w tym przewodniku wyjaśniono powitania dla zestawy skalowania maszyny Wirtualnej, hello te same informacje dotyczą tooautoscaling [usługi w chmurze](https://azure.microsoft.com/services/cloud-services/), i [usługi aplikacji — aplikacje sieci Web](https://azure.microsoft.com/services/app-service/web/).
> Dla prostego skali we/wy ustawienie dla zestawu skalowania maszyny Wirtualnej w oparciu o metryki wydajności prosty przykład procesora CPU, zobacz toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) i [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) dokumentów
>
>

## <a name="walkthrough"></a>Przewodnik
W tym przewodniku używamy [Eksploratora zasobów Azure](https://resources.azure.com/) tooconfigure i zaktualizuj ustawienia skalowania automatycznego powitania dla zestawu skalowania. Eksplorator zasobów platformy Azure jest łatwy sposób toomanage zasobów platformy Azure za pomocą szablonów Resource Manager. W przypadku nowego narzędzia Eksplorator zasobów tooAzure odczytu [to wprowadzenie](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).

1. Wdrożenie nowej skali ustawić przy użyciu ustawienia skalowania automatycznego podstawowe. W tym artykule wykorzystano hello jedną z galerii Szybki Start Azure, który ma systemu Windows hello zestawu przy użyciu szablonu podstawowego skalowania automatycznego skalowania. Skala Linux ustawia hello pracy tak samo.
2. Po utworzeniu zestawu skalowania hello Przejdź zasób zestawu skali toohello z Eksploratora zasobów Azure. Zostanie wyświetlony następujący hello w elemencie Microsoft.Insights węźle.

    ![Eksplorator systemu Azure](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    wykonanie szablonu Hello utworzył domyślnego ustawienia skalowania automatycznego o nazwie hello **"autoscalewad"**. Na prawej stronie powitania można wyświetlić hello pełnej definicji tego ustawienia skalowania automatycznego. W takim przypadku hello domyślne ustawienie skalowania automatycznego zawiera reguły Procesora % na podstawie skalowalnego w poziomie i w skali.  

3. Teraz można dodać więcej profilów i reguły na podstawie harmonogramu hello lub określone wymagania. Utworzymy ustawieniu skalowania automatycznego przy użyciu trzech profilów. Profile toounderstand i zasady automatycznego skalowania, przejrzyj [najlepsze rozwiązania w zakresie skalowania automatycznego](insights-autoscale-best-practices.md).  

    | Profile & reguły | Opis |
    |--- | --- |
    | **Profil** |**Na podstawie wydajności/metryki** |
    | Reguła |Liczba wiadomości w kolejce magistrali usługi > x |
    | Reguła |Liczba wiadomości w kolejce magistrali usługi < y |
    | Reguła |Procent użycia procesora CPU > n |
    | Reguła |Procent użycia procesora CPU < p |
    | **Profil** |**Dzień tygodnia godziny rano (Brak reguł)** |
    | **Profil** |**Dzień uruchamiania produktu (Brak reguł)** |

4. Oto scenariusza skalowania hipotetycznego używamy na potrzeby tego przewodnika.

    * **Na podstawie obciążenia** — Chcę się tooscale out lub w oparte na powitania obciążenie mojej aplikacji hostowanych na mój set.* skali
    * **Rozmiar kolejki wiadomości** -kolejką usługi Service Bus można używać do hello przychodzących komunikatów toomy aplikacji. Liczba wiadomości w kolejce hello i procent użycia procesora CPU i skonfiguruj tootrigger profil domyślny akcji skalowania, jeśli liczba komunikatów lub Procesora trafień hello threshold.*
    * **Czas tydzień i dzień** — Chcę co tydzień cyklicznego profilu "czasu dnia hello", na podstawie o nazwie "Godzin dnia tygodnia rano". Na podstawie danych historycznych, wiadomo, że jest lepsze toohave pewność, że liczba maszyn wirtualnych wystąpień toohandle Moja aplikacja obciążenia podczas tego time.*
    * **Wybranych dat** — po dodaniu profilu produktu uruchamianie dnia. I planowanie określonymi datami tak Moja aplikacja jest gotowy toohandle hello obciążenia powodu anonsów marketing i gdy testujemy nowego produktu hello application.*
    * *ostatnie dwa profile Hello ma także inne metryki na podstawie zasad wydajności w nich. W takim przypadku I uzgodnionych nie toohave, jeden i zamiast tego toorely na powitania metrykę wydajności na podstawie reguł. Reguły są opcjonalne dla profilów hello cyklicznego i oparty na dacie.*

    Aparat skalowania automatycznego priorytetyzacji hello profile i reguł, również zostanie zarejestrowane w hello [najlepsze rozwiązania w zakresie Skalowanie automatyczne](insights-autoscale-best-practices.md) artykułu.
    Listę typowych metryki skalowania automatycznego zawiera [wspólnej metryki automatycznego skalowania](insights-autoscale-common-metrics.md)

5. Upewnij się, że znajdują się na powitania **odczytu/zapisu** trybu w Eksploratorze zasobów

    ![Autoscalewad, ustawienie skalowania automatycznego domyślne](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. Kliknij przycisk Edytuj. **Zastąp** element profile"hello" w ustawieniu skalowania automatycznego z hello następującej konfiguracji:

    ![Profile](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    Obsługiwane pól i ich wartości, zobacz [dokumentacja interfejsu API REST skalowania automatycznego](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx). Teraz ustawienia skalowania automatycznego zawiera trzy profile hello wyjaśniono wcześniej.

7. Na koniec przyjrzeć się hello skalowania automatycznego **powiadomień** sekcji. Powiadomienia skalowania automatycznego pozwalają toodo trzy czynności podczas skalowania w poziomie lub w akcji pomyślnie zostanie wywołany.
   - Powiadom Witaj, Administratorze i współadministratorzy subskrypcji
   - Wyślij wiadomość e-mail zbioru użytkowników
   - Wyzwala wywołanie elementu webhook. Po, ten element webhook wysyła metadane dotyczące hello Skalowanie automatyczne warunku i zestawu skalowania hello zasobów. toolearn więcej informacji o ładunku hello webhook skalowania automatycznego, zobacz [skonfigurować elementu Webhook & powiadomienia E-mail dotyczące skalowania automatycznego](insights-autoscale-to-webhook-email.md).

   Dodaj powitania po zastępuje ustawienie skalowania automatycznego toohello Twojego **powiadomień** elementu, którego wartość ma wartość null

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   Trafienia **Put** przycisk w ustawieniu skalowania automatycznego hello tooupdate Eksploratora zasobów.

Zaktualizowano skalowania automatycznego ustawienie wiele profilów skalowania tooinclude zestaw skalowania maszyny Wirtualnej i skalować powiadomienia.

## <a name="next-steps"></a>Następne kroki
Użyj tych toolearn łącza więcej informacji na temat Skalowanie automatyczne.

[Rozwiązywanie problemów z automatycznie skalowana za pomocą zestawów skali maszyny wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[Typowe metryki automatycznego skalowania](insights-autoscale-common-metrics.md)

[Najlepsze rozwiązania dotyczące usługi Azure skalowania automatycznego](insights-autoscale-best-practices.md)

[Zarządzaj skalowania automatycznego przy użyciu programu PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[Zarządzaj skalowania automatycznego przy użyciu interfejsu wiersza polecenia](insights-cli-samples.md#autoscale)

[Konfigurowanie elementu Webhook & powiadomienia E-mail dotyczące skalowania automatycznego](insights-autoscale-to-webhook-email.md)
