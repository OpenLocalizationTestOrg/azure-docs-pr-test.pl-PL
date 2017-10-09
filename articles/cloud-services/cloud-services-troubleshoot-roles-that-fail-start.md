---
title: "aaaTroubleshoot ról, które nie są toostart | Dokumentacja firmy Microsoft"
description: "Poniżej przedstawiono niektóre typowe przyczyny, dlaczego roli usługi w chmurze może się nie powieść toostart. Podawane są również rozwiązania toothese problemów."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a><span data-ttu-id="0fc20-104">Rozwiązywanie problemów z ról usługi w chmurze, które nie są toostart</span><span class="sxs-lookup"><span data-stu-id="0fc20-104">Troubleshoot Cloud Service roles that fail toostart</span></span>
<span data-ttu-id="0fc20-105">Poniżej przedstawiono niektóre typowe problemy i rozwiązania pokrewne tooAzure usługi w chmurze ról, które się nie powieść toostart.</span><span class="sxs-lookup"><span data-stu-id="0fc20-105">Here are some common problems and solutions related tooAzure Cloud Services roles that fail toostart.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="0fc20-106">Brak biblioteki DLL lub zależności</span><span class="sxs-lookup"><span data-stu-id="0fc20-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="0fc20-107">Odpowiadać oraz ról, które są cykliczne między **inicjowanie**, **zajęty**, i **zatrzymywanie** stanów może być spowodowany brakiem biblioteki DLL lub zestawów.</span><span class="sxs-lookup"><span data-stu-id="0fc20-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="0fc20-108">Objawy Brak biblioteki DLL lub zestawy mogą być:</span><span class="sxs-lookup"><span data-stu-id="0fc20-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="0fc20-109">Wystąpienie roli jest okrągło **inicjowanie**, **zajęty**, i **zatrzymywanie** stanów.</span><span class="sxs-lookup"><span data-stu-id="0fc20-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="0fc20-110">Wystąpienie roli przeniósł zbyt**gotowe** , ale w przypadku przejścia aplikacji sieci web tooyour hello strona nie jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="0fc20-110">Your role instance has moved too**Ready** but if you navigate tooyour web application, hello page does not appear.</span></span>

<span data-ttu-id="0fc20-111">Istnieje kilka metod zalecane do badania tych problemów.</span><span class="sxs-lookup"><span data-stu-id="0fc20-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="0fc20-112">Diagnozowanie Brak problemów biblioteki DLL w roli sieć web</span><span class="sxs-lookup"><span data-stu-id="0fc20-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="0fc20-113">Po przejściu tooa witryny sieci Web, które zostało wdrożone w roli sieci web, hello przeglądarka wyświetla serwera błąd podobny toohello następujące, może to oznaczać brak biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="0fc20-113">When you navigate tooa website that is deployed in a web role, and hello browser displays a server error similar toohello following, it may indicate that a DLL is missing.</span></span>

