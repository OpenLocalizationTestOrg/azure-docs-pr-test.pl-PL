---
title: wprowadzenie do programu Microsoft Power BI Embedded aaaGet
description: "Usługa Power BI Embedded — dodawanie interaktywnych raportów usługi Power BI do aplikacji analizy biznesowej"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="5db51-103">Wprowadzenie do usługi Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="5db51-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="5db51-104">**Power BI Embedded** jest usługą platformy Azure z tym tooadd deweloperzy aplikacji umożliwia raporty interakcyjne usługi Power BI do własnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5db51-104">**Power BI Embedded** is an Azure service that enables application developers tooadd interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="5db51-105">**Power BI Embedded** Zaloguj współpracuje z istniejącymi aplikacjami bez konieczności one lub zmiana hello użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5db51-105">**Power BI Embedded** works with existing applications without needing redesign or changing hello way users sign in.</span></span>

<span data-ttu-id="5db51-106">Zasoby dla **Microsoft Power BI Embedded** za pośrednictwem hello [API Azure ARM](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="5db51-106">Resources for **Microsoft Power BI Embedded** are provisioned through hello [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="5db51-107">W tym przypadku jest udostępnianie zasobów hello **kolekcji obszarów roboczych usługi Power BI**.</span><span class="sxs-lookup"><span data-stu-id="5db51-107">In this case, hello resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="5db51-108">Tworzenie kolekcji obszarów roboczych</span><span class="sxs-lookup"><span data-stu-id="5db51-108">Create a workspace collection</span></span>

<span data-ttu-id="5db51-109">A **kolekcji obszarów roboczych** jest hello najwyższego poziomu zasobem platformy Azure i kontenerem zawartości hello, która zostanie osadzona w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5db51-109">A **Workspace Collection** is hello top-level Azure resource and a container for hello content that will be embedded in your application.</span></span> <span data-ttu-id="5db51-110">**Kolekcję obszarów roboczych** można utworzyć na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="5db51-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="5db51-111">Ręcznie przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5db51-111">Manually using hello Azure Portal</span></span>
* <span data-ttu-id="5db51-112">Programowo przy użyciu hello interfejsów API usługi Azure Resource Manager (ARM)</span><span class="sxs-lookup"><span data-stu-id="5db51-112">Programmatically using hello Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="5db51-113">Przejdźmy hello kroki toobuild **kolekcji obszarów roboczych** przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5db51-113">Let's walk through hello steps toobuild a **Workspace Collection** using hello Azure Portal.</span></span>

1. <span data-ttu-id="5db51-114">Otwórz witrynę **Azure Portal**: [http://portal.azure.com](http://portal.azure.com) i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="5db51-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="5db51-115">Kliknij przycisk **+ nowy** na powitania górnym panelu.</span><span class="sxs-lookup"><span data-stu-id="5db51-115">Click **+ New** on hello top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="5db51-116">W obszarze **Dane i analizy** kliknij opcję **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="5db51-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="5db51-117">Na powitania **bloku kolekcji obszarów roboczych**, wprowadź hello wymagane informacje.</span><span class="sxs-lookup"><span data-stu-id="5db51-117">On hello **Workspace Collection Blade**, enter hello required information.</span></span> <span data-ttu-id="5db51-118">Aby poznać **ceny**, zobacz [Usługa Power BI Embedded — cennik](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="5db51-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="5db51-119">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5db51-119">Click **Create**.</span></span>

<span data-ttu-id="5db51-120">Witaj **kolekcji obszarów roboczych** potrwa kilka chwil tooprovision.</span><span class="sxs-lookup"><span data-stu-id="5db51-120">hello **Workspace Collection** will take a few moments tooprovision.</span></span> <span data-ttu-id="5db51-121">Po zakończeniu spowoduje przekierowanie toohello **bloku kolekcji obszarów roboczych**.</span><span class="sxs-lookup"><span data-stu-id="5db51-121">When completed, you'll be taken toohello **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="5db51-122">Witaj **blok tworzenia** informacjami hello należy toocall hello interfejsów API służących do tworzenia obszarów roboczych i wdrażania toothem zawartości.</span><span class="sxs-lookup"><span data-stu-id="5db51-122">hello **Creation Blade** contains hello information you need toocall hello APIs that create workspaces and deploy content toothem.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="5db51-123">Wyświetlanie kluczy dostępu interfejsu API usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="5db51-123">View Power BI API access keys</span></span>

<span data-ttu-id="5db51-124">Jeden z hello najważniejsze elementy toocall informacje potrzebne hello API REST usługi Power BI są hello **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="5db51-124">One of hello most important pieces of information needed toocall hello Power BI REST APIs are hello **Access Keys**.</span></span> <span data-ttu-id="5db51-125">Są one używane toogenerate hello **tokenów aplikacji** , które są używane tooauthenticate żądań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5db51-125">These are used toogenerate hello **app tokens** that are used tooauthenticate your API requests.</span></span> <span data-ttu-id="5db51-126">tooview Twojego **klucze dostępu**, kliknij przycisk **klucze dostępu** na powitania **bloku ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="5db51-126">tooview your **Access Keys**, click **Access Keys** on hello **Settings Blade**.</span></span> <span data-ttu-id="5db51-127">Aby uzyskać więcej informacji o **tokenach aplikacji**, zobacz [Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="5db51-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="5db51-128">Zauważysz, że masz dwa klucze.</span><span class="sxs-lookup"><span data-stu-id="5db51-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="5db51-129">Skopiuj te klucze i przechowuj je bezpiecznie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5db51-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="5db51-130">Jest bardzo ważne, aby traktować te klucze jak hasła, ponieważ będzie zapewniają dostęp do tooall hello zawartości w Twojej **kolekcji obszarów roboczych**.</span><span class="sxs-lookup"><span data-stu-id="5db51-130">It's very important that you treat these keys as you would a password, because they'll provide access tooall hello content in your **Workspace Collection**.</span></span>

<span data-ttu-id="5db51-131">Chociaż wyświetlane są dwa klucze, w określonym czasie potrzebny jest tylko jeden.</span><span class="sxs-lookup"><span data-stu-id="5db51-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="5db51-132">Witaj drugi klucz jest dostarczany, więc można okresowo generować ponownie klucze bez przerywania dostępu toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="5db51-132">hello second key is provided so you can periodically regenerate keys without interrupting access toohello service.</span></span>

<span data-ttu-id="5db51-133">Teraz, gdy masz wystąpienie usługi Power BI dla danej aplikacji oraz **klucze dostępu**, możesz zaimportować raport do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5db51-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="5db51-134">Przed dowiesz się, jak tooimport, a raport, hello następnej sekcji opisano tworzenie tooembed zestawów danych i raportów usługi Power BI do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5db51-134">Before you learn how tooimport a report, hello next section describes creating Power BI datasets and reports tooembed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="5db51-135">Praca z obszarami roboczymi</span><span class="sxs-lookup"><span data-stu-id="5db51-135">Working with workspaces</span></span>

<span data-ttu-id="5db51-136">Po utworzeniu kolekcji obszaru roboczego, konieczne będzie toocreate obszaru roboczego, który będzie zawierać raporty i zestawy danych programu.</span><span class="sxs-lookup"><span data-stu-id="5db51-136">After you have created your workspace collection, you will need toocreate a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="5db51-137">toocreate obszaru roboczego, konieczne będzie toouse hello [interfejsu API REST Worksapce Post](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="5db51-137">toocreate a workspace, you will need toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="5db51-138">Utwórz tooembed zestawów danych i raportów usługi Power BI do aplikacji za pomocą Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="5db51-138">Create Power BI datasets and reports tooembed into an app using Power BI Desktop</span></span>

<span data-ttu-id="5db51-139">Teraz, gdy masz utworzone wystąpienie usługi Power BI dla aplikacji i mieć **klucze dostępu**, konieczne będzie toocreate hello usługi Power BI z zestawów danych i raportów, które mają tooembed.</span><span class="sxs-lookup"><span data-stu-id="5db51-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need toocreate hello Power BI datasets and reports that you want tooembed.</span></span> <span data-ttu-id="5db51-140">Zestawy danych i raporty można tworzyć za pomocą programu **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="5db51-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="5db51-141">Możesz pobrać program [Power BI Desktop za darmo](https://go.microsoft.com/fwlink/?LinkId=521662).</span><span class="sxs-lookup"><span data-stu-id="5db51-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="5db51-142">Lub, tooquickly rozpocząć pracę, możesz pobrać hello [Retail Analysis próbki PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="5db51-142">Or, tooquickly get started, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="5db51-143">więcej informacji na temat toolearn toouse **Power BI Desktop**, zobacz [wprowadzenie Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="5db51-143">toolearn more about how toouse **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="5db51-144">Z **Power BI Desktop**, Połącz źródła danych tooyour importując kopię danych hello do **Power BI Desktop** lub bezpośrednio łącząc toohello danych źródła przy użyciu **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="5db51-144">With **Power BI Desktop**, you connect tooyour data source by importing a copy of hello data into **Power BI Desktop** or connecting directly toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="5db51-145">Poniżej przedstawiono różnice hello przy użyciu **importu** i **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="5db51-145">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="5db51-146">Import</span><span class="sxs-lookup"><span data-stu-id="5db51-146">Import</span></span> | <span data-ttu-id="5db51-147">Tryb DirectQuery</span><span class="sxs-lookup"><span data-stu-id="5db51-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="5db51-148">Tabele, kolumny, *i dane* są importowane lub kopiowane do programu **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="5db51-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="5db51-149">Podczas pracy nad wizualizacjami program **Power BI Desktop** kopii danych hello zapytań.</span><span class="sxs-lookup"><span data-stu-id="5db51-149">As you work with visualizations, **Power BI Desktop** queries a copy of hello data.</span></span> <span data-ttu-id="5db51-150">toosee wszelkie zmiany danych podstawowych toohello wystąpił, należy odświeżyć lub zaimportować pełny bieżący zestaw danych ponownie.</span><span class="sxs-lookup"><span data-stu-id="5db51-150">toosee any changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="5db51-151">Tylko *tabele i kolumny* są importowane lub kopiowane do programu **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="5db51-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="5db51-152">Podczas pracy nad wizualizacjami program **Power BI Desktop** zapytania hello źródła danych, co oznacza zawsze wyświetlana bieżące dane.</span><span class="sxs-lookup"><span data-stu-id="5db51-152">As you work with visualizations, **Power BI Desktop** queries hello underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="5db51-153">Aby uzyskać więcej informacji o źródle danych tooa łączącego zobacz [źródła danych tooa Connect](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="5db51-153">For more about connecting tooa data source, see [Connect tooa data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="5db51-154">Po zapisaniu pracy w programie **Power BI Desktop** tworzony jest plik PBIX.</span><span class="sxs-lookup"><span data-stu-id="5db51-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="5db51-155">Ten plik zawiera raport.</span><span class="sxs-lookup"><span data-stu-id="5db51-155">This file contains your report.</span></span> <span data-ttu-id="5db51-156">Ponadto po zaimportowaniu hello danych plik PBIX zawiera pełen zestaw hello lub jeśli używasz **DirectQuery**, hello plik PBIX zawiera tylko schemat zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="5db51-156">In addition, if you import data hello PBIX contains hello complete dataset, or if you use **DirectQuery**, hello PBIX contains just a dataset schema.</span></span> <span data-ttu-id="5db51-157">Programowe wdrażanie hello PBIX do obszaru roboczego przy użyciu hello [API Import usługi Power BI](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="5db51-157">You programmatically deploy hello PBIX into your workspace using hello [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="5db51-158">**Power BI Embedded** ma dodatkowe interfejsy API toochange powitania serwera i bazy danych, czy zestaw danych wskazuje zestaw tooand poświadczenia konta usługi hello zestawu danych będzie używać tooconnect tooyour w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="5db51-158">**Power BI Embedded** has additional APIs toochange hello server and database that your dataset is pointing tooand set a service account credential that hello dataset will use tooconnect tooyour database.</span></span> <span data-ttu-id="5db51-159">Zobacz artykuły dotyczące operacji [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) i [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span><span class="sxs-lookup"><span data-stu-id="5db51-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="5db51-160">Tworzenie zestawów danych i raportów usługi Power BI za pomocą interfejsów API</span><span class="sxs-lookup"><span data-stu-id="5db51-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="5db51-161">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="5db51-161">Datsets</span></span>

<span data-ttu-id="5db51-162">Można utworzyć zestawy danych w usłudze Power BI Embedded przy użyciu hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="5db51-162">You can create datasets within Power BI Embedded using hello REST API.</span></span> <span data-ttu-id="5db51-163">Następnie można wypchnąć dane do własnego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="5db51-163">You can then push data into your dataset.</span></span> <span data-ttu-id="5db51-164">Dzięki temu toowork z danymi bez konieczności hello programu Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="5db51-164">This allows you toowork with data without hello need of Power BI Desktop.</span></span> <span data-ttu-id="5db51-165">Aby uzyskać więcej informacji, zobacz: [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Wysyłanie zestawów danych za pomocą żądania POST).</span><span class="sxs-lookup"><span data-stu-id="5db51-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="5db51-166">Raporty</span><span class="sxs-lookup"><span data-stu-id="5db51-166">Reports</span></span>

<span data-ttu-id="5db51-167">Można utworzyć raport z zestawu danych bezpośrednio w aplikacji przy użyciu hello JavaScript API.</span><span class="sxs-lookup"><span data-stu-id="5db51-167">You can create a report from a dataset directly in your application using hello JavaScript API.</span></span> <span data-ttu-id="5db51-168">Aby uzyskać więcej informacji, zobacz [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Tworzenie nowego raportu z zestawu danych w usłudze Power BI Embedded).</span><span class="sxs-lookup"><span data-stu-id="5db51-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5db51-169">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5db51-169">See Also</span></span>

[<span data-ttu-id="5db51-170">Rozpoczęcie pracy z przykładem</span><span class="sxs-lookup"><span data-stu-id="5db51-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="5db51-171">Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="5db51-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
<span data-ttu-id="5db51-172">[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)</span><span class="sxs-lookup"><span data-stu-id="5db51-172">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
<span data-ttu-id="5db51-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Tworzenie nowego raportu z zestawu danych w usłudze Power BI Embedded) 
[Save reports](power-bi-embedded-save-reports.md) (Zapisywanie raportów)</span><span class="sxs-lookup"><span data-stu-id="5db51-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="5db51-174">Program Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="5db51-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="5db51-175">Przykład osadzania skryptu JavaScript</span><span class="sxs-lookup"><span data-stu-id="5db51-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="5db51-176">Masz więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="5db51-176">More questions?</span></span> [<span data-ttu-id="5db51-177">Spróbuj hello Power BI społeczności</span><span class="sxs-lookup"><span data-stu-id="5db51-177">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

