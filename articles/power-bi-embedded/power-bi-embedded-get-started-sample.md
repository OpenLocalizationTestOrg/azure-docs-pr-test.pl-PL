---
title: "aaaGet pracę z przykładowym"
description: "Power BI Embedded, należy użyć zestawu SDK tooadd interakcyjne usługi Power BI raportów do aplikacji analizy biznesowej"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a>Rozpoczęcie pracy z przykładem Power BI Embedded

Z **Microsoft Power BI Embedded**, można zintegrować raportów usługi Power BI bezpośrednio z sieci web lub aplikacji dla urządzeń przenośnych. W tym artykule, firma Microsoft będzie przedstawiono toohello **Power BI Embedded** próbki uruchomiono get.

Przed rozszerzana wszelkie dodatkowe, prawdopodobnie należy hello toosave następujące zasoby. Będzie pomagają składników podczas integrowania raportów usługi Power BI za hello przykładową aplikację i własnych aplikacji.

* [Przykładową aplikację sieci web dla obszaru roboczego](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Power BI Embedded API reference](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (dostępnych za pośrednictwem pakietu NuGet)
* [Przykładowe osadzić raport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> Zanim można skonfigurować i wykonywania hello Power BI Embedded uzyskać uruchomiona próbki, należy toocreate co najmniej jeden **kolekcji obszarów roboczych** w Twojej subskrypcji platformy Azure. toolearn jak toocreate **kolekcji obszarów roboczych** hello Azure Portal zawiera [wprowadzenie do programu Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="configure-hello-sample-app"></a>Skonfiguruj hello przykładowej aplikacji

Przejdźmy przy konfigurowaniu aplikacja programu Visual Studio programowanie środowiska tooaccess hello składniki wymagane toorun hello próbki.

1. Pobierz i Rozpakuj hello [Power BI Embedded — integracji raportu w aplikacji sieci web](http://go.microsoft.com/fwlink/?LinkId=761493) w witrynie GitHub.
2. Otwórz **PowerBI embedded.sln** w programie Visual Studio. Może być konieczne tooexecute hello **pakiet aktualizacji** w hello konsoli Menedżera pakietów NuGET w pakietach hello tooupdate kolejności używane w tym rozwiązaniu.
3. Utworzenie rozwiązania hello.
4. Uruchom hello **ProvisionSample** aplikacji konsoli. Hello przykładowej aplikacji konsoli służy do obsługi administracyjnej obszaru roboczego i importowanie pliku PBIX.
5. tooprovision nowy **obszaru roboczego**, wybierz opcję 1, **zarządzania kolekcji**, a następnie wybierz opcję 6, **udostępnić nowy obszar roboczy**
6. tooimport nowy **raport**, wybierz opcję 2, **raport zarządzania**, a następnie wybierz opcję 3, **pulpitu PBIX importu pliku do obszaru roboczego**.

7. Wprowadź użytkownika **kolekcji obszarów roboczych** nazwa, i **klucz dostępu**. Można uzyskać w hello **Azure Portal**. więcej informacji na temat toolearn tooget z **klucz dostępu**, zobacz [kluczy dostępu interfejsu API widoku Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) w wprowadzenie do programu Microsoft Power BI Embedded.

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. Skopiuj i Zapisz hello nowo utworzony **identyfikator obszaru roboczego** toouse w dalszej części tego artykułu. Po hello **identyfikator obszaru roboczego** jest utworzony, można go znaleźć hello **Azure Portal**.

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. plików PBIX tooimport do Twojej **obszaru roboczego**, wybierz opcję **6. Importowanie pliku PBIX pulpitu do istniejący obszar roboczy**. Jeśli nie masz PBIX pliku przydatną, możesz pobrać hello [Retail Analysis próbki PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).
10. Jeśli zostanie wyświetlony monit, wprowadź przyjazną nazwę dla Twojego **zestawu danych**.

Powinna zostać wyświetlona odpowiedź, takich jak:

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> Jeśli plik PBIX zawiera wszystkie połączenia zapytania bezpośredniego, należy uruchomić parametry połączenia hello 7 tooupdate opcji.

W tym momencie masz raport programu Power BI PBIX zaimportowane do programu **obszaru roboczego**. Teraz Przyjrzyjmy się jak toorun hello **Power BI Embedded** Pobierz wprowadzenie przykładową aplikację sieci web.

## <a name="run-hello-sample-web-app"></a>Uruchom hello przykładową aplikację sieci web
przykład aplikacji sieci web Hello jest przykładowej aplikacji, która renderuje raporty zaimportowane do programu **obszaru roboczego**. Oto, jak tooconfigure hello przykładowej aplikacji sieci web.

1. W hello **osadzonych PowerBI** prawo rozwiązania Visual Studio kliknij hello **EmbedSample** aplikacji sieci web, a następnie wybierz pozycję **Ustaw jako projekt startowy**.
2. W **web.config**, w hello **EmbedSample** aplikacji sieci web, Edytuj hello **appSettings**: **AccessKey**,  **WorkspaceCollection** nazwa, i **WorkspaceId**.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Uruchom hello **EmbedSample** aplikacji sieci web.

Po uruchomieniu hello **EmbedSample** aplikacji sieci web powinna zawierać panelu nawigacji po lewej stronie powitania **raporty** menu. Raport hello tooview zaimportowane, rozwiń węzeł **raporty**i kliknij przycisk raport. Jeśli importowany hello [Retail Analysis próbki PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello przykładową aplikację sieci web będzie wyglądać następująco:

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

Kliknij przycisk raport, hello **EmbedSample** aplikacji sieci web powinien wyglądać to:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a>Eksploruj hello przykładowy kod

Witaj **Microsoft Power BI Embedded** próbka jest przykładową aplikację sieci web przedstawiająca sposób toointegrate **usługi Power BI** raportów w aplikacji. Używa Model-widok-kontroler (MVC) toodemonstrate wzorzec — najlepsze praktyki projektowania. W tej sekcji opisano części hello przykładowy kod, który można sprawdzić w hello **osadzonych usługi Power BI** rozwiązania aplikacji w sieci web. Witaj wzorca Model-widok-kontroler (MVC) oddziela modelowania hello hello domeny, hello prezentacji i akcji hello w oparciu o dane wejściowe użytkownika do trzech osobnych klas: Model, widok i kontroli. toolearn więcej informacji o nazwie wzorca MVC, zobacz [Dowiedz się więcej o ASP.NET](http://www.asp.net/mvc).

Witaj **Microsoft Power BI Embedded** przykładowy kod jest oddzielona w następujący sposób. Każda sekcja zawiera nazwy pliku hello w hello rozwiązania embedded.sln usługi Power BI, aby mógł łatwo znaleźć kod hello w przykładowym hello.

> [!NOTE]
> W tej sekcji znajduje się podsumowanie hello przykładowy kod, który pokazuje, jak kod hello został zapisany. tooview hello kompletne przykładowe, załaduj rozwiązania hello embedded.sln usługi Power BI w programie Visual Studio.

### <a name="model"></a>Model

przykład Witaj ma **ReportsViewModel** i **ReportViewModel**.

**ReportsViewModel.cs**: reprezentuje raportami programu Power BI.

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

**ReportViewModel.cs**: reprezentuje raportu Power BI.

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a>Parametry połączenia

Parametry połączenia Hello należy hello następującego formatu:

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

Za pomocą serwera i bazy danych takie same atrybuty wspólne zakończy się niepowodzeniem. Na przykład: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>Widok

Witaj **widoku** zarządza wyświetlania hello usługi Power BI **raporty** i usługi Power BI **raport**.

**Reports.cshtml**: iteracja **Model.Reports** toocreate **ActionLink**. Witaj **ActionLink** składa się w następujący sposób:

| Część | Opis |
| --- | --- |
| Tytuł |Nazwa hello raportu. |
| Ciąg zapytania |Łącze toohello identyfikator raportu. |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

Report.cshtml: Ustaw hello **Model.AccessToken**, i hello wyrażenie Lambda **PowerBIReportFor**.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Kontrolera

**DashboardController.cs**: tworzy przekazywanie PowerBIClient **tokenu aplikacji**. JSON tokenów sieci Web (JWT) są generowane na podstawie hello **klucza podpisywania** tooget hello **poświadczenia**. Witaj **poświadczenia** są używane toocreate wystąpienia **PowerBIClient**. Po utworzeniu wystąpienia **PowerBIClient**, można wywołać GetReports() i GetReportsAsync().

CreatePowerBIClient()

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

ActionResult Reports()

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


Zadanie<ActionResult> raportu (ciąg reportId)

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a>Integracji raportu w swojej aplikacji

Po utworzeniu **raport**, możesz użyć **IFrame** tooembed hello usługi Power BI **raport**. Oto fragment kodu z powerbi.js w hello **Microsoft Power BI Embedded** próbki.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>Raporty filtru osadzonego w aplikacji

Osadzony raport można filtrować przy użyciu składni adresu URL. toodo, możesz dodać **$filter** parametr ciągu zapytania o **eq** url źródła iFrame tooyour operatora z filtrem hello. Oto składnia zapytania filtru hello:

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName} nie może zawierać spacji ani znaków specjalnych. Witaj {fieldValue} akceptuje pojedyncze wartości kategorii.  

## <a name="see-also"></a>Zobacz też

[Typowe scenariusze Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)  
[Tworzenie nowego raportu przy użyciu zestawu danych](power-bi-embedded-create-report-from-dataset.md)  
[Program Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Przykład osadzania skryptu JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)
