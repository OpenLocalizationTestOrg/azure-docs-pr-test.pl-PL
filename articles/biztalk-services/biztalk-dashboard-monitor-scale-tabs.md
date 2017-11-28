---
title: "aaaDashboard, monitora, skalowania, konfigurowanie i połączeń hybrydowych w usługi BizTalk Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello formantów i monitorowanie wydajności na kartach portalu klasycznego hello usługi BizTalk Services: pulpitu nawigacyjnego, Monitor skali, konfigurowanie i połączeń hybrydowych było możliwe. MABS, WABS"
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
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="f0640-104">Przejrzyj hello karty Pulpit nawigacyjny, Monitor skali, konfigurowanie i połączenia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="f0640-104">Review hello Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="f0640-105">Po utworzeniu usługi BizTalk i wdrażania aplikacji, można zmienić niektóre ustawienia usługi BizTalk hello i monitorowanie wydajności aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f0640-105">After you create your BizTalk Service and deploy your application, you can change some of hello BizTalk Service settings and monitor hello application performance.</span></span> 

<span data-ttu-id="f0640-106">Po otwarciu hello klasycznego portalu Azure, można automatycznie umieszczane w hello **wszystkie elementy** tooview kartę usługi BizTalk, wybierz usługę BizTalk w hello **wszystkie elementy** tab lub wybierz hello **Usługi BIZTALK SERVICES** ; a następnie wybierz nazwę usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-106">When you open hello Azure classic portal, you are automatically placed at hello **ALL ITEMS** tab. tooview your BizTalk Service, select your BizTalk Service in hello **ALL ITEMS** tab or select hello **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="f0640-107">Spowoduje to otwarcie nowego okna z hello następujące karty.</span><span class="sxs-lookup"><span data-stu-id="f0640-107">This opens a new window with hello following tabs.</span></span> <span data-ttu-id="f0640-108">W tym temacie opisano te karty.</span><span class="sxs-lookup"><span data-stu-id="f0640-108">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="f0640-109">(Szybki Start</span><span class="sxs-lookup"><span data-stu-id="f0640-109">Quickstart (</span></span>![Szybki start][Quickstart]<span data-ttu-id="f0640-111">)</span><span class="sxs-lookup"><span data-stu-id="f0640-111">)</span></span>
<span data-ttu-id="f0640-112">W zależności od wersji usługi BizTalk hello wszystkie opcje wymienione mogą nie być dostępne.</span><span class="sxs-lookup"><span data-stu-id="f0640-112">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="f0640-113"><strong>Pobierz narzędzia hello</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-113"><strong>Get hello tools</strong></span></span></td>
        <td><span data-ttu-id="f0640-114">Pobierz hello zestawu SDK usługi BizTalk Services tooinstall hello szablony projektu Visual Studio na komputerze deweloperskim lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="f0640-114">Download hello BizTalk Services SDK tooinstall hello Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="f0640-115">Te szablony tworzą hello <strong>usługi BizTalk Services</strong> (mostek) i hello <strong>artefaktów usługi BizTalk</strong> projektów programu Visual Studio (Transform), które są wdrożone tooyour usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-115">These templates create hello <strong>BizTalk Services</strong> (bridge) and hello <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed tooyour BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="f0640-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Jak mogę uruchomić przy użyciu hello zestaw SDK usług BizTalk Azure </a> i <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">hello Instalowanie zestawu SDK usługi BizTalk Azure</a> list hello tooget kroki pracy.</span><span class="sxs-lookup"><span data-stu-id="f0640-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using hello Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing hello Azure BizTalk Services SDK</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="f0640-117"><strong>Tworzenie partnerów, umów</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-117"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="f0640-118">Zostanie otwarta hello Portal usługi BizTalk Azure hostowanej na platformie Azure, gdzie Dodawanie partnerami i tworzenie X12, AS2 oraz umów EDIFACT EDI.</span><span class="sxs-lookup"><span data-stu-id="f0640-118">Opens hello Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="f0640-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Konfigurowanie składników EDI obsługi wiadomości w portalu usługi BizTalk</a> list hello tooget kroki pracy.</span><span class="sxs-lookup"><span data-stu-id="f0640-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="f0640-120"><strong>Dowiedz się więcej na temat usługi BizTalk Services</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-120"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="f0640-121">Przejdź toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">Centrum uczenia</a> toolearn więcej informacji na temat usług BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="f0640-121">Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="f0640-122">Na pasku zadań hello u dołu hello można:</span><span class="sxs-lookup"><span data-stu-id="f0640-122">In hello task bar at hello bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="f0640-123"><strong>Zarządzanie</strong> wdrażania aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0640-123"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="f0640-124">Otwiera hello portalu Azure usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-124">Opens hello Azure BizTalk Services portal.</span></span> <span data-ttu-id="f0640-125">Portal usługi BizTalk Hello jest hello wejściu tooEDI konfiguracji, w tym dodawanie partnerami i tworzenie X12, AS2 oraz umów EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="f0640-125">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="f0640-126">To jest identyczny hello <strong>Tworzenie umów z partnerami</strong> na powitania <strong>Szybki Start</strong> kartę.</span><span class="sxs-lookup"><span data-stu-id="f0640-126">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="f0640-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Konfigurowanie składników EDI obsługi wiadomości w portalu usługi BizTalk</a> zamieszczono więcej informacji dotyczących hello Portal usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="f0640-128"><strong>Informacje o połączeniu</strong> z hello Namespace kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="f0640-128"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="f0640-129">Po wybraniu informacje o połączeniu tekst hello Namespace kontroli dostępu, domyślne wystawcy i klucza domyślne są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="f0640-129">When you select Connection Information, then hello Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="f0640-130">Możesz skopiować te wartości.</span><span class="sxs-lookup"><span data-stu-id="f0640-130">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="f0640-131">Można również otworzyć hello portalu kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="f0640-131">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="f0640-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Utwórz kontroli dostępu Namespace</a> zamieszczono więcej informacji dotyczących hello portalu kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="f0640-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="f0640-133"><strong>Synchronizowanie kluczy</strong> w hello konta magazynu</span><span class="sxs-lookup"><span data-stu-id="f0640-133"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="f0640-134">Podczas tworzenia konta usługi Storage następuje automatyczne utworzenie klucza podstawowego i klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="f0640-134">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="f0640-135">Te klucze szyfrowania kontroli dostępu tooyour konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f0640-135">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="f0640-136">Usługi BizTalk automatycznie używa hello klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f0640-136">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="f0640-137"><strong>Synchronizowanie kluczy</strong> włączyć tooswitch użytkowników między hello klucz podstawowy i klucz pomocniczy hello bez zakłócania hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-137"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="f0640-138">Na przykład chcesz hello toouse usługi BizTalk nowy klucz podstawowy hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f0640-138">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="f0640-139">toodo to:</span><span class="sxs-lookup"><span data-stu-id="f0640-139">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="f0640-140">Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>.</span><span class="sxs-lookup"><span data-stu-id="f0640-140">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="f0640-141">Wybierz hello klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="f0640-141">Select hello Secondary Key.</span></span> <span data-ttu-id="f0640-142">Po wykonaniu tej czynności hello usługi BizTalk zacznie korzystać hello klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="f0640-142">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="f0640-143">W hello klasycznego portalu Azure wybierz konto magazynu i ponownie wygenerować hello klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f0640-143">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="f0640-144">Należy pamiętać, że usługi BizTalk używa hello klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="f0640-144">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="f0640-145">Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>.</span><span class="sxs-lookup"><span data-stu-id="f0640-145">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="f0640-146">Teraz wybierz hello klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f0640-146">Now, select hello Primary Key.</span></span> <span data-ttu-id="f0640-147">Jest to nowy hello można ponownie wygenerować klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="f0640-147">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="f0640-148">W hello klasycznego portalu Azure wybierz konto magazynu i ponownie wygenerować klucz pomocniczy hello.</span><span class="sxs-lookup"><span data-stu-id="f0640-148">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="f0640-149">Ten proces jest nazywany "przerzucania kluczy".</span><span class="sxs-lookup"><span data-stu-id="f0640-149">This process is called "rollover keys".</span></span> <span data-ttu-id="f0640-150">Celem Hello jest tooenable tooswitch użytkowników między hello klucz podstawowy i klucz pomocniczy hello bez zakłócania hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-150">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="f0640-151"><strong>Usuń</strong> aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0640-151"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="f0640-152">Po wybraniu usunąć usługi BizTalk, a wszystkie tooit wdrożone elementy są usuwane.</span><span class="sxs-lookup"><span data-stu-id="f0640-152">When you select Delete, your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="f0640-153">Pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="f0640-153">Dashboard</span></span>
