---
title: "aaaCreate alerty dla usług Azure - CLI wieloplatformowych | Dokumentacja firmy Microsoft"
description: "Gdy są spełnione warunki hello wyzwolenia wiadomości e-mail, powiadomienia, adresy URL witryny sieci Web wywołania (elementy webhook) lub automatyzacji."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Tworzenie metryki alertów w monitorze Azure dla usług Azure - CLI między platformami
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [Program PowerShell](insights-alerts-powershell.md)
> * [Interfejs wiersza polecenia](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Omówienie
W tym artykule opisano, jak tooset Azure metryki alerty za pomocą hello wieloplatformowych interfejsu wiersza polecenia (CLI).

> [!NOTE]
> Azure Monitor jest nową nazwę hello proponowaną "Azure Insights" do 25 września 2016 r. Jednak hello przestrzeni nazw, dlatego poniższe polecenia hello nadal zawierać hello "insights".
>
>

Możesz otrzymywać alertu na podstawie metryki monitorowania lub zdarzenia na usługami Azure.

* **Wartości metryki** — Witaj alertu wyzwalacze, jeśli wartość hello określonej metryki przecina próg przypisać w żadnym kierunku. Oznacza to, że oba wyzwala kiedy najpierw zostanie spełniony warunek hello i następnie później podczas warunku jest już spełniane.    
* **Zdarzenia dziennika aktywności** — alert może wyzwolić na *co* zdarzenia lub tylko wtedy, gdy występuje określone zdarzenia. więcej informacji na temat alertów dotyczących działań w dzienniku toolearn [kliknij tutaj](monitoring-activity-log-alerts.md)

Można skonfigurować hello metryki toodo alertów po, wyzwala:

* Wyślij administratora usługi toohello powiadomienia e-mail i współadministratorzy
* Wyślij wiadomość e-mail tooadditional wiadomości e-mail, które określisz.
* Wywołanie elementu webhook
* Uruchamia wykonywanie elementów runbook platformy Azure (tylko z portalu Azure w tej chwili hello)

Można skonfigurować i uzyskać informacje na temat metryki reguły alertów za pomocą

* [Witryna Azure Portal](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [Interfejs wiersza polecenia (CLI)](insights-alerts-command-line-interface.md)
* [Interfejs API REST Azure monitora](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Zawsze może odbierać pomocy dla poleceń, wpisując polecenie i odkładanie — pomoc na końcu hello. Na przykład:

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>Tworzyć reguły alertów za pomocą hello interfejsu wiersza polecenia
1. Wykonaj hello warunki wstępne i tooAzure logowania. Zobacz [przykłady interfejsu wiersza polecenia Azure Monitor](insights-cli-samples.md). Krótko mówiąc Zainstaluj hello interfejsu wiersza polecenia i uruchom następujące polecenia. One się zalogować, Pokaż subskrypcję, a przygotowanie toorun poleceń Azure monitora.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. toolist istniejących reguł dla grupy zasobów, użyj powitania po formularza **insights azure alerty reguły listy** *[opcje] &lt;grupa zasobów&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. toocreate regułę, należy toohave kilku ważnych informacji najpierw.
  * Witaj **identyfikator zasobu** hello zasobu ma tooset alert dla
  * Witaj **definicji metryk** dostępne dla tego zasobu

     Jednym ze sposobów tooget hello identyfikator zasobu jest hello toouse portalu Azure. Zakładając, że zasób hello został już utworzony, wybierz go w portalu hello. Następnie w bloku dalej hello, wybierz *właściwości* w obszarze hello *ustawienia* sekcji. Witaj *identyfikator ZASOBU* jest polem w następnym bloku hello. Innym sposobem jest toouse hello [Eksploratora zasobów Azure](https://resources.azure.com/).

     Identyfikator zasobu przykład dla aplikacji sieci web jest

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     tooget listę hello dostępne metryki i jednostki dla tych metryki, np. hello poprzedniego zasobu hello Użyj następującego polecenia interfejsu wiersza polecenia:  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* jest hello szczegółowości miary dostępne hello (1-minutowy). Przy użyciu różnych szczegółowości zapewnia różne opcje metryki.
4. toocreate metryki na podstawie reguły alertu, polecenie hello następującej postaci:

    **Azure insights metryki zestaw reguł alertów** *[opcje] &lt;ruleName&gt; &lt;lokalizacji&gt; &lt;resourceGroup&gt; &lt;Rozmiar_okna&gt; &lt;operator&gt; &lt;próg&gt; &lt;element targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*

    powitania po przykład konfiguruje alert o zasobów witryny sieci web. Wyzwalacze alertu Hello zawsze, gdy odbierze spójnie cały ruch do 5 minut i ponownie po otrzymaniu żaden ruch na 5 minut.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. toocreate elementu webhook lub Wyślij wiadomość e-mail po zgłoszeniu alertu metryki, najpierw utwórz hello poczty e-mail i/lub elementów webhook. Od razu utworzyć regułę hello później. Nie można skojarzyć elementu webhook lub wiadomości e-mail przy użyciu już utworzone przy użyciu interfejsu wiersza polecenia hello reguły.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. Aby sprawdzić, czy alerty zostały utworzone prawidłowo analizując poszczególnych reguł.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. reguły toodelete polecenie hello formularza:

    **szczegółowe informacje, Usuń regułę alertów** [opcje] &lt;resourceGroup&gt; &lt;ruleName&gt;

    Te polecenia usuwania reguł hello utworzony wcześniej w tym artykule.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>Następne kroki
* [Omówienie monitorowania Azure](monitoring-overview.md) tym hello typy informacji, można zbierać i monitorowania.
* Dowiedz się więcej o [konfigurowaniu elementów webhook w alertach](insights-webhooks-alerts.md).
* Dowiedz się więcej o [konfigurowania alertów na zdarzenia dziennika aktywności](monitoring-activity-log-alerts.md).
* Dowiedz się więcej o [elementów Runbook automatyzacji Azure](../automation/automation-starting-a-runbook.md).
* Pobierz [omówienie zbierania dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md) toocollect szczegółowe metryki wysokiej częstotliwości w usłudze.
* Pobierz [omówienie zbierania metryk](insights-how-to-customize-monitoring.md) toomake się, że usługa jest dostępna i elastyczny.
