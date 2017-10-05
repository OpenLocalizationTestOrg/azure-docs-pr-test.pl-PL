---
title: "Pulpit nawigacyjny, monitora, skalowania, skonfigurować i połączeń hybrydowych w usługi BizTalk Services | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat formantów i monitorowanie wydajności na kartach klasycznym portalu usługi BizTalk Services: pulpitu nawigacyjnego, Monitor skali, konfigurowanie i połączeń hybrydowych było możliwe. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 4ec88d9a681a5692b31f7e3990d1c153296b18ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="6dd4d-104">Przegląd kart Pulpit nawigacyjny, Monitorowanie, Skala, Konfigurowanie i Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="6dd4d-104">Review the Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="6dd4d-105">Po utworzeniu usługi BizTalk i wdrażania aplikacji, można zmienić niektóre ustawienia usługi BizTalk i monitorowania wydajności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-105">After you create your BizTalk Service and deploy your application, you can change some of the BizTalk Service settings and monitor the application performance.</span></span> 

<span data-ttu-id="6dd4d-106">Po otwarciu klasycznego portalu Azure, można automatycznie umieszczane w **wszystkie elementy** kartę.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-106">When you open the Azure classic portal, you are automatically placed at the **ALL ITEMS** tab.</span></span> <span data-ttu-id="6dd4d-107">Aby wyświetlić usługi BizTalk, wybierz usługę BizTalk w **wszystkie elementy** karcie lub wybierz **usługi BIZTALK SERVICES** ; a następnie wybierz nazwę usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-107">To view your BizTalk Service, select your BizTalk Service in the **ALL ITEMS** tab or select the **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="6dd4d-108">Spowoduje to otwarcie nowego okna zawierająca poniższe karty.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-108">This opens a new window with the following tabs.</span></span> <span data-ttu-id="6dd4d-109">W tym temacie opisano te karty.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-109">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="6dd4d-110">(Szybki Start</span><span class="sxs-lookup"><span data-stu-id="6dd4d-110">Quickstart (</span></span>![Szybki start][Quickstart]<span data-ttu-id="6dd4d-112">)</span><span class="sxs-lookup"><span data-stu-id="6dd4d-112">)</span></span>
<span data-ttu-id="6dd4d-113">W zależności od wersji usługi BizTalk wszystkie opcje wymienione mogą nie być dostępne.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-113">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="6dd4d-114"><strong>Pobierz narzędzia</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-114"><strong>Get the tools</strong></span></span></td>
        <td><span data-ttu-id="6dd4d-115">Pobierz zestaw SDK usługi BizTalk do zainstalowania na komputerze deweloperskim lokalnymi szablony projektu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-115">Download the BizTalk Services SDK to install the Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="6dd4d-116">Te szablony tworzą <strong>usługi BizTalk Services</strong> (mostek) i <strong>artefaktów usługi BizTalk</strong> projektów programu Visual Studio (Transform), które są wdrażane do usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-116">These templates create the <strong>BizTalk Services</strong> (bridge) and the <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed to your BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="6dd4d-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Jak uruchomić, przy użyciu zestawu SDK usługi Azure BizTalk </a> i <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Instalowanie zestawu SDK usługi Azure BizTalk</a> zawiera listę czynności, aby rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using the Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing the Azure BizTalk Services SDK</a> lists the steps to get started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="6dd4d-118"><strong>Tworzenie partnerów, umów</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-118"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="6dd4d-119">Otwiera hostowanej na platformie Azure, gdzie Dodawanie partnerami i tworzenie X12, AS2, portalu usługi Azure BizTalk i umów EDIFACT EDI.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-119">Opens the Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="6dd4d-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Konfigurowanie składników EDI obsługi wiadomości w portalu usługi BizTalk</a> zawiera listę czynności, aby rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists the steps to get started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="6dd4d-121"><strong>Dowiedz się więcej na temat usługi BizTalk Services</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-121"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="6dd4d-122">Przejdź do <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">Centrum uczenia</a> Aby dowiedzieć się więcej o usługach BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-122">Go to the <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> to learn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="6dd4d-123">Na pasku zadań u dołu można:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-123">In the task bar at the bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="6dd4d-124"><strong>Zarządzanie</strong> wdrażania aplikacji</span><span class="sxs-lookup"><span data-stu-id="6dd4d-124"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="6dd4d-125">Otwiera portalu Azure usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-125">Opens the Azure BizTalk Services portal.</span></span> <span data-ttu-id="6dd4d-126">Portal usługi BizTalk jest wejścia do konfiguracji EDI, w tym dodawanie partnerami i tworzenie X12, AS2 oraz umów EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-126">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="6dd4d-127">To jest taka sama jak <strong>Tworzenie umów z partnerami</strong> na <strong>Szybki Start</strong> kartę.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-127">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="6dd4d-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Konfigurowanie składników EDI obsługi wiadomości w portalu usługi BizTalk</a> zamieszczono więcej informacji dotyczących portalu usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="6dd4d-129"><strong>Informacje o połączeniu</strong> z Namespace kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="6dd4d-129"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="6dd4d-130">Po wybraniu informacje o połączeniu, następnie Namespace kontroli dostępu, domyślne wystawcy i klucza domyślne są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-130">When you select Connection Information, then the Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="6dd4d-131">Możesz skopiować te wartości.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-131">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="6dd4d-132">Można również otworzyć Portal kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-132">You can also open the Access Control Portal.</span></span> <span data-ttu-id="6dd4d-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Utwórz kontroli dostępu Namespace</a> zamieszczono więcej informacji dotyczących portalu kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="6dd4d-134"><strong>Synchronizowanie kluczy</strong> na koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="6dd4d-134"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="6dd4d-135">Podczas tworzenia konta usługi Storage następuje automatyczne utworzenie klucza podstawowego i klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-135">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="6dd4d-136">Te klucze szyfrowania kontroli dostępu do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-136">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="6dd4d-137">Usługi BizTalk automatycznie korzysta z klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-137">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="6dd4d-138"><strong>Synchronizowanie kluczy</strong> użytkownicy mogą przełączać się między klucz podstawowy i klucz pomocniczy bez zakłócania działania usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-138"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="6dd4d-139">Możesz na przykład usługi BizTalk do nowego podstawowego klucza dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-139">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="6dd4d-140">W tym celu:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-140">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="6dd4d-141">Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-141">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="6dd4d-142">Wybierz klucz pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-142">Select the Secondary Key.</span></span> <span data-ttu-id="6dd4d-143">Po wykonaniu tej czynności usługa BizTalk jest uruchamiana za pomocą klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-143">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="6dd4d-144">W klasycznym portalu Azure wybierz konto magazynu i ponowne wygenerowanie klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-144">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="6dd4d-145">Należy pamiętać, że usługi BizTalk używa klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-145">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="6dd4d-146">Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-146">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="6dd4d-147">Teraz wybierz klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-147">Now, select the Primary Key.</span></span> <span data-ttu-id="6dd4d-148">Jest to nowy klucz podstawowy zostanie ponownie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-148">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="6dd4d-149">W klasycznym portalu Azure wybierz konto magazynu i ponowne wygenerowanie klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-149">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="6dd4d-150">Ten proces jest nazywany "przerzucania kluczy".</span><span class="sxs-lookup"><span data-stu-id="6dd4d-150">This process is called "rollover keys".</span></span> <span data-ttu-id="6dd4d-151">Celem jest umożliwienie użytkownikom przełączać się między klucz podstawowy i klucz pomocniczy bez zakłócania działania usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-151">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="6dd4d-152"><strong>Usuń</strong> aplikacji</span><span class="sxs-lookup"><span data-stu-id="6dd4d-152"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="6dd4d-153">Po wybraniu usunąć usługi BizTalk i zostaną usunięte wszystkie elementy w nim wdrożona.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-153">When you select Delete, your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="6dd4d-154">Pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="6dd4d-154">Dashboard</span></span>