<span data-ttu-id="f0640-154">W zależności od wersji usługi BizTalk hello wszystkie opcje wymienione mogą nie być dostępne.</span><span class="sxs-lookup"><span data-stu-id="f0640-154">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="f0640-155">Po wybraniu nazwy usługi BizTalk, karta pulpitu nawigacyjnego hello jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="f0640-155">When you select your BizTalk Service name, hello Dashboard tab is displayed.</span></span> <span data-ttu-id="f0640-156">Na pulpicie nawigacyjnym można:</span><span class="sxs-lookup"><span data-stu-id="f0640-156">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a><span data-ttu-id="f0640-157">Przegląd wykorzystania: Pokazuje hello liczbę używanych połączeń hybrydowych</span><span class="sxs-lookup"><span data-stu-id="f0640-157">Usage Overview: Shows hello number of used Hybrid Connections</span></span>
<span data-ttu-id="f0640-158">Wykorzystanie danych hello są również wyświetlane w GB.</span><span class="sxs-lookup"><span data-stu-id="f0640-158">Also displays hello data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="f0640-159">Wykres metryki: Lista stałej metryki wydajności</span><span class="sxs-lookup"><span data-stu-id="f0640-159">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="f0640-160">Te metryki Podaj wartości w czasie rzeczywistym dotyczące kondycji hello hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-160">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="f0640-161">Możesz również hello **względną** lub **bezwzględną** wartości i hello zakres czasu **interwał** hello metryk, które są wyświetlane na wykresie hello.</span><span class="sxs-lookup"><span data-stu-id="f0640-161">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed in hello graph.</span></span> 

