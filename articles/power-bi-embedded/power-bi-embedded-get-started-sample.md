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
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="acb69-103">Rozpoczęcie pracy z przykładem Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="acb69-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="acb69-104">Z **Microsoft Power BI Embedded**, można zintegrować raportów usługi Power BI bezpośrednio z sieci web lub aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="acb69-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="acb69-105">W tym artykule, firma Microsoft będzie przedstawiono toohello **Power BI Embedded** próbki uruchomiono get.</span><span class="sxs-lookup"><span data-stu-id="acb69-105">In this article, we'll introduce you toohello **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="acb69-106">Przed rozszerzana wszelkie dodatkowe, prawdopodobnie należy hello toosave następujące zasoby.</span><span class="sxs-lookup"><span data-stu-id="acb69-106">Before we go any further, you'll probably want toosave hello following resources.</span></span> <span data-ttu-id="acb69-107">Będzie pomagają składników podczas integrowania raportów usługi Power BI za hello przykładową aplikację i własnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="acb69-107">They'll help you when integrating Power BI reports into hello sample app and your own apps too.</span></span>

* [<span data-ttu-id="acb69-108">Przykładową aplikację sieci web dla obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="acb69-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="acb69-109">Power BI Embedded API reference</span><span class="sxs-lookup"><span data-stu-id="acb69-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="acb69-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (dostępnych za pośrednictwem pakietu NuGet)</span><span class="sxs-lookup"><span data-stu-id="acb69-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="acb69-111">Przykładowe osadzić raport JavaScript</span><span class="sxs-lookup"><span data-stu-id="acb69-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="acb69-112">Zanim można skonfigurować i wykonywania hello Power BI Embedded uzyskać uruchomiona próbki, należy toocreate co najmniej jeden **kolekcji obszarów roboczych** w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="acb69-112">Before you can configure and run hello Power BI Embedded get started sample, you need toocreate at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="acb69-113">toolearn jak toocreate **kolekcji obszarów roboczych** hello Azure Portal zawiera [wprowadzenie do programu Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="acb69-113">toolearn how toocreate a **Workspace Collection** in hello Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-hello-sample-app"></a><span data-ttu-id="acb69-114">Skonfiguruj hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="acb69-114">Configure hello sample app</span></span>

<span data-ttu-id="acb69-115">Przejdźmy przy konfigurowaniu aplikacja programu Visual Studio programowanie środowiska tooaccess hello składniki wymagane toorun hello próbki.</span><span class="sxs-lookup"><span data-stu-id="acb69-115">Let's walk through setting up your Visual Studio development environment tooaccess hello  components needed toorun hello sample app.</span></span>

1. <span data-ttu-id="acb69-116">Pobierz i Rozpakuj hello [Power BI Embedded — integracji raportu w aplikacji sieci web](http://go.microsoft.com/fwlink/?LinkId=761493) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="acb69-116">Download and unzip hello [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="acb69-117">Otwórz **PowerBI embedded.sln** w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="acb69-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="acb69-118">Może być konieczne tooexecute hello **pakiet aktualizacji** w hello konsoli Menedżera pakietów NuGET w pakietach hello tooupdate kolejności używane w tym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="acb69-118">You may need tooexecute hello **Update-Package** command in hello NuGET Package Manager Console in order tooupdate hello packages used in this solution.</span></span>
3. <span data-ttu-id="acb69-119">Utworzenie rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="acb69-119">Build hello solution.</span></span>
4. <span data-ttu-id="acb69-120">Uruchom hello **ProvisionSample** aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="acb69-120">Run hello **ProvisionSample** console app.</span></span> <span data-ttu-id="acb69-121">Hello przykładowej aplikacji konsoli służy do obsługi administracyjnej obszaru roboczego i importowanie pliku PBIX.</span><span class="sxs-lookup"><span data-stu-id="acb69-121">In hello sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="acb69-122">tooprovision nowy **obszaru roboczego**, wybierz opcję 1, **zarządzania kolekcji**, a następnie wybierz opcję 6, **udostępnić nowy obszar roboczy**</span><span class="sxs-lookup"><span data-stu-id="acb69-122">tooprovision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="acb69-123">tooimport nowy **raport**, wybierz opcję 2, **raport zarządzania**, a następnie wybierz opcję 3, **pulpitu PBIX importu pliku do obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="acb69-123">tooimport a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="acb69-124">Wprowadź użytkownika **kolekcji obszarów roboczych** nazwa, i **klucz dostępu**.</span><span class="sxs-lookup"><span data-stu-id="acb69-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="acb69-125">Można uzyskać w hello **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="acb69-125">You can get these in hello **Azure Portal**.</span></span> <span data-ttu-id="acb69-126">więcej informacji na temat toolearn tooget z **klucz dostępu**, zobacz [kluczy dostępu interfejsu API widoku Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) w wprowadzenie do programu Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="acb69-126">toolearn more about how tooget your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="acb69-127">Skopiuj i Zapisz hello nowo utworzony **identyfikator obszaru roboczego** toouse w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="acb69-127">Copy and save hello newly created **Workspace ID** toouse later in this article.</span></span> <span data-ttu-id="acb69-128">Po hello **identyfikator obszaru roboczego** jest utworzony, można go znaleźć hello **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="acb69-128">After hello **Workspace ID** is created, you can find it hello **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="acb69-129">plików PBIX tooimport do Twojej **obszaru roboczego**, wybierz opcję **6. Importowanie pliku PBIX pulpitu do istniejący obszar roboczy**.</span><span class="sxs-lookup"><span data-stu-id="acb69-129">tooimport a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="acb69-130">Jeśli nie masz PBIX pliku przydatną, możesz pobrać hello [Retail Analysis próbki PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="acb69-130">If you don't have a PBIX file handy, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="acb69-131">Jeśli zostanie wyświetlony monit, wprowadź przyjazną nazwę dla Twojego **zestawu danych**.</span><span class="sxs-lookup"><span data-stu-id="acb69-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="acb69-132">Powinna zostać wyświetlona odpowiedź, takich jak:</span><span class="sxs-lookup"><span data-stu-id="acb69-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="acb69-133">Jeśli plik PBIX zawiera wszystkie połączenia zapytania bezpośredniego, należy uruchomić parametry połączenia hello 7 tooupdate opcji.</span><span class="sxs-lookup"><span data-stu-id="acb69-133">If your PBIX file contains any direct query connections, run option 7 tooupdate hello connection strings.</span></span>

<span data-ttu-id="acb69-134">W tym momencie masz raport programu Power BI PBIX zaimportowane do programu **obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="acb69-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="acb69-135">Teraz Przyjrzyjmy się jak toorun hello **Power BI Embedded** Pobierz wprowadzenie przykładową aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="acb69-135">Now, let's look at how toorun hello **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-hello-sample-web-app"></a><span data-ttu-id="acb69-136">Uruchom hello przykładową aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="acb69-136">Run hello sample web app</span></span>
<span data-ttu-id="acb69-137">przykład aplikacji sieci web Hello jest przykładowej aplikacji, która renderuje raporty zaimportowane do programu **obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="acb69-137">hello web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="acb69-138">Oto, jak tooconfigure hello przykładowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="acb69-138">Here's how tooconfigure hello web app sample.</span></span>

1. <span data-ttu-id="acb69-139">W hello **osadzonych PowerBI** prawo rozwiązania Visual Studio kliknij hello **EmbedSample** aplikacji sieci web, a następnie wybierz pozycję **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="acb69-139">In hello **PowerBI-embedded** Visual Studio solution, right click hello **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="acb69-140">W **web.config**, w hello **EmbedSample** aplikacji sieci web, Edytuj hello **appSettings**: **AccessKey**,  **WorkspaceCollection** nazwa, i **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="acb69-140">In **web.config**, in hello **EmbedSample** web application, edit hello **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="acb69-141">Uruchom hello **EmbedSample** aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="acb69-141">Run hello **EmbedSample** web application.</span></span>

<span data-ttu-id="acb69-142">Po uruchomieniu hello **EmbedSample** aplikacji sieci web powinna zawierać panelu nawigacji po lewej stronie powitania **raporty** menu.</span><span class="sxs-lookup"><span data-stu-id="acb69-142">Once you run hello **EmbedSample** web application, hello left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="acb69-143">Raport hello tooview zaimportowane, rozwiń węzeł **raporty**i kliknij przycisk raport.</span><span class="sxs-lookup"><span data-stu-id="acb69-143">tooview hello report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="acb69-144">Jeśli importowany hello [Retail Analysis próbki PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello przykładową aplikację sieci web będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="acb69-144">If you imported hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="acb69-145">Kliknij przycisk raport, hello **EmbedSample** aplikacji sieci web powinien wyglądać to:</span><span class="sxs-lookup"><span data-stu-id="acb69-145">After you click a report, hello **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a><span data-ttu-id="acb69-146">Eksploruj hello przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="acb69-146">Explore hello sample code</span></span>

<span data-ttu-id="acb69-147">Witaj **Microsoft Power BI Embedded** próbka jest przykładową aplikację sieci web przedstawiająca sposób toointegrate **usługi Power BI** raportów w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="acb69-147">hello **Microsoft Power BI Embedded** sample is an example web app that shows you how toointegrate **Power BI** reports into your app.</span></span> <span data-ttu-id="acb69-148">Używa Model-widok-kontroler (MVC) toodemonstrate wzorzec — najlepsze praktyki projektowania.</span><span class="sxs-lookup"><span data-stu-id="acb69-148">It uses a Model-View-Controller (MVC) design pattern toodemonstrate best practices.</span></span> <span data-ttu-id="acb69-149">W tej sekcji opisano części hello przykładowy kod, który można sprawdzić w hello **osadzonych usługi Power BI** rozwiązania aplikacji w sieci web.</span><span class="sxs-lookup"><span data-stu-id="acb69-149">This section highlights parts of hello sample code that you can explore within hello **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="acb69-150">Witaj wzorca Model-widok-kontroler (MVC) oddziela modelowania hello hello domeny, hello prezentacji i akcji hello w oparciu o dane wejściowe użytkownika do trzech osobnych klas: Model, widok i kontroli.</span><span class="sxs-lookup"><span data-stu-id="acb69-150">hello Model-View-Controller (MVC) pattern separates hello modeling of hello domain, hello presentation, and hello actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="acb69-151">toolearn więcej informacji o nazwie wzorca MVC, zobacz [Dowiedz się więcej o ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="acb69-151">toolearn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="acb69-152">Witaj **Microsoft Power BI Embedded** przykładowy kod jest oddzielona w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="acb69-152">hello **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="acb69-153">Każda sekcja zawiera nazwy pliku hello w hello rozwiązania embedded.sln usługi Power BI, aby mógł łatwo znaleźć kod hello w przykładowym hello.</span><span class="sxs-lookup"><span data-stu-id="acb69-153">Each section includes hello file name in hello PowerBI-embedded.sln solution so that you can easily find hello code in hello sample.</span></span>

> [!NOTE]
> <span data-ttu-id="acb69-154">W tej sekcji znajduje się podsumowanie hello przykładowy kod, który pokazuje, jak kod hello został zapisany.</span><span class="sxs-lookup"><span data-stu-id="acb69-154">This section is a summary of hello sample code that shows how hello code was written.</span></span> <span data-ttu-id="acb69-155">tooview hello kompletne przykładowe, załaduj rozwiązania hello embedded.sln usługi Power BI w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="acb69-155">tooview hello complete sample, please load hello PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="acb69-156">Model</span><span class="sxs-lookup"><span data-stu-id="acb69-156">Model</span></span>

<span data-ttu-id="acb69-157">przykład Witaj ma **ReportsViewModel** i **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="acb69-157">hello sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="acb69-158">**ReportsViewModel.cs**: reprezentuje raportami programu Power BI.</span><span class="sxs-lookup"><span data-stu-id="acb69-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="acb69-159">**ReportViewModel.cs**: reprezentuje raportu Power BI.</span><span class="sxs-lookup"><span data-stu-id="acb69-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="acb69-160">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="acb69-160">Connection string</span></span>

<span data-ttu-id="acb69-161">Parametry połączenia Hello należy hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="acb69-161">hello connection string must be in hello following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="acb69-162">Za pomocą serwera i bazy danych takie same atrybuty wspólne zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="acb69-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="acb69-163">Na przykład: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="acb69-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="acb69-164">Widok</span><span class="sxs-lookup"><span data-stu-id="acb69-164">View</span></span>

<span data-ttu-id="acb69-165">Witaj **widoku** zarządza wyświetlania hello usługi Power BI **raporty** i usługi Power BI **raport**.</span><span class="sxs-lookup"><span data-stu-id="acb69-165">hello **View** manages hello display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="acb69-166">**Reports.cshtml**: iteracja **Model.Reports** toocreate **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="acb69-166">**Reports.cshtml**: Iterate over **Model.Reports** toocreate an **ActionLink**.</span></span> <span data-ttu-id="acb69-167">Witaj **ActionLink** składa się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="acb69-167">hello **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="acb69-168">Część</span><span class="sxs-lookup"><span data-stu-id="acb69-168">Part</span></span> | <span data-ttu-id="acb69-169">Opis</span><span class="sxs-lookup"><span data-stu-id="acb69-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="acb69-170">Tytuł</span><span class="sxs-lookup"><span data-stu-id="acb69-170">Title</span></span> |<span data-ttu-id="acb69-171">Nazwa hello raportu.</span><span class="sxs-lookup"><span data-stu-id="acb69-171">Name of hello Report.</span></span> |
| <span data-ttu-id="acb69-172">Ciąg zapytania</span><span class="sxs-lookup"><span data-stu-id="acb69-172">QueryString</span></span> |<span data-ttu-id="acb69-173">Łącze toohello identyfikator raportu.</span><span class="sxs-lookup"><span data-stu-id="acb69-173">A link toohello Report ID.</span></span> |

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

<span data-ttu-id="acb69-174">Report.cshtml: Ustaw hello **Model.AccessToken**, i hello wyrażenie Lambda **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="acb69-174">Report.cshtml: Set hello **Model.AccessToken**, and hello Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="acb69-175">Kontrolera</span><span class="sxs-lookup"><span data-stu-id="acb69-175">Controller</span></span>

<span data-ttu-id="acb69-176">**DashboardController.cs**: tworzy przekazywanie PowerBIClient **tokenu aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="acb69-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="acb69-177">JSON tokenów sieci Web (JWT) są generowane na podstawie hello **klucza podpisywania** tooget hello **poświadczenia**.</span><span class="sxs-lookup"><span data-stu-id="acb69-177">A JSON Web Token (JWT) is generated from hello **Signing Key** tooget hello **Credentials**.</span></span> <span data-ttu-id="acb69-178">Witaj **poświadczenia** są używane toocreate wystąpienia **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="acb69-178">hello **Credentials** are used toocreate an instance of **PowerBIClient**.</span></span> <span data-ttu-id="acb69-179">Po utworzeniu wystąpienia **PowerBIClient**, można wywołać GetReports() i GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="acb69-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="acb69-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="acb69-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="acb69-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="acb69-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="acb69-182">Zadanie<ActionResult> raportu (ciąg reportId)</span><span class="sxs-lookup"><span data-stu-id="acb69-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="acb69-183">Integracji raportu w swojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="acb69-183">Integrate a report into your app</span></span>

<span data-ttu-id="acb69-184">Po utworzeniu **raport**, możesz użyć **IFrame** tooembed hello usługi Power BI **raport**.</span><span class="sxs-lookup"><span data-stu-id="acb69-184">Once you have a **Report**, you use an **IFrame** tooembed hello Power BI **Report**.</span></span> <span data-ttu-id="acb69-185">Oto fragment kodu z powerbi.js w hello **Microsoft Power BI Embedded** próbki.</span><span class="sxs-lookup"><span data-stu-id="acb69-185">Here is a code snippet from  powerbi.js in hello **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="acb69-186">Raporty filtru osadzonego w aplikacji</span><span class="sxs-lookup"><span data-stu-id="acb69-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="acb69-187">Osadzony raport można filtrować przy użyciu składni adresu URL.</span><span class="sxs-lookup"><span data-stu-id="acb69-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="acb69-188">toodo, możesz dodać **$filter** parametr ciągu zapytania o **eq** url źródła iFrame tooyour operatora z filtrem hello.</span><span class="sxs-lookup"><span data-stu-id="acb69-188">toodo this, you add a **$filter** query string parameter with an **eq** operator tooyour iFrame src url with hello filter specified.</span></span> <span data-ttu-id="acb69-189">Oto składnia zapytania filtru hello:</span><span class="sxs-lookup"><span data-stu-id="acb69-189">Here is hello filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="acb69-190">{tableName/fieldName} nie może zawierać spacji ani znaków specjalnych.</span><span class="sxs-lookup"><span data-stu-id="acb69-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="acb69-191">Witaj {fieldValue} akceptuje pojedyncze wartości kategorii.</span><span class="sxs-lookup"><span data-stu-id="acb69-191">hello {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="acb69-192">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="acb69-192">See also</span></span>

[<span data-ttu-id="acb69-193">Typowe scenariusze Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="acb69-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="acb69-194">Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="acb69-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
<span data-ttu-id="acb69-195">[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)</span><span class="sxs-lookup"><span data-stu-id="acb69-195">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="acb69-196">Tworzenie nowego raportu przy użyciu zestawu danych</span><span class="sxs-lookup"><span data-stu-id="acb69-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="acb69-197">Program Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="acb69-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="acb69-198">Przykład osadzania skryptu JavaScript</span><span class="sxs-lookup"><span data-stu-id="acb69-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="acb69-199">Masz więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="acb69-199">More questions?</span></span> [<span data-ttu-id="acb69-200">Spróbuj hello Power BI społeczności</span><span class="sxs-lookup"><span data-stu-id="acb69-200">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