<span data-ttu-id="6dd4d-155">W zależności od wersji usługi BizTalk wszystkie opcje wymienione mogą nie być dostępne.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-155">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="6dd4d-156">Po wybraniu nazwy usługi BizTalk karty Pulpit nawigacyjny jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-156">When you select your BizTalk Service name, the Dashboard tab is displayed.</span></span> <span data-ttu-id="6dd4d-157">Na pulpicie nawigacyjnym można:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-157">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a><span data-ttu-id="6dd4d-158">Przegląd wykorzystania: Pokazuje liczbę używanych połączeń hybrydowych</span><span class="sxs-lookup"><span data-stu-id="6dd4d-158">Usage Overview: Shows the number of used Hybrid Connections</span></span>
<span data-ttu-id="6dd4d-159">Dane użycia są również wyświetlane w GB.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-159">Also displays the data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="6dd4d-160">Wykres metryki: Lista stałej metryki wydajności</span><span class="sxs-lookup"><span data-stu-id="6dd4d-160">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="6dd4d-161">Te metryki Podaj wartości w czasie rzeczywistym dotyczące kondycji usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-161">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="6dd4d-162">Można również wybrać **względną** lub **bezwzględną** wartości i zakres czasu **interwał** metryk, które są wyświetlane na wykresie.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-162">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed in the graph.</span></span> 