<span data-ttu-id="f0640-162">Aby uzyskać opis tych metryk wydajności Przejdź zbyt[dostępne metryki](#Metrics) w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="f0640-162">For a description of these performance metrics, go too[Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="f0640-163">Szybkiego dostępu: Wyświetla listę właściwości usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="f0640-163">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="f0640-164"><strong>Zaktualizuj poświadczenia śledzenia bazy danych</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-164"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="f0640-165">Zmiany hello nazwę użytkownika i hasło używane toolog do hello śledzenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f0640-165">Changes hello user name and password used toolog into hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-166"><strong>Aktualizuj certyfikat protokołu SSL</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-166"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="f0640-167">Można aktualizować hello toouse usługi BizTalk innego certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="f0640-167">Can update hello BizTalk Service toouse a different SSL certificate.</span></span> <span data-ttu-id="f0640-168">Certyfikatu SSL z podpisem własnym jest tworzony automatycznie, gdy użytkownik <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">utworzyć hello usługi BizTalk</a>.</span><span class="sxs-lookup"><span data-stu-id="f0640-168">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create hello BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-169"><strong>Pobierz certyfikat</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-169"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="f0640-170">Możesz pobrać hello certyfikat SSL używany przez komputer lokalny tooa usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-170">You can download hello SSL certificate used by your BizTalk Service tooa local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-171"><strong>Stan</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-171"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="f0640-172">Wyświetla bieżący stan hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-172">Displays hello current status of your BizTalk Service.</span></span> <span data-ttu-id="f0640-173">Zobacz <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">usługi BizTalk Services: Usługa stanu wykresu</a>.</span><span class="sxs-lookup"><span data-stu-id="f0640-173">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="f0640-174"><strong>Adres URL usługi</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-174"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="f0640-175">adres URL Hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-175">hello URL for your BizTalk Service.</span></span> <span data-ttu-id="f0640-176">Jest to samo hello jako hello <strong>adresu URL domeny</strong> wprowadzane podczas tworzenia usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-176">This is hello same as hello <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-177"><strong>Adres publiczny wirtualnego adresu IP (VIP)</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-177"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="f0640-178">adres IP Hello przypisany tooyour usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-178">hello IP address assigned tooyour BizTalk Service.</span></span> <span data-ttu-id="f0640-179">Jest on używany dla wszystkich wejściowych punktów końcowych i jest hello adresu źródłowego dla ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="f0640-179">It is used for all input endpoints and is hello source address for outbound traffic.</span></span> <span data-ttu-id="f0640-180">Ten adres IP należy tooyour usługi BizTalk, pod warunkiem jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="f0640-180">This IP address belongs tooyour BizTalk Service as long as it is created.</span></span> <span data-ttu-id="f0640-181">Jeśli usuniesz hello usługi BizTalk, adres IP hello jest przypisany tooanother usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-181">If you delete hello BizTalk Service, hello IP address is assigned tooanother BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-182"><strong>Namespace ACS</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-182"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="f0640-183">Jest uwierzytelniany w usłudze hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-183">Authenticates with hello BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-184"><strong>Wersja</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-184"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="f0640-185">Wyświetla listę hello wprowadzona w wersji po utworzeniu hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-185">Lists hello Edition entered when hello BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-186"><strong>Lokalizacja</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-186"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="f0640-187">Wyświetla hello region geograficzny, który jest hostem usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-187">Displays hello geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-188"><strong>Utworzone</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-188"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="f0640-189">Hello hello Wyświetla datę i godzinę utworzenia usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-189">Displays hello date and time hello BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-190"><strong>Śledzenie bazy danych</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-190"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="f0640-191">Nazwa bazy danych SQL Azure Hello przechowuje hello śledzenia tabelami używanymi przez usługę BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-191">hello Azure SQL Database name that stores hello tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="f0640-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Wymagania dotyczące poradnik</a> zawiera szczegółowe informacje na powitania śledzenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f0640-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-193"><strong>Monitorowanie archiwizacji magazynu</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-193"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="f0640-194">Hello nazwę konta magazynu Azure, która przechowuje hello monitorowania danych wyjściowych usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-194">hello Azure Storage account name that stores hello monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="f0640-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Wymagania dotyczące poradnik</a> zawiera szczegółowe informacje na powitania konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f0640-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-196"><strong>Nazwa subskrypcji</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-196"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="f0640-197">Wyświetla listę subskrypcji hello, który jest hostem usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-197">Lists hello subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="f0640-198">Subskrypcja Hello reguluje toohello dostępu do klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f0640-198">hello subscription governs access toohello Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-199"><strong>Identyfikator subskrypcji</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-199"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="f0640-200">Identyfikator subskrypcji jest generowany automatycznie podczas tworzenia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f0640-200">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="f0640-201">Podczas korzystania z interfejsów API REST, może być konieczne hello tooenter identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f0640-201">When using REST APIs, you may need tooenter hello Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="f0640-202">[Usługi BizTalk Services: Inicjowanie obsługi administracyjnej klasycznego portalu Azure za pomocą](http://go.microsoft.com/fwlink/p/?LinkID=302280) list hello toocreate kroki usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-202">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists hello steps toocreate a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a><span data-ttu-id="f0640-203">Zarządzanie, informacje o połączeniu, klucze synchronizacji i Usuń na pasku zadań hello:</span><span class="sxs-lookup"><span data-stu-id="f0640-203">Manage, Connection Information, Sync Keys, and Delete in hello task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="f0640-204"><strong>Zarządzanie</strong> wdrażania aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0640-204"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="f0640-205">Otwiera hello Azure Portal usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-205">Opens hello Azure BizTalk Services Portal.</span></span> <span data-ttu-id="f0640-206">Portal usługi BizTalk Hello jest hello wejściu tooEDI konfiguracji, w tym dodawanie partnerami i tworzenie X12, AS2 oraz umów EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="f0640-206">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="f0640-207">To jest identyczny hello <strong>Tworzenie umów z partnerami</strong> na powitania <strong>Szybki Start</strong> kartę.</span><span class="sxs-lookup"><span data-stu-id="f0640-207">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="f0640-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Konfigurowanie składników EDI obsługi wiadomości w portalu usługi BizTalk</a> zamieszczono więcej informacji dotyczących hello Portal usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-209"><strong>Informacje o połączeniu</strong> z hello Namespace kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="f0640-209"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="f0640-210">Wyświetla hello Namespace kontroli dostępu, domyślne wystawcy i klucza domyślne wartości. które mogą zostać skopiowane.</span><span class="sxs-lookup"><span data-stu-id="f0640-210">Displays hello Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="f0640-211">Można również otworzyć hello portalu kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="f0640-211">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="f0640-212">Ten Portal kontroli dostępu jest hello taki sam jak przy użyciu opcji usługi Active Directory hello w okienku nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="f0640-212">This Access Control Portal is hello same as using hello Active Directory option in hello left navigation pane.</span></span>
<br/><br/><span data-ttu-id="f0640-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Zarządzanie Your Namespace ACS</a> zamieszczono więcej informacji dotyczących hello portalu kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="f0640-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-214"><strong>Synchronizowanie kluczy</strong> w hello konta magazynu</span><span class="sxs-lookup"><span data-stu-id="f0640-214"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="f0640-215">Podczas tworzenia konta usługi Storage następuje automatyczne utworzenie klucza podstawowego i klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="f0640-215">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="f0640-216">Te klucze szyfrowania kontroli dostępu tooyour konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f0640-216">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="f0640-217">Usługi BizTalk automatycznie używa hello klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f0640-217">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="f0640-218"><strong>Synchronizowanie kluczy</strong> włączyć tooswitch użytkowników między hello klucz podstawowy i klucz pomocniczy hello bez zakłócania hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-218"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="f0640-219">Na przykład chcesz hello toouse usługi BizTalk nowy klucz podstawowy hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f0640-219">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="f0640-220">toodo to:</span><span class="sxs-lookup"><span data-stu-id="f0640-220">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="f0640-221">Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>.</span><span class="sxs-lookup"><span data-stu-id="f0640-221">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="f0640-222">Wybierz hello klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="f0640-222">Select hello Secondary Key.</span></span> <span data-ttu-id="f0640-223">Po wykonaniu tej czynności hello usługi BizTalk zacznie korzystać hello klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="f0640-223">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="f0640-224">W hello klasycznego portalu Azure wybierz konto magazynu i ponownie wygenerować hello klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f0640-224">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="f0640-225">Należy pamiętać, że usługi BizTalk używa hello klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="f0640-225">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="f0640-226">Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>.</span><span class="sxs-lookup"><span data-stu-id="f0640-226">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="f0640-227">Teraz wybierz hello klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f0640-227">Now, select hello Primary Key.</span></span> <span data-ttu-id="f0640-228">Jest to nowy hello można ponownie wygenerować klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="f0640-228">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="f0640-229">W hello klasycznego portalu Azure wybierz konto magazynu i ponownie wygenerować klucz pomocniczy hello.</span><span class="sxs-lookup"><span data-stu-id="f0640-229">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="f0640-230">Ten proces jest nazywany "przerzucania kluczy".</span><span class="sxs-lookup"><span data-stu-id="f0640-230">This process is called "rollover keys".</span></span> <span data-ttu-id="f0640-231">Celem Hello jest tooenable tooswitch użytkowników między hello klucz podstawowy i klucz pomocniczy hello bez zakłócania hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-231">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="f0640-232"><strong>Usuń</strong> aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0640-232"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="f0640-233">Usługi BizTalk i wszystkie tooit wdrożone elementy zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="f0640-233">Your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="f0640-234">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="f0640-234">Monitor</span></span>
<span data-ttu-id="f0640-235">Nie ma zastosowania toohello bezpłatna wersja.</span><span class="sxs-lookup"><span data-stu-id="f0640-235">Does not apply toohello Free Edition.</span></span>

<span data-ttu-id="f0640-236">Po wybraniu nazwy usługi BizTalk kartę Monitor hello jest dostępny i wyświetla następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f0640-236">When you select your BizTalk Service name, hello Monitor tab is available and displays hello following:</span></span>

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a><span data-ttu-id="f0640-237">Wykres metryki: Hello Wyświetla wybrany metryki wydajności</span><span class="sxs-lookup"><span data-stu-id="f0640-237">Metric Graph: Displays hello selected performance metrics</span></span>
<span data-ttu-id="f0640-238">Te metryki Podaj wartości w czasie rzeczywistym dotyczące kondycji hello hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-238">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="f0640-239">Możesz wybrać metryki wydajności, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="f0640-239">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="f0640-240">Maksymalnie sześć metryki wydajności mogą być jednocześnie wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="f0640-240">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="f0640-241">Możesz również hello **względną** lub **bezwzględną** wartości i hello zakres czasu **interwał** hello metryk, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="f0640-241">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed.</span></span> 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a><span data-ttu-id="f0640-242">metryki tooremove lub wyświetlany na wykresie hello:</span><span class="sxs-lookup"><span data-stu-id="f0640-242">tooremove or display metrics in hello graph:</span></span>
1. <span data-ttu-id="f0640-243">Wybierz hello **Monitor** kartę.</span><span class="sxs-lookup"><span data-stu-id="f0640-243">Select hello **Monitor** tab.</span></span>
2. <span data-ttu-id="f0640-244">Wybierz **dodać metryki** na pasku zadań hello:</span><span class="sxs-lookup"><span data-stu-id="f0640-244">Select **Add Metrics** in hello task bar:</span></span>  
   <span data-ttu-id="f0640-245">![Wybierz opcję Dodaj metryk][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="f0640-245">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="f0640-246">Sprawdź metryki wydajności hello ma toodisplay.</span><span class="sxs-lookup"><span data-stu-id="f0640-246">Check hello performance metrics you want toodisplay.</span></span>
4. <span data-ttu-id="f0640-247">Wybierz hello znacznikiem wyboru tooreturn toohello **Monitor** kartę.</span><span class="sxs-lookup"><span data-stu-id="f0640-247">Select hello checkmark tooreturn toohello **Monitor** tab.</span></span>
5. <span data-ttu-id="f0640-248">Wybierz hello koło dalej toohello metryki toodisplay wartość tej metryki hello wykresie.</span><span class="sxs-lookup"><span data-stu-id="f0640-248">Select hello circle next toohello metric toodisplay that metric's value in hello graph.</span></span>  
   
    <span data-ttu-id="f0640-249">Na przykład Witaj **użycie procesora CPU** metryka jest wyszarzona; dane wyjściowe nie jest wyświetlany na wykresie hello:</span><span class="sxs-lookup"><span data-stu-id="f0640-249">For example, hello **CPU Usage** metric is grayed out; its output is not displayed in hello graph:</span></span>  
   <span data-ttu-id="f0640-250">![Metryki użycia procesora CPU jest szary.][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="f0640-250">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="f0640-251">Wybierz hello wygaszone hello tooenable koło **użycie procesora CPU** metryki toodisplay dane wyjściowe w grafie hello:</span><span class="sxs-lookup"><span data-stu-id="f0640-251">Select hello grayed out circle tooenable hello **CPU Usage** metric toodisplay its output in hello graph:</span></span>  
   <span data-ttu-id="f0640-252">![Metryki użycia procesora CPU jest włączona.][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="f0640-252">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="f0640-253">Wybierz tooremove Metryka z hello wyświetlania wykresu i listy hello **usunąć Metryka** na pasku zadań hello.</span><span class="sxs-lookup"><span data-stu-id="f0640-253">tooremove a metric from hello display graph and hello list, select **Delete Metric** in hello task bar.</span></span> <span data-ttu-id="f0640-254">tooadd hello metryki toohello wstecz listy, wybierz **dodać metryki** na pasku zadań hello, sprawdź hello metryki i wybierz hello znacznikiem wyboru tooreturn toohello **Monitor** kartę. Wybierz hello wygaszone koło tooenable hello metryki.</span><span class="sxs-lookup"><span data-stu-id="f0640-254">tooadd hello metric back toohello list, select **Add Metrics** in hello task bar, check hello metric, and select hello checkmark tooreturn toohello **Monitor** tab. Select hello grayed out circle tooenable hello metric.</span></span>

## <span data-ttu-id="f0640-255"><a name="Metrics"></a>Dostępne metryki</span><span class="sxs-lookup"><span data-stu-id="f0640-255"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="f0640-256">Witaj następujące metryki liczniki wydajności są dostępne:</span><span class="sxs-lookup"><span data-stu-id="f0640-256">hello following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="f0640-257"><strong>Opóźnienie RountdTrip</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-257"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="f0640-258">Wyświetla hello Średni czas w milisekundach (ms) tooprocess, otrzymany komunikat z wiadomość hello czasu powitania dopóki wiadomość hello pełni jest przetwarzany przez hello usługi BizTalk we wszystkich mostków.</span><span class="sxs-lookup"><span data-stu-id="f0640-258">Displays hello average time taken in milliseconds (ms) tooprocess a message from hello time hello message is received until hello message is fully processed by hello BizTalk Service across all bridges.</span></span> <span data-ttu-id="f0640-259">Zliczane są tylko pomyślnie przetworzonych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="f0640-259">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="f0640-260">Gdy występują następujące zdarzenia hello, tworzona jest sygnatura czasowa:</span><span class="sxs-lookup"><span data-stu-id="f0640-260">When hello following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="f0640-261">Komunikat wprowadza hello bramy</span><span class="sxs-lookup"><span data-stu-id="f0640-261">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="f0640-262">Komunikat jest miejscem docelowym toohello routingiem</span><span class="sxs-lookup"><span data-stu-id="f0640-262">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="f0640-263">Miejsce docelowe odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f0640-263">Destination response is received</span></span></li>
<li><span data-ttu-id="f0640-264">Docelowy potwierdzenia odpowiedzi wysłanych toohello bramy</span><span class="sxs-lookup"><span data-stu-id="f0640-264">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="f0640-265">Ta metryka przedstawia wynik hello hello następujące obliczenie:</span><span class="sxs-lookup"><span data-stu-id="f0640-265">This metric shows hello result of hello following calculation:</span></span>
<br/><br/>
<span data-ttu-id="f0640-266">[Docelowy potwierdzenia odpowiedzi wysłanych toohello brama] - [hello brama wprowadza wiadomości]</span><span class="sxs-lookup"><span data-stu-id="f0640-266">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-267"><strong>Błędy w źródle</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-267"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="f0640-268">Wyświetla hello całkowita liczba komunikatów, których nie powiodła się przez hello usługi BizTalk, gdy ściąganie wiadomości z punktów końcowych źródła hello.</span><span class="sxs-lookup"><span data-stu-id="f0640-268">Displays hello total number of messages that failed by hello BizTalk Service when pulling messages from hello source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-269"><strong>Użycie procesora CPU</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-269"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="f0640-270">Wyświetla listę hello średni procent czasu procesora wszystkich wystąpień ról.</span><span class="sxs-lookup"><span data-stu-id="f0640-270">Lists hello average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-271"><strong>Opóźnienie przetwarzania</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-271"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="f0640-272">Wyświetla średni czas hello w milisekundach (ms) tooprocess wiadomości przez hello usługi BizTalk we wszystkich mostków, z wyłączeniem czasu hello spędzony w miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="f0640-272">Displays hello average time taken In milliseconds (ms) tooprocess a message by hello BizTalk Service across all bridges, excluding hello time spent in destinations.</span></span> <span data-ttu-id="f0640-273">Zliczane są tylko pomyślnie przetworzonych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="f0640-273">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="f0640-274">Po każdym hello następujące zdarzenia, tworzona jest sygnatura czasowa:</span><span class="sxs-lookup"><span data-stu-id="f0640-274">When each of hello following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="f0640-275">Komunikat wprowadza hello bramy</span><span class="sxs-lookup"><span data-stu-id="f0640-275">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="f0640-276">Komunikat jest miejscem docelowym toohello routingiem</span><span class="sxs-lookup"><span data-stu-id="f0640-276">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="f0640-277">Miejsce docelowe odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f0640-277">Destination response is received</span></span></li>
<li><span data-ttu-id="f0640-278">Docelowy potwierdzenia odpowiedzi wysłanych toohello bramy</span><span class="sxs-lookup"><span data-stu-id="f0640-278">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/><span data-ttu-id="f0640-279">Ta metryka przedstawia wynik hello hello następujące obliczenie:</span><span class="sxs-lookup"><span data-stu-id="f0640-279">This metric shows hello result of hello following calculation:</span></span><br/><br/>
<span data-ttu-id="f0640-280">[Docelowy potwierdzenia odpowiedzi wysłanych toohello brama] - [komunikat wprowadza bramy hello] - [docelowy odpowiedzi] + [wiadomość jest miejscem docelowym routingiem toohello]</span><span class="sxs-lookup"><span data-stu-id="f0640-280">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway] - [Destination response is received] + [Message is routed toohello destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-281"><strong>Błędy w procesie</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-281"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="f0640-282">Wyświetla hello całkowita liczba komunikatów, których nie powiodła się podczas przetwarzania przez hello usługi BizTalk we wszystkich mostków hello w interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="f0640-282">Displays hello total number of messages that failed during processing by hello BizTalk Service across all hello bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-283"><strong>Komunikaty wysyłane</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-283"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="f0640-284">Wyświetla hello całkowitą liczbę komunikatów wysłanych przez hello usługi BizTalk we wszystkich mostków w interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="f0640-284">Displays hello total number of messages sent by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="f0640-285">Ta metryka jest zwiększany, gdy komunikat wysłany z potokiem osiągnie hello docelowy trasy.</span><span class="sxs-lookup"><span data-stu-id="f0640-285">This metric is incremented when a message sent from a pipeline reaches hello route destination.</span></span> <span data-ttu-id="f0640-286">Ta metryka nie wskazuje, że wiadomość jest pomyślnie przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="f0640-286">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="f0640-287">W scenariuszu "żądanie-odpowiedź" hello metryka jest zwiększany po docelowy trasy hello wysyła potoku wstecz toohello potwierdzenia otrzymania.</span><span class="sxs-lookup"><span data-stu-id="f0640-287">In a Request-Reply scenario, hello metric is incremented when hello route destination sends a receipt acknowledgement back toohello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-288"><strong>Odebrane wiadomości</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-288"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="f0640-289">Wyświetla hello całkowitą liczbę komunikatów odebranych przez hello usługi BizTalk we wszystkich mostków w interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="f0640-289">Displays hello total number of messages received by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="f0640-290">Ta metryka jest zwiększany, gdy nowy komunikat jest odbierany przez hello potoku.</span><span class="sxs-lookup"><span data-stu-id="f0640-290">This metric is incremented when a new message is received by hello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-291"><strong>Komunikaty w procesie</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-291"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="f0640-292">Wyświetla hello całkowita liczba aktualnie przetwarzanych przez usługę BizTalk hello w interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="f0640-292">Displays hello total number of messages currently being processed by hello BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0640-293"><strong>Liczba przetworzonych komunikatów</strong></span><span class="sxs-lookup"><span data-stu-id="f0640-293"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="f0640-294">Wyświetla hello całkowita liczba komunikatów pomyślnie przetworzone przez hello usługi BizTalk we wszystkich mostków w interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="f0640-294">Displays hello total number of messages successfully processed by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="f0640-295">Ta metryka jest zwiększany, gdy wiadomość została odebrana pomyślnie hello potok i docelowym toohello pomyślnie routingiem.</span><span class="sxs-lookup"><span data-stu-id="f0640-295">This metric is incremented when a message is successfully received by hello pipeline and successfully routed toohello destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="f0640-296">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="f0640-296">Scale</span></span>
<span data-ttu-id="f0640-297">Na karcie skali hello można dodać lub odjąć hello liczbę jednostek używanych przez usługę BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-297">In hello Scale tab, you can add or subtract hello number of units used by your BizTalk Service.</span></span> <span data-ttu-id="f0640-298">Domyślnie istnieje skonfigurowane jednostki.</span><span class="sxs-lookup"><span data-stu-id="f0640-298">By default, there is one Unit configured.</span></span> <span data-ttu-id="f0640-299">Dodatkowe jednostki można dodać tooscale usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="f0640-299">Additional Units can be added tooscale your BizTalk Service.</span></span> <span data-ttu-id="f0640-300">Zwiększenie skali hello są zwiększyć przepustowość.</span><span class="sxs-lookup"><span data-stu-id="f0640-300">When you increase hello scale, you are increasing throughput.</span></span> <span data-ttu-id="f0640-301">Witaj ilość zasobów zwiększa także, tym mostków wdrożone, umowy, LOB połączeń i mocy obliczeniowej.</span><span class="sxs-lookup"><span data-stu-id="f0640-301">hello amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="f0640-302">Na przykład można zwiększyć hello skali od 1 jednostki too2 jednostki.</span><span class="sxs-lookup"><span data-stu-id="f0640-302">For example, you increase hello scale from 1 Unit too2 Units.</span></span> <span data-ttu-id="f0640-303">W takiej sytuacji można wdrożyć hello dwa razy liczba mostków, double umów hello double hello LOB połączeń i mocy obliczeniowej hello dwa razy.</span><span class="sxs-lookup"><span data-stu-id="f0640-303">In this situation, you can deploy double hello number of bridges, double hello agreements, double hello LOB connections, and double hello processing power.</span></span>

<span data-ttu-id="f0640-304">Niektóre wersje BizTalk nie oferują opcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="f0640-304">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="f0640-305">W takim przypadku jednostki jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="f0640-305">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="f0640-306">toodetermine liczbę jednostek, które mogą być skalowane posiadanej wersji, zobacz zbyt[usługi BizTalk Services: wersje wykresu](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="f0640-306">toodetermine how many units your edition can be scaled, refer too[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="f0640-307">Zwiększenie liczby hello jednostek może mieć wpływ cennik.</span><span class="sxs-lookup"><span data-stu-id="f0640-307">Increasing hello number of units may impact pricing.</span></span> <span data-ttu-id="f0640-308">Jeśli zwiększysz hello jednostki, wybierając **zapisać** zostanie wyświetlony komunikat informujący o tym, jeśli jest wpływ na rozliczenia.</span><span class="sxs-lookup"><span data-stu-id="f0640-308">If you increase hello Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="f0640-309">Następnie wybierz toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f0640-309">You then choose toocontinue.</span></span> <span data-ttu-id="f0640-310">Wraz ze zwiększeniem hello liczbę jednostek hello stan usługi BizTalk zmienia Active tooUpdating.</span><span class="sxs-lookup"><span data-stu-id="f0640-310">When you increase hello number of Units, hello BizTalk Service status changes from Active tooUpdating.</span></span> <span data-ttu-id="f0640-311">W hello aktualizacji stanu usługi BizTalk nadal toorun.</span><span class="sxs-lookup"><span data-stu-id="f0640-311">In hello Updating state, your BizTalk Service continues toorun.</span></span>

<span data-ttu-id="f0640-312">[Usługi BizTalk Services: Wersje wykresu](biztalk-editions-feature-chart.md) definiuje "Jednostki".</span><span class="sxs-lookup"><span data-stu-id="f0640-312">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="f0640-313">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="f0640-313">Configure</span></span>
<span data-ttu-id="f0640-314">Nie dotyczy połączeń tooHybrid.</span><span class="sxs-lookup"><span data-stu-id="f0640-314">Does not apply tooHybrid Connections.</span></span>

<span data-ttu-id="f0640-315">Ustawia hello tooNone stanu kopii zapasowej lub automatyczne.</span><span class="sxs-lookup"><span data-stu-id="f0640-315">Sets hello Backup Status tooNone or Automatic.</span></span> <span data-ttu-id="f0640-316">Po ustawieniu tooNone, nie ma kopii zapasowych są tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="f0640-316">When set tooNone, no backups are automatically created.</span></span> <span data-ttu-id="f0640-317">Po ustawieniu tooAutomatic, skonfiguruj hello lokalizacji kopii zapasowej, częstotliwość hello hello kopii zapasowej i jak długo pliki kopii zapasowej hello tookeep.</span><span class="sxs-lookup"><span data-stu-id="f0640-317">When set tooAutomatic, you configure hello backup location, hello frequency of hello backup, and how long tookeep hello backup files.</span></span> 

<span data-ttu-id="f0640-318">[Usługi BizTalk Services: Kopia zapasowa i przywracanie](biztalk-backup-restore.md) hello szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="f0640-318">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides hello details.</span></span> 

## <span data-ttu-id="f0640-319"><a name="HybridConnections"></a>Połączenia hybrydowe</span><span class="sxs-lookup"><span data-stu-id="f0640-319"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="f0640-320">Połączenia hybrydowe umożliwiają łączenie aplikacji Azure, takich jak aplikacje sieci Web lub aplikacji mobilnych w usłudze Azure App Service, zasób lokalną tooan, który używa portu TCP statycznego, takich jak SQL Server, MySQL, interfejsów API sieci Web HTTP i najbardziej niestandardowych usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f0640-320">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, tooan on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="f0640-321">Usługi BizTalk Services zarządzania połączeń hybrydowych w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f0640-321">Hybrid Connections are managed in  BizTalk Services in hello Azure classic portal.</span></span>

<span data-ttu-id="f0640-322">toocreate połączeń hybrydowych w usłudze Azure App Service, zobacz [dostępu do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f0640-322">toocreate Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="f0640-323">toocreate lub zarządzać połączeń hybrydowych w usłudze Azure BizTalk Services, zobacz [połączeń hybrydowych](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f0640-323">toocreate or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="f0640-324">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0640-324">Next</span></span>
<span data-ttu-id="f0640-325">Teraz, kiedy znasz różnych kartach zawierających hello, możesz dowiedzieć się więcej funkcji usług BizTalk Azure hello:</span><span class="sxs-lookup"><span data-stu-id="f0640-325">Now that you're familiar with hello different tabs, you can learn more about hello Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="f0640-326">BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)</span><span class="sxs-lookup"><span data-stu-id="f0640-326">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="f0640-327">BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)</span><span class="sxs-lookup"><span data-stu-id="f0640-327">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="f0640-328">BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)</span><span class="sxs-lookup"><span data-stu-id="f0640-328">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="f0640-329">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f0640-329">See Also</span></span>
* [<span data-ttu-id="f0640-330">Połączenia hybrydowe</span><span class="sxs-lookup"><span data-stu-id="f0640-330">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="f0640-331">Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu</span><span class="sxs-lookup"><span data-stu-id="f0640-331">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="f0640-332">Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="f0640-332">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="f0640-333">Usługi BizTalk Services: Stan usługi BizTalk wykresu</span><span class="sxs-lookup"><span data-stu-id="f0640-333">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="f0640-334">Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="f0640-334">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