![Błąd serwera w "/" aplikacji.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="0fc20-115">Diagnozowanie problemów przez wyłączenie błędów niestandardowych</span><span class="sxs-lookup"><span data-stu-id="0fc20-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="0fc20-116">Bardziej szczegółowy informacje o błędzie mogą zostać przejrzane przez konfigurowanie hello web.config dla roli sieci web hello tooset tooOff tryb błędów niestandardowych hello ani ponownego wdrażania hello usługi.</span><span class="sxs-lookup"><span data-stu-id="0fc20-116">More complete error information can be viewed by configuring hello web.config for hello web role tooset hello custom error mode tooOff and redeploying hello service.</span></span>

<span data-ttu-id="0fc20-117">tooview Wypełnij więcej błędy bez przy użyciu pulpitu zdalnego:</span><span class="sxs-lookup"><span data-stu-id="0fc20-117">tooview more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="0fc20-118">Otwórz rozwiązanie hello w programie Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0fc20-118">Open hello solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="0fc20-119">W hello **Eksploratora rozwiązań**, Znajdź plik web.config hello i otwórz go.</span><span class="sxs-lookup"><span data-stu-id="0fc20-119">In hello **Solution Explorer**, locate hello web.config file and open it.</span></span>
3. <span data-ttu-id="0fc20-120">W pliku web.config hello zlokalizować sekcji system.web hello i Dodaj powitania po wierszu:</span><span class="sxs-lookup"><span data-stu-id="0fc20-120">In hello web.config file, locate hello system.web section and add hello following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="0fc20-121">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="0fc20-121">Save hello file.</span></span>
5. <span data-ttu-id="0fc20-122">Spakuj ponownie i ponownie wdrożyć usługę hello.</span><span class="sxs-lookup"><span data-stu-id="0fc20-122">Repackage and redeploy hello service.</span></span>

<span data-ttu-id="0fc20-123">Gdy jest ponownie wdrożyć usługę hello, zostanie wyświetlony komunikat o błędzie, nazwą hello hello brakuje zestawu lub biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="0fc20-123">Once hello service is redeployed, you will see an error message with hello name of hello missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a><span data-ttu-id="0fc20-124">Diagnozowanie problemów poprzez wyświetlenie błędu hello zdalnie</span><span class="sxs-lookup"><span data-stu-id="0fc20-124">Diagnose issues by viewing hello error remotely</span></span>
<span data-ttu-id="0fc20-125">Możesz za pomocą roli hello tooaccess pulpitu zdalnego i wyświetlić więcej informacji o zdalnie.</span><span class="sxs-lookup"><span data-stu-id="0fc20-125">You can use Remote Desktop tooaccess hello role and view more complete error information remotely.</span></span> <span data-ttu-id="0fc20-126">Użyj hello następujące błędy hello tooview czynności przy użyciu pulpitu zdalnego:</span><span class="sxs-lookup"><span data-stu-id="0fc20-126">Use hello following steps tooview hello errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="0fc20-127">Upewnij się, że Azure SDK 1.3 lub nowszy jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="0fc20-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="0fc20-128">Podczas wdrażania hello hello rozwiązania przy użyciu programu Visual Studio, wybierz za "Konfigurowanie pulpitu zdalnego połączeń...".</span><span class="sxs-lookup"><span data-stu-id="0fc20-128">During hello deployment of hello solution by using Visual Studio, choose too“Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="0fc20-129">Aby uzyskać więcej informacji na temat konfigurowania hello Podłączanie pulpitu zdalnego, zobacz [za pomocą pulpitu zdalnego z rolami Azure](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0fc20-129">For more information on configuring hello Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="0fc20-130">W hello Microsoft klasycznego portalu Azure, po wystąpieniu hello wskazuje stan **gotowe**, kliknij jeden z hello wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="0fc20-130">In hello Microsoft Azure classic portal, once hello instance shows a status of **Ready**, click one of hello role instances.</span></span>
4. <span data-ttu-id="0fc20-131">Kliknij przycisk hello **Connect** ikonę w hello **dostępu zdalnego** obszaru hello wstążki.</span><span class="sxs-lookup"><span data-stu-id="0fc20-131">Click hello **Connect** icon in hello **Remote Access** area of hello ribbon.</span></span>
5. <span data-ttu-id="0fc20-132">Zaloguj przy użyciu poświadczeń hello, które zostały określone podczas konfigurowania usług pulpitu zdalnego hello toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0fc20-132">Sign in toohello virtual machine by using hello credentials that were specified during hello Remote Desktop configuration.</span></span>
6. <span data-ttu-id="0fc20-133">Otwórz okno poleceń.</span><span class="sxs-lookup"><span data-stu-id="0fc20-133">Open a command window.</span></span>
7. <span data-ttu-id="0fc20-134">Wpisz polecenie `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="0fc20-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="0fc20-135">Zanotuj wartość adres IPV4 hello.</span><span class="sxs-lookup"><span data-stu-id="0fc20-135">Note hello IPV4 Address value.</span></span>
9. <span data-ttu-id="0fc20-136">Otwórz program Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="0fc20-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="0fc20-137">Wpisz adres hello i nazwa hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0fc20-137">Type hello address and hello name of hello web application.</span></span> <span data-ttu-id="0fc20-138">Na przykład `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="0fc20-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="0fc20-139">Nawigowanie po toohello witryny sieci Web zwróci teraz dokładniejsze komunikaty o błędach:</span><span class="sxs-lookup"><span data-stu-id="0fc20-139">Navigating toohello website will now return more explicit error messages:</span></span>

* <span data-ttu-id="0fc20-140">Błąd serwera w "/" aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0fc20-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="0fc20-141">Opis: Wystąpił nieobsługiwany wyjątek podczas wykonywania bieżącego żądania sieci web hello hello.</span><span class="sxs-lookup"><span data-stu-id="0fc20-141">Description: An unhandled exception occurred during hello execution of hello current web request.</span></span> <span data-ttu-id="0fc20-142">Przejrzyj ślad stosu hello, aby uzyskać więcej informacji o błędzie hello i miejscu jego występowania w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="0fc20-142">Please review hello stack trace for more information about hello error and where it originated in hello code.</span></span>
* <span data-ttu-id="0fc20-143">Szczegóły wyjątku: System.IO.FIleNotFoundException: nie można załadować pliku lub zestawu "Microsoft.WindowsAzure.StorageClient, wersja = 1.1.0.0, Culture = neutral, PublicKeyToken = 31bf856ad364e35" lub jednej z jego zależności.</span><span class="sxs-lookup"><span data-stu-id="0fc20-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="0fc20-144">Witaj, system nie może odnaleźć określonego pliku hello.</span><span class="sxs-lookup"><span data-stu-id="0fc20-144">hello system cannot find hello file specified.</span></span>

<span data-ttu-id="0fc20-145">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0fc20-145">For example:</span></span>

![Błąd serwera jawne w '/' aplikacji](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a><span data-ttu-id="0fc20-147">Diagnozowanie problemów przy użyciu emulatora obliczeń hello</span><span class="sxs-lookup"><span data-stu-id="0fc20-147">Diagnose issues by using hello compute emulator</span></span>
<span data-ttu-id="0fc20-148">Można użyć toodiagnose emulatora obliczeń hello w Microsoft Azure i rozwiązywanie problemów z brakujących zależności i błędy w pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="0fc20-148">You can use hello Microsoft Azure compute emulator toodiagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="0fc20-149">Aby uzyskać najlepsze wyniki za pomocą tej metody diagnostyki należy używać komputer lub maszynę wirtualną, która ma czystą instalację systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0fc20-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="0fc20-150">toobest symulować hello środowiska platformy Azure, należy użyć systemu Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="0fc20-150">toobest simulate hello Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="0fc20-151">Zainstaluj wersję autonomicznej hello hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0fc20-151">Install hello standalone version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="0fc20-152">Na komputerze deweloperskim hello kompilacji hello projekt usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0fc20-152">On hello development machine, build hello cloud service project.</span></span>
3. <span data-ttu-id="0fc20-153">W Eksploratorze Windows przejdź folderu bin\debug toohello hello projekt usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0fc20-153">In Windows Explorer, navigate toohello bin\debug folder of hello cloud service project.</span></span>
4. <span data-ttu-id="0fc20-154">Skopiuj folder csx hello i komputera toohello pliku .cscfg używasz toodebug hello problemy.</span><span class="sxs-lookup"><span data-stu-id="0fc20-154">Copy hello .csx folder and .cscfg file toohello computer that you are using toodebug hello issues.</span></span>
5. <span data-ttu-id="0fc20-155">Na powitania oczyszczania komputera, Otwórz okno wiersza polecenia Azure SDK i wpisz `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="0fc20-155">On hello clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="0fc20-156">Wpisz w wierszu polecenia hello `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="0fc20-156">At hello command prompt, type `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="0fc20-157">Po uruchomieniu roli hello, zobaczysz szczegółowe informacje o błędzie w programie Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="0fc20-157">When hello role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="0fc20-158">Można również użyć standardowego systemu Windows, narzędzia do rozwiązywania problemów toofurther zdiagnozować hello problem.</span><span class="sxs-lookup"><span data-stu-id="0fc20-158">You can also use standard Windows troubleshooting tools toofurther diagnose hello problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="0fc20-159">Diagnozowanie problemów przy użyciu funkcji IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="0fc20-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="0fc20-160">Dla procesu roboczego oraz role sieci web, które używają programu .NET Framework 4, możesz użyć [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), która jest dostępna w programie Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0fc20-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="0fc20-161">Wykonaj te kroki toodeploy hello usługi przy użyciu funkcji IntelliTrace włączone:</span><span class="sxs-lookup"><span data-stu-id="0fc20-161">Follow these steps toodeploy hello service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="0fc20-162">Potwierdź, że zestaw Azure SDK 1.3 lub nowszej jest zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="0fc20-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="0fc20-163">Wdrażanie rozwiązania hello przy użyciu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0fc20-163">Deploy hello solution by using Visual Studio.</span></span> <span data-ttu-id="0fc20-164">Podczas wdrażania, sprawdź hello **włączenia funkcji IntelliTrace dla ról platformy .NET 4** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="0fc20-164">During deployment, check hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="0fc20-165">Po uruchomieniu wystąpienia hello Otwórz hello **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="0fc20-165">Once hello instance starts, open hello **Server Explorer**.</span></span>
4. <span data-ttu-id="0fc20-166">Rozwiń węzeł hello **Azure\\usługi w chmurze** węzła i Znajdź hello wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="0fc20-166">Expand hello **Azure\\Cloud Services** node and locate hello deployment.</span></span>
5. <span data-ttu-id="0fc20-167">Rozwiń hello wdrożenia do momentu wyświetlenia hello wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="0fc20-167">Expand hello deployment until you see hello role instances.</span></span> <span data-ttu-id="0fc20-168">Kliknij prawym przyciskiem myszy na jednym z wystąpień hello.</span><span class="sxs-lookup"><span data-stu-id="0fc20-168">Right-click on one of hello instances.</span></span>
6. <span data-ttu-id="0fc20-169">Wybierz **dzienniki IntelliTrace widoku**.</span><span class="sxs-lookup"><span data-stu-id="0fc20-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="0fc20-170">Witaj **Podsumowanie funkcji IntelliTrace** zostanie otwarty.</span><span class="sxs-lookup"><span data-stu-id="0fc20-170">hello **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="0fc20-171">Zlokalizuj hello wyjątki części hello podsumowania.</span><span class="sxs-lookup"><span data-stu-id="0fc20-171">Locate hello exceptions section of hello summary.</span></span> <span data-ttu-id="0fc20-172">Jeśli istnieją wyjątki, zostaną oznaczone etykietą sekcji hello **wyjątku**.</span><span class="sxs-lookup"><span data-stu-id="0fc20-172">If there are exceptions, hello section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="0fc20-173">Rozwiń węzeł hello **wyjątku** i poszukaj **System.IO.FileNotFoundException** błędy podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="0fc20-173">Expand hello **Exception Data** and look for **System.IO.FileNotFoundException** errors similar toohello following:</span></span>

![Dane wyjątku, Brak pliku lub zestawu](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="0fc20-175">Brak biblioteki dll i zestawy adresów</span><span class="sxs-lookup"><span data-stu-id="0fc20-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="0fc20-176">tooaddress Brak biblioteki DLL i zestawu błędów, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0fc20-176">tooaddress missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="0fc20-177">Otwórz rozwiązanie hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0fc20-177">Open hello solution in Visual Studio.</span></span>
2. <span data-ttu-id="0fc20-178">W **Eksploratora rozwiązań**, otwórz hello **odwołania** folderu.</span><span class="sxs-lookup"><span data-stu-id="0fc20-178">In **Solution Explorer**, open hello **References** folder.</span></span>
3. <span data-ttu-id="0fc20-179">Kliknij zestaw hello objęci hello błąd.</span><span class="sxs-lookup"><span data-stu-id="0fc20-179">Click hello assembly identified in hello error.</span></span>
4. <span data-ttu-id="0fc20-180">W hello **właściwości** okienku Znajdź **właściwości kopii lokalnej** i ustaw wartość hello zbyt**True**.</span><span class="sxs-lookup"><span data-stu-id="0fc20-180">In hello **Properties** pane, locate **Copy Local property** and set hello value too**True**.</span></span>
5. <span data-ttu-id="0fc20-181">Należy ponownie wdrożyć usługę w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="0fc20-181">Redeploy hello cloud service.</span></span>

<span data-ttu-id="0fc20-182">Po upewnieniu się, że wszystkie błędy zostaną naprawione, można wdrożyć usługi hello bez sprawdzania hello **włączenia funkcji IntelliTrace dla ról platformy .NET 4** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="0fc20-182">Once you have verified that all errors have been corrected, you can deploy hello service without checking hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fc20-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0fc20-183">Next steps</span></span>
<span data-ttu-id="0fc20-184">Wyświetl więcej [Rozwiązywanie problemów z artykułów](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) dla usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0fc20-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="0fc20-185">toolearn jak roli usługi w chmurze tootroubleshoot problemów przy użyciu danych diagnostycznych komputera Azure PaaS, zobacz [serii blogu Kevina Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fc20-185">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