<span data-ttu-id="6dd4d-163">Aby uzyskać opis tych metryk wydajności, przejdź do [dostępne metryki](#Metrics) w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-163">For a description of these performance metrics, go to [Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="6dd4d-164">Szybkiego dostępu: Wyświetla listę właściwości usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="6dd4d-164">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="6dd4d-165"><strong>Zaktualizuj poświadczenia śledzenia bazy danych</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-165"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="6dd4d-166">Zmienia nazwę użytkownika i hasło używane do logowania do bazy danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-166">Changes the user name and password used to log into the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-167"><strong>Aktualizuj certyfikat protokołu SSL</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-167"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="6dd4d-168">Można zaktualizować usługi BizTalk, aby użyć innego certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-168">Can update the BizTalk Service to use a different SSL certificate.</span></span> <span data-ttu-id="6dd4d-169">Certyfikat SSL z podpisem własnym jest tworzony automatycznie, gdy użytkownik <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Utwórz usługę BizTalk</a>.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-169">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create the BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-170"><strong>Pobierz certyfikat</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-170"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="6dd4d-171">Możesz pobrać certyfikat SSL używany przez usługę BizTalk do komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-171">You can download the SSL certificate used by your BizTalk Service to a local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-172"><strong>Stan</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-172"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="6dd4d-173">Wyświetla bieżący stan usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-173">Displays the current status of your BizTalk Service.</span></span> <span data-ttu-id="6dd4d-174">Zobacz <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">usługi BizTalk Services: Usługa stanu wykresu</a>.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-174">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-175"><strong>Adres URL usługi</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-175"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="6dd4d-176">Adres URL dla usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-176">The URL for your BizTalk Service.</span></span> <span data-ttu-id="6dd4d-177">To jest taka sama jak <strong>adresu URL domeny</strong> wprowadzane podczas tworzenia usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-177">This is the same as the <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-178"><strong>Adres publiczny wirtualnego adresu IP (VIP)</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-178"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="6dd4d-179">Adres IP przypisany do usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-179">The IP address assigned to your BizTalk Service.</span></span> <span data-ttu-id="6dd4d-180">Jest on używany dla wszystkich wejściowych punktów końcowych i jest adresu źródłowego dla ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-180">It is used for all input endpoints and is the source address for outbound traffic.</span></span> <span data-ttu-id="6dd4d-181">Ten adres IP należy do usługi BizTalk, pod warunkiem jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-181">This IP address belongs to your BizTalk Service as long as it is created.</span></span> <span data-ttu-id="6dd4d-182">Usunięcie usługi BizTalk, adres IP jest przypisany do innej usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-182">If you delete the BizTalk Service, the IP address is assigned to another BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-183"><strong>Namespace ACS</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-183"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="6dd4d-184">Uwierzytelnianie przy użyciu usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-184">Authenticates with the BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-185"><strong>Wersja</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-185"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="6dd4d-186">Wyświetla wersję wprowadzane podczas tworzenia usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-186">Lists the Edition entered when the BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-187"><strong>Lokalizacja</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-187"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="6dd4d-188">Wyświetla region geograficzny, który jest hostem usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-188">Displays the geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-189"><strong>Utworzone</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-189"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="6dd4d-190">Wyświetla datę i godzinę utworzenia usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-190">Displays the date and time the BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-191"><strong>Śledzenie bazy danych</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-191"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="6dd4d-192">Nazwa bazy danych SQL Azure, która przechowuje tabele śledzenia używane przez usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-192">The Azure SQL Database name that stores the tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="6dd4d-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Wymagania dotyczące poradnik</a> zawiera szczegółowe informacje w bazie danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-194"><strong>Monitorowanie archiwizacji magazynu</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-194"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="6dd4d-195">Nazwa konta usługi Azure Storage przechowuje dane wyjściowe monitorowania usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-195">The Azure Storage account name that stores the monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="6dd4d-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Wymagania dotyczące poradnik</a> zawiera szczegółowe informacje na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-197"><strong>Nazwa subskrypcji</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-197"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="6dd4d-198">Wyświetla listę subskrypcji, który jest hostem usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-198">Lists the subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="6dd4d-199">Subskrypcja kontroluje dostęp do klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-199">The subscription governs access to the Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-200"><strong>Identyfikator subskrypcji</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-200"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="6dd4d-201">Identyfikator subskrypcji jest generowany automatycznie podczas tworzenia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-201">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="6dd4d-202">Podczas korzystania z interfejsów API REST, należy podać nazwę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-202">When using REST APIs, you may need to enter the Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="6dd4d-203">[Usługi BizTalk Services: Inicjowanie obsługi administracyjnej klasycznego portalu Azure za pomocą](http://go.microsoft.com/fwlink/p/?LinkID=302280) zawiera listę czynności w celu utworzenia usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-203">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists the steps to create a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a><span data-ttu-id="6dd4d-204">Zarządzanie, informacje o połączeniu, klucze synchronizacji i Usuń na pasku zadań:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-204">Manage, Connection Information, Sync Keys, and Delete in the task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="6dd4d-205"><strong>Zarządzanie</strong> wdrażania aplikacji</span><span class="sxs-lookup"><span data-stu-id="6dd4d-205"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="6dd4d-206">Otwiera portalu usługi Azure BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-206">Opens the Azure BizTalk Services Portal.</span></span> <span data-ttu-id="6dd4d-207">Portal usługi BizTalk jest wejścia do konfiguracji EDI, w tym dodawanie partnerami i tworzenie X12, AS2 oraz umów EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-207">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="6dd4d-208">To jest taka sama jak <strong>Tworzenie umów z partnerami</strong> na <strong>Szybki Start</strong> kartę.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-208">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="6dd4d-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Konfigurowanie składników EDI obsługi wiadomości w portalu usługi BizTalk</a> zamieszczono więcej informacji dotyczących portalu usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-210"><strong>Informacje o połączeniu</strong> z Namespace kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="6dd4d-210"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="6dd4d-211">Wyświetla Namespace kontroli dostępu, domyślne wystawcy i klucza domyślne wartości. które mogą zostać skopiowane.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-211">Displays the Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="6dd4d-212">Można również otworzyć Portal kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-212">You can also open the Access Control Portal.</span></span> <span data-ttu-id="6dd4d-213">Ten Portal kontroli dostępu jest taka sama jak przy użyciu opcji usługi Active Directory, w lewym okienku nawigacji.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-213">This Access Control Portal is the same as using the Active Directory option in the left navigation pane.</span></span>
<br/><br/><span data-ttu-id="6dd4d-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Zarządzanie Your Namespace ACS</a> zamieszczono więcej informacji dotyczących portalu kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-215"><strong>Synchronizowanie kluczy</strong> na koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="6dd4d-215"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="6dd4d-216">Podczas tworzenia konta usługi Storage następuje automatyczne utworzenie klucza podstawowego i klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-216">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="6dd4d-217">Te klucze szyfrowania kontroli dostępu do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-217">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="6dd4d-218">Usługi BizTalk automatycznie korzysta z klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-218">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="6dd4d-219"><strong>Synchronizowanie kluczy</strong> użytkownicy mogą przełączać się między klucz podstawowy i klucz pomocniczy bez zakłócania działania usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-219"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="6dd4d-220">Możesz na przykład usługi BizTalk do nowego podstawowego klucza dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-220">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="6dd4d-221">W tym celu:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-221">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="6dd4d-222">Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-222">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="6dd4d-223">Wybierz klucz pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-223">Select the Secondary Key.</span></span> <span data-ttu-id="6dd4d-224">Po wykonaniu tej czynności usługa BizTalk jest uruchamiana za pomocą klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-224">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="6dd4d-225">W klasycznym portalu Azure wybierz konto magazynu i ponowne wygenerowanie klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-225">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="6dd4d-226">Należy pamiętać, że usługi BizTalk używa klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-226">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="6dd4d-227">Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-227">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="6dd4d-228">Teraz wybierz klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-228">Now, select the Primary Key.</span></span> <span data-ttu-id="6dd4d-229">Jest to nowy klucz podstawowy zostanie ponownie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-229">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="6dd4d-230">W klasycznym portalu Azure wybierz konto magazynu i ponowne wygenerowanie klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-230">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="6dd4d-231">Ten proces jest nazywany "przerzucania kluczy".</span><span class="sxs-lookup"><span data-stu-id="6dd4d-231">This process is called "rollover keys".</span></span> <span data-ttu-id="6dd4d-232">Celem jest umożliwienie użytkownikom przełączać się między klucz podstawowy i klucz pomocniczy bez zakłócania działania usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-232">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="6dd4d-233"><strong>Usuń</strong> aplikacji</span><span class="sxs-lookup"><span data-stu-id="6dd4d-233"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="6dd4d-234">Usługi BizTalk i wszystkie elementy w nim wdrożona zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-234">Your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="6dd4d-235">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="6dd4d-235">Monitor</span></span>
<span data-ttu-id="6dd4d-236">Nie ma zastosowania do bezpłatna wersja.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-236">Does not apply to the Free Edition.</span></span>

<span data-ttu-id="6dd4d-237">Po wybraniu nazwy usługi BizTalk karcie Monitor jest dostępne i zostaną wyświetlone następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-237">When you select your BizTalk Service name, the Monitor tab is available and displays the following:</span></span>

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a><span data-ttu-id="6dd4d-238">Wykres metryki: Wyświetla metryki wydajności wybranych</span><span class="sxs-lookup"><span data-stu-id="6dd4d-238">Metric Graph: Displays the selected performance metrics</span></span>
<span data-ttu-id="6dd4d-239">Te metryki Podaj wartości w czasie rzeczywistym dotyczące kondycji usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-239">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="6dd4d-240">Możesz wybrać metryki wydajności, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-240">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="6dd4d-241">Maksymalnie sześć metryki wydajności mogą być jednocześnie wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-241">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="6dd4d-242">Można również wybrać **względną** lub **bezwzględną** wartości i zakres czasu **interwał** metryk, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-242">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed.</span></span> 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a><span data-ttu-id="6dd4d-243">Aby usunąć lub wyświetlania metryk na wykresie:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-243">To remove or display metrics in the graph:</span></span>
1. <span data-ttu-id="6dd4d-244">Wybierz **Monitor** kartę.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-244">Select the **Monitor** tab.</span></span>
2. <span data-ttu-id="6dd4d-245">Wybierz **dodać metryki** na pasku zadań:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-245">Select **Add Metrics** in the task bar:</span></span>  
   <span data-ttu-id="6dd4d-246">![Wybierz opcję Dodaj metryk][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="6dd4d-246">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="6dd4d-247">Sprawdź metryki wydajności, które mają być wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-247">Check the performance metrics you want to display.</span></span>
4. <span data-ttu-id="6dd4d-248">Wybierz znacznik wyboru, aby powrócić do **Monitor** kartę.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-248">Select the checkmark to return to the **Monitor** tab.</span></span>
5. <span data-ttu-id="6dd4d-249">Wybierz kółko obok metrykę, aby wyświetlić wartość tego metryki na wykresie.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-249">Select the circle next to the metric to display that metric's value in the graph.</span></span>  
   
    <span data-ttu-id="6dd4d-250">Na przykład **użycie procesora CPU** metryka jest wyszarzona; jego dane wyjściowe nie są wyświetlane na wykresie:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-250">For example, the **CPU Usage** metric is grayed out; its output is not displayed in the graph:</span></span>  
   <span data-ttu-id="6dd4d-251">![Metryki użycia procesora CPU jest szary.][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="6dd4d-251">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="6dd4d-252">Wybierz na wygaszone się koło, aby włączyć **użycie procesora CPU** metrykę, aby wyświetlić dane wyjściowe na wykresie:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-252">Select the grayed out circle to enable the **CPU Usage** metric to display its output in the graph:</span></span>  
   <span data-ttu-id="6dd4d-253">![Metryki użycia procesora CPU jest włączona.][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="6dd4d-253">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="6dd4d-254">Aby usunąć metryki z wykresu wyświetlania i listy, wybierz **usunąć Metryka** na pasku zadań.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-254">To remove a metric from the display graph and the list, select **Delete Metric** in the task bar.</span></span> <span data-ttu-id="6dd4d-255">Aby dodać metryki wstecz do listy, wybierz opcję **dodać metryki** na pasku zadań sprawdź metrykę, a następnie wybierz znacznik wyboru, aby powrócić do **Monitor** kartę.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-255">To add the metric back to the list, select **Add Metrics** in the task bar, check the metric, and select the checkmark to return to the **Monitor** tab.</span></span> <span data-ttu-id="6dd4d-256">Wybierz wygaszone koło, aby włączyć metryki.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-256">Select the grayed out circle to enable the metric.</span></span>

## <span data-ttu-id="6dd4d-257"><a name="Metrics"></a>Dostępne metryki</span><span class="sxs-lookup"><span data-stu-id="6dd4d-257"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="6dd4d-258">Dostępne są następujące liczniki wydajności/metryki:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-258">The following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="6dd4d-259"><strong>Opóźnienie RountdTrip</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-259"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="6dd4d-260">Wyświetla wszystkie mostków Średni czas przetwarzania wiadomości od czasu odbioru wiadomości do momentu wiadomości jest w pełni przetworzone przez usługę BizTalk w milisekundach (ms).</span><span class="sxs-lookup"><span data-stu-id="6dd4d-260">Displays the average time taken in milliseconds (ms) to process a message from the time the message is received until the message is fully processed by the BizTalk Service across all bridges.</span></span> <span data-ttu-id="6dd4d-261">Zliczane są tylko pomyślnie przetworzonych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-261">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="6dd4d-262">Gdy występują następujące zdarzenia, tworzona jest sygnatura czasowa:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-262">When the following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="6dd4d-263">Brama wprowadza wiadomości</span><span class="sxs-lookup"><span data-stu-id="6dd4d-263">Message enters the gateway</span></span></li>
<li><span data-ttu-id="6dd4d-264">Komunikat jest kierowany do miejsca docelowego</span><span class="sxs-lookup"><span data-stu-id="6dd4d-264">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="6dd4d-265">Miejsce docelowe odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6dd4d-265">Destination response is received</span></span></li>
<li><span data-ttu-id="6dd4d-266">Wysłane do bramy odpowiedzi potwierdzenia docelowego</span><span class="sxs-lookup"><span data-stu-id="6dd4d-266">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="6dd4d-267">Ta metryka przedstawia wynik następującego obliczenia:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-267">This metric shows the result of the following calculation:</span></span>
<br/><br/>
<span data-ttu-id="6dd4d-268">[Docelowy potwierdzenia odpowiedzi wysłanych do bramy] - [brama wprowadza wiadomości]</span><span class="sxs-lookup"><span data-stu-id="6dd4d-268">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-269"><strong>Błędy w źródle</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-269"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="6dd4d-270">Wyświetla całkowitą liczbę wiadomości, których nie powiodła się przez usługę BizTalk, gdy ściąganie wiadomości z punktów końcowych źródła.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-270">Displays the total number of messages that failed by the BizTalk Service when pulling messages from the source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-271"><strong>Użycie procesora CPU</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-271"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="6dd4d-272">Wyświetla średni procent czasu procesora wszystkich wystąpień ról.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-272">Lists the average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-273"><strong>Opóźnienie przetwarzania</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-273"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="6dd4d-274">Wyświetla średni czas w milisekundach (ms) do przetworzenia komunikatu przez usługę BizTalk mostków wszystkich, z wyłączeniem czasu poświęconego w miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-274">Displays the average time taken In milliseconds (ms) to process a message by the BizTalk Service across all bridges, excluding the time spent in destinations.</span></span> <span data-ttu-id="6dd4d-275">Zliczane są tylko pomyślnie przetworzonych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-275">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="6dd4d-276">W przypadku wystąpienia każdej z następujących zdarzeń, tworzona jest sygnatura czasowa:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-276">When each of the following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="6dd4d-277">Brama wprowadza wiadomości</span><span class="sxs-lookup"><span data-stu-id="6dd4d-277">Message enters the gateway</span></span></li>
<li><span data-ttu-id="6dd4d-278">Komunikat jest kierowany do miejsca docelowego</span><span class="sxs-lookup"><span data-stu-id="6dd4d-278">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="6dd4d-279">Miejsce docelowe odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6dd4d-279">Destination response is received</span></span></li>
<li><span data-ttu-id="6dd4d-280">Wysłane do bramy odpowiedzi potwierdzenia docelowego</span><span class="sxs-lookup"><span data-stu-id="6dd4d-280">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/><span data-ttu-id="6dd4d-281">Ta metryka przedstawia wynik następującego obliczenia:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-281">This metric shows the result of the following calculation:</span></span><br/><br/>
<span data-ttu-id="6dd4d-282">[Docelowy potwierdzenia odpowiedzi wysłanych do bramy] - [brama wprowadza wiadomości] - [docelowy odpowiedzi] + [wiadomość jest przesyłana do lokalizacji docelowej]</span><span class="sxs-lookup"><span data-stu-id="6dd4d-282">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway] - [Destination response is received] + [Message is routed to the destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-283"><strong>Błędy w procesie</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-283"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="6dd4d-284">Wyświetla całkowitą liczbę komunikatów, których nie powiodła się podczas przetwarzania przez usługę BizTalk we wszystkich mostków w interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-284">Displays the total number of messages that failed during processing by the BizTalk Service across all the bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-285"><strong>Komunikaty wysyłane</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-285"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="6dd4d-286">Wyświetla całkowitą liczbę komunikatów wysłanych przez usługę BizTalk we wszystkich mostków w interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-286">Displays the total number of messages sent by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="6dd4d-287">Ta metryka jest zwiększany, gdy komunikat wysłany z potokiem osiągnie docelowy trasy.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-287">This metric is incremented when a message sent from a pipeline reaches the route destination.</span></span> <span data-ttu-id="6dd4d-288">Ta metryka nie wskazuje, że wiadomość jest pomyślnie przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-288">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="6dd4d-289">W scenariuszu żądanie-odpowiedź metryka jest zwiększany po docelowy trasy wysyła potwierdzenia otrzymania z powrotem do potoku.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-289">In a Request-Reply scenario, the metric is incremented when the route destination sends a receipt acknowledgement back to the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-290"><strong>Odebrane wiadomości</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-290"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="6dd4d-291">Wyświetla całkowitą liczbę komunikatów odebranych przez usługę BizTalk we wszystkich mostków w interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-291">Displays the total number of messages received by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="6dd4d-292">Ta metryka jest zwiększany, gdy nowy komunikat jest odbierany przez potok.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-292">This metric is incremented when a new message is received by the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-293"><strong>Komunikaty w procesie</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-293"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="6dd4d-294">Wyświetla całkowitą liczbę komunikatów aktualnie przetwarzanych przez usługę BizTalk w interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-294">Displays the total number of messages currently being processed by the BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dd4d-295"><strong>Liczba przetworzonych komunikatów</strong></span><span class="sxs-lookup"><span data-stu-id="6dd4d-295"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="6dd4d-296">Wyświetla całkowitą liczbę komunikatów pomyślnie przetworzone przez usługę BizTalk we wszystkich mostków w interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-296">Displays the total number of messages successfully processed by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="6dd4d-297">Ta metryka jest zwiększany, gdy komunikat jest pomyślnie zostały odebrane przez potok i pomyślnie skierowany do miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-297">This metric is incremented when a message is successfully received by the pipeline and successfully routed to the destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="6dd4d-298">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="6dd4d-298">Scale</span></span>
<span data-ttu-id="6dd4d-299">Na karcie skali można dodać lub odjąć liczbę jednostek używanych przez usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-299">In the Scale tab, you can add or subtract the number of units used by your BizTalk Service.</span></span> <span data-ttu-id="6dd4d-300">Domyślnie istnieje skonfigurowane jednostki.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-300">By default, there is one Unit configured.</span></span> <span data-ttu-id="6dd4d-301">Można dodać dodatkowe jednostki skalowania usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-301">Additional Units can be added to scale your BizTalk Service.</span></span> <span data-ttu-id="6dd4d-302">Zwiększenie skali są zwiększyć przepustowość.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-302">When you increase the scale, you are increasing throughput.</span></span> <span data-ttu-id="6dd4d-303">Ilość zasobów zwiększa także, tym mostków wdrożone, umowy, LOB połączeń i mocy obliczeniowej.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-303">The amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="6dd4d-304">Na przykład zwiększenie skali od 1 jednostka do 2 jednostki.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-304">For example, you increase the scale from 1 Unit to 2 Units.</span></span> <span data-ttu-id="6dd4d-305">W takiej sytuacji można wdrożyć podwoić liczbę mostków, dwukrotnie umowy, dwukrotnie połączeń biznesowych i dwukrotnie moc obliczeniową.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-305">In this situation, you can deploy double the number of bridges, double the agreements, double the LOB connections, and double the processing power.</span></span>

<span data-ttu-id="6dd4d-306">Niektóre wersje BizTalk nie oferują opcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-306">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="6dd4d-307">W takim przypadku jednostki jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-307">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="6dd4d-308">Aby określić liczbę jednostek, które mogą być skalowane posiadanej wersji, zajrzyj do [usługi BizTalk Services: wersje wykresu](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="6dd4d-308">To determine how many units your edition can be scaled, refer to [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="6dd4d-309">Zwiększenie liczby jednostek może mieć wpływ cennik.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-309">Increasing the number of units may impact pricing.</span></span> <span data-ttu-id="6dd4d-310">Jeśli zwiększysz jednostki, wybierając **zapisać** zostanie wyświetlony komunikat informujący o tym, jeśli jest wpływ na rozliczenia.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-310">If you increase the Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="6dd4d-311">Następnie można kontynuować.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-311">You then choose to continue.</span></span> <span data-ttu-id="6dd4d-312">Wraz ze zwiększeniem liczba jednostek, zmiany stanu usługi BizTalk z aktywnego aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-312">When you increase the number of Units, the BizTalk Service status changes from Active to Updating.</span></span> <span data-ttu-id="6dd4d-313">Stan aktualizacji usługi BizTalk jest nadal uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-313">In the Updating state, your BizTalk Service continues to run.</span></span>

<span data-ttu-id="6dd4d-314">[Usługi BizTalk Services: Wersje wykresu](biztalk-editions-feature-chart.md) definiuje "Jednostki".</span><span class="sxs-lookup"><span data-stu-id="6dd4d-314">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="6dd4d-315">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="6dd4d-315">Configure</span></span>
<span data-ttu-id="6dd4d-316">Nie ma zastosowania do połączeń hybrydowych było możliwe.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-316">Does not apply to Hybrid Connections.</span></span>

<span data-ttu-id="6dd4d-317">Ustawia stan kopii zapasowej, None lub automatyczne.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-317">Sets the Backup Status to None or Automatic.</span></span> <span data-ttu-id="6dd4d-318">Jeśli wartość None, nie ma kopii zapasowych są tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-318">When set to None, no backups are automatically created.</span></span> <span data-ttu-id="6dd4d-319">Jeśli ustawiono automatyczne, możesz skonfigurować lokalizację kopii zapasowej, częstotliwości kopii zapasowych i jak długo, aby zachować pliki kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-319">When set to Automatic, you configure the backup location, the frequency of the backup, and how long to keep the backup files.</span></span> 

<span data-ttu-id="6dd4d-320">[Usługi BizTalk Services: Kopia zapasowa i przywracanie](biztalk-backup-restore.md) udostępnia szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-320">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides the details.</span></span> 

## <span data-ttu-id="6dd4d-321"><a name="HybridConnections"></a>Połączenia hybrydowe</span><span class="sxs-lookup"><span data-stu-id="6dd4d-321"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="6dd4d-322">Połączenia hybrydowe umożliwiają łączenie aplikacji Azure, takich jak aplikacje sieci Web lub Mobile Apps w usłudze Azure App Service lokalnymi zasobem, który korzysta z portu statycznego TCP, takich jak SQL Server, MySQL, interfejsów API sieci Web HTTP i większość niestandardowych usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-322">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, to an on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="6dd4d-323">Usługi BizTalk Services zarządzania połączeń hybrydowych w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6dd4d-323">Hybrid Connections are managed in  BizTalk Services in the Azure classic portal.</span></span>

<span data-ttu-id="6dd4d-324">Aby utworzyć połączeń hybrydowych w usłudze Azure App Service, zobacz [dostępu do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6dd4d-324">To create Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="6dd4d-325">Aby utworzyć lub zarządzać połączeń hybrydowych w usłudze Azure BizTalk Services, zobacz [połączeń hybrydowych](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6dd4d-325">To create or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="6dd4d-326">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6dd4d-326">Next</span></span>
<span data-ttu-id="6dd4d-327">Teraz, kiedy znasz różnych kartach zawierających, można dowiedzieć się więcej o funkcji usług BizTalk Azure:</span><span class="sxs-lookup"><span data-stu-id="6dd4d-327">Now that you're familiar with the different tabs, you can learn more about the Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="6dd4d-328">BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)</span><span class="sxs-lookup"><span data-stu-id="6dd4d-328">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="6dd4d-329">BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)</span><span class="sxs-lookup"><span data-stu-id="6dd4d-329">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="6dd4d-330">BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)</span><span class="sxs-lookup"><span data-stu-id="6dd4d-330">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="6dd4d-331">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6dd4d-331">See Also</span></span>
* [<span data-ttu-id="6dd4d-332">Połączenia hybrydowe</span><span class="sxs-lookup"><span data-stu-id="6dd4d-332">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="6dd4d-333">Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu</span><span class="sxs-lookup"><span data-stu-id="6dd4d-333">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="6dd4d-334">Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="6dd4d-334">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="6dd4d-335">Usługi BizTalk Services: Stan usługi BizTalk wykresu</span><span class="sxs-lookup"><span data-stu-id="6dd4d-335">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="6dd4d-336">Jak rozpocząć pracę z zestawem SDK usługi Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="6dd4d-336">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

