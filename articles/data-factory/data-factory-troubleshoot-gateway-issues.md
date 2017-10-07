---
title: "problemy z aaaTroubleshoot brama zarządzania danymi | Dokumentacja firmy Microsoft"
description: "Zawiera porady tootroubleshoot problemów powiązanych tooData brama zarządzania."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="652c0-103">Rozwiązywanie problemów z używaniem bramy zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="652c0-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="652c0-104">Ten artykuł zawiera informacje na temat rozwiązywania problemów przy użyciu bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="652c0-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="652c0-105">Zobacz hello [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać szczegółowe informacje o hello bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-105">See hello [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about hello gateway.</span></span> <span data-ttu-id="652c0-106">Zobacz hello [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu przewodnik przenoszenia danych z tooMicrosoft bazy danych programu SQL Server lokalnego magazynu obiektów Blob platformy Azure przy użyciu bramy hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-106">See hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database tooMicrosoft Azure Blob storage by using hello gateway.</span></span>
>
>

## <a name="failed-tooinstall-or-register-gateway"></a><span data-ttu-id="652c0-107">Nie powiodło się tooinstall lub zarejestruj bramę</span><span class="sxs-lookup"><span data-stu-id="652c0-107">Failed tooinstall or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="652c0-108">1. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-108">1. Problem</span></span>
<span data-ttu-id="652c0-109">Widzisz ten komunikat o błędzie podczas instalowania i rejestrowanie bramy, w szczególności podczas pobierania pliku instalacyjnego hello bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-109">You see this error message when installing and registering a gateway, specifically, while downloading hello gateway installation file.</span></span>

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="652c0-110">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-110">Cause</span></span>
<span data-ttu-id="652c0-111">Hello maszyny, na którym próbujesz tooinstall hello bramy nie powiodło się toodownload hello najnowszej bramy plik instalacyjny z Centrum pobierania hello powodu tooa problem z siecią.</span><span class="sxs-lookup"><span data-stu-id="652c0-111">hello machine on which you are trying tooinstall hello gateway has failed toodownload hello latest gateway installation file from hello download center due tooa network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="652c0-112">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-112">Resolution</span></span>
<span data-ttu-id="652c0-113">Sprawdź toosee ustawienia z zapory serwera proxy serwera czy ustawienia hello blokują hello połączenia sieciowego z hello komputera toohello [Centrum pobierania](https://download.microsoft.com/)i zaktualizuj ustawienia hello odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="652c0-113">Check your firewall proxy server settings toosee whether hello settings block hello network connection from hello computer toohello [download center](https://download.microsoft.com/), and update hello settings accordingly.</span></span>

<span data-ttu-id="652c0-114">Alternatywnie można pobrać plik instalacyjny hello hello najnowszą bramę z hello [Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=39717) na innych komputerach, które mogą uzyskiwać dostęp do Centrum pobierania hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-114">Alternatively, you can download hello installation file for hello latest gateway from hello [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access hello download center.</span></span> <span data-ttu-id="652c0-115">Mogą być następnie brama toohello pliku Instalatora hello kopiowania komputera-hosta i uruchomić go ręcznie bramy hello tooinstall i aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="652c0-115">You can then copy hello installer file toohello gateway host computer and run it manually tooinstall and update hello gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="652c0-116">2. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-116">2. Problem</span></span>
<span data-ttu-id="652c0-117">Ten błąd jest widoczny podczas tooinstall bramy w przypadku próby klikając **Zainstaluj bezpośrednio na tym komputerze** w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="652c0-117">You see this error when you're attempting tooinstall a gateway by clicking **install directly on this computer** in hello Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="652c0-118">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-118">Cause</span></span>
<span data-ttu-id="652c0-119">Brama jest już zainstalowana na komputerze hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-119">A gateway is already installed on hello machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="652c0-120">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-120">Resolution</span></span>
<span data-ttu-id="652c0-121">Odinstaluj istniejącą bramę hello na maszynie hello, a następnie kliknij przycisk hello **Zainstaluj bezpośrednio na tym komputerze** połączyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="652c0-121">Uninstall hello existing gateway on hello machine and click hello **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="652c0-122">3. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-122">3. Problem</span></span>
<span data-ttu-id="652c0-123">Ten błąd może być widoczna podczas rejestrowania nowej bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-123">You might see this error when registering a new gateway.</span></span>

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="652c0-124">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-124">Cause</span></span>
<span data-ttu-id="652c0-125">Można napotkać tego komunikatu dla jednego z hello z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="652c0-125">You might see this message for one of hello following reasons:</span></span>

* <span data-ttu-id="652c0-126">format Hello hello klucz bramy jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="652c0-126">hello format of hello gateway key is invalid.</span></span>
* <span data-ttu-id="652c0-127">klucz bramy Hello została unieważniona.</span><span class="sxs-lookup"><span data-stu-id="652c0-127">hello gateway key has been invalidated.</span></span>
* <span data-ttu-id="652c0-128">wygenerowano ponownie klucz bramy Hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="652c0-128">hello gateway key has been regenerated from hello portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="652c0-129">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-129">Resolution</span></span>
<span data-ttu-id="652c0-130">Sprawdź, czy używasz hello klucz prawo bramy z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-130">Verify whether you are using hello right gateway key from hello portal.</span></span> <span data-ttu-id="652c0-131">W razie potrzeby ponownie wygenerować klucz i użyj hello klucza tooregister hello bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-131">If needed, regenerate a key and use hello key tooregister hello gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="652c0-132">4. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-132">4. Problem</span></span>
<span data-ttu-id="652c0-133">Może pojawić się następujący komunikat o błędzie, jeśli rejestrujesz bramy hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-133">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Zawartość i format klucza jest nieprawidłowy](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="652c0-135">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-135">Cause</span></span>
<span data-ttu-id="652c0-136">Witaj zawartości lub format hello klucz bramy wejściowy jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="652c0-136">hello content or format of hello input gateway key is incorrect.</span></span> <span data-ttu-id="652c0-137">Jednego z powodów hello może być to, że tylko część klucza hello został skopiowany z portalu hello lub jest używany nieprawidłowy klucz.</span><span class="sxs-lookup"><span data-stu-id="652c0-137">One of hello reasons can be that you copied only a portion of hello key from hello portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="652c0-138">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-138">Resolution</span></span>
<span data-ttu-id="652c0-139">Wygeneruj klucz bramy w portalu hello i użyj hello kopiowania przycisk toocopy hello cały klucz.</span><span class="sxs-lookup"><span data-stu-id="652c0-139">Generate a gateway key in hello portal, and use hello copy button toocopy hello whole key.</span></span> <span data-ttu-id="652c0-140">Następnie wklej go w tej bramy hello tooregister okna.</span><span class="sxs-lookup"><span data-stu-id="652c0-140">Then paste it in this window tooregister hello gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="652c0-141">5. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-141">5. Problem</span></span>
<span data-ttu-id="652c0-142">Może pojawić się następujący komunikat o błędzie, jeśli rejestrujesz bramy hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-142">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![Klucz bramy jest nieprawidłowy lub pusty](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="652c0-144">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-144">Cause</span></span>
<span data-ttu-id="652c0-145">wygenerowano ponownie klucz bramy Hello lub hello bramy został usunięty w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="652c0-145">hello gateway key has been regenerated or hello gateway has been deleted in hello Azure portal.</span></span> <span data-ttu-id="652c0-146">Możliwe również, czy hello konfiguracji bramy zarządzania danymi nie jest najnowszą.</span><span class="sxs-lookup"><span data-stu-id="652c0-146">It can also happen if hello Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="652c0-147">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-147">Resolution</span></span>
<span data-ttu-id="652c0-148">Sprawdź hello konfiguracji bramy zarządzania danymi jest najnowsza wersja hello, możesz znaleźć najnowszej wersji hello na powitania Microsoft [Centrum pobierania](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="652c0-148">Check if hello Data Management Gateway setup is hello latest version, you can find hello latest version on hello Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="652c0-149">Jeśli Instalator jest bieżący / najnowsze i brama nadal istnieje w portalu, ponownie wygenerować klucz bramy hello w hello portalu Azure, użyj hello kopiowania przycisk toocopy hello cały klucz i wklej go w tej bramy hello tooregister okna.</span><span class="sxs-lookup"><span data-stu-id="652c0-149">If setup is current/ latest and gateway still exists on Portal, regenerate hello gateway key in hello Azure portal, and use hello copy button toocopy hello whole key, and then paste it in this window tooregister hello gateway.</span></span> <span data-ttu-id="652c0-150">W przeciwnym razie ponownie hello bramy i zacząć od nowa.</span><span class="sxs-lookup"><span data-stu-id="652c0-150">Otherwise, recreate hello gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="652c0-151">6. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-151">6. Problem</span></span>
<span data-ttu-id="652c0-152">Może pojawić się następujący komunikat o błędzie, jeśli rejestrujesz bramy hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-152">You might see hello following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![Klucz bramy jest nieprawidłowy lub pusty](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="652c0-154">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-154">Cause</span></span>
<span data-ttu-id="652c0-155">Ten błąd może się zdarzyć, ponieważ usunięto bramę hello lub ponownie wygenerować klucz bramy skojarzone hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-155">This error might happen because either hello gateway has been deleted or hello associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="652c0-156">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-156">Resolution</span></span>
<span data-ttu-id="652c0-157">Usunięcie bramy hello ponownie utworzyć bramę hello hello portalu, kliknij przycisk **zarejestrować**, skopiuj klucz hello z portalu hello, wklej go, a następnie spróbuj tooregister hello bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-157">If hello gateway has been deleted, re-create hello gateway from hello portal, click **Register**, copy hello key from hello portal, paste it, and try tooregister hello gateway.</span></span>

<span data-ttu-id="652c0-158">Jeśli brama hello nadal istnieje, ale ponownego wygenerowania klucza jego, użyj hello nowego klucza tooregister hello bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-158">If hello gateway still exists but its key has been regenerated, use hello new key tooregister hello gateway.</span></span> <span data-ttu-id="652c0-159">Jeśli nie masz klucza hello, należy ponownie wygenerować klucz hello ponownie z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-159">If you don’t have hello key, regenerate hello key again from hello portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="652c0-160">7. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-160">7. Problem</span></span>
<span data-ttu-id="652c0-161">W przypadku rejestrowania bramy, może być konieczne tooenter ścieżkę i hasło certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="652c0-161">When you're registering a gateway, you might need tooenter path and password for a certificate.</span></span>

![Określ certyfikat](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="652c0-163">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-163">Cause</span></span>
<span data-ttu-id="652c0-164">Brama Hello została zarejestrowana na innych komputerach przed.</span><span class="sxs-lookup"><span data-stu-id="652c0-164">hello gateway has been registered on other machines before.</span></span> <span data-ttu-id="652c0-165">Podczas rejestracji początkowej hello bramy certyfikat szyfrowania został skojarzony z hello bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-165">During hello initial registration of a gateway, an encryption certificate has been associated with hello gateway.</span></span> <span data-ttu-id="652c0-166">certyfikat Hello można własnym generowanych przez bramę hello lub podane przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-166">hello certificate can either be self-generated by hello gateway or provided by hello user.</span></span>  <span data-ttu-id="652c0-167">Ten certyfikat jest poświadczeń używanych tooencrypt hello magazynu danych (połączonej usługi).</span><span class="sxs-lookup"><span data-stu-id="652c0-167">This certificate is used tooencrypt credentials of hello data store (linked service).</span></span>  

![Eksportowanie certyfikatu](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="652c0-169">Gdy Przywracanie hello bramy na inny komputer hosta, Kreator rejestracji hello zapyta, dla tego certyfikatu toodecrypt poświadczeń wcześniej zaszyfrowanych z tym certyfikatem.</span><span class="sxs-lookup"><span data-stu-id="652c0-169">When restoring hello gateway on a different host machine, hello registration wizard asks for this certificate toodecrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="652c0-170">Bez tego certyfikatu nie może odszyfrować poświadczeń hello hello nowej bramy i wykonania działania kolejnych kopii skojarzone z tym nową bramę zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="652c0-170">Without this certificate, hello credentials cannot be decrypted by hello new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="652c0-171">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-171">Resolution</span></span>
<span data-ttu-id="652c0-172">Jeśli certyfikat poświadczeń hello zostały wyeksportowane z oryginalnego komputera bramy hello przy użyciu hello **wyeksportować** przycisk na powitania **ustawienia** karcie w danych Menedżera konfiguracji bramy zarządzania, należy użyć hello certyfikat w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="652c0-172">If you have exported hello credential certificate from hello original gateway machine by using hello **Export** button on hello **Settings** tab in Data Management Gateway Configuration Manager, use hello certificate here.</span></span>

<span data-ttu-id="652c0-173">Nie można pominąć ten etap, podczas przywracania bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="652c0-174">Jeśli brakuje certyfikatu hello toodelete hello bramy z portalu hello i ponownie Tworzenie nowej bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-174">If hello certificate is missing, you need toodelete hello gateway from hello portal and re-create a new gateway.</span></span>  <span data-ttu-id="652c0-175">Ponadto należy zaktualizować wszystkie połączone usługi, które są powiązane toohello bramy przez ponownego wprowadzania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="652c0-175">In addition, update all linked services that are related toohello gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="652c0-176">8. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-176">8. Problem</span></span>
<span data-ttu-id="652c0-177">Może pojawić się następujący komunikat o błędzie hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-177">You might see hello following error message.</span></span>

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="652c0-178">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-178">Cause</span></span>
<span data-ttu-id="652c0-179">Ten błąd wystąpi, gdy brama jest w środowisku, które wymaga tooaccess serwera proxy HTTP zasobów internetowych, lub serwer proxy uwierzytelniania hasła jest zmieniany, ale nie jest odpowiednio aktualizowany w bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-179">This error happens when your gateway is in an environment that requires an HTTP proxy tooaccess Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="652c0-180">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-180">Resolution</span></span>
<span data-ttu-id="652c0-181">Postępuj zgodnie z instrukcjami hello hello [zagadnienia dotyczące serwera Proxy](#proxy-server-considerations) sekcji tego artykułu, a następnie skonfiguruj ustawienia serwera proxy z danych Menedżera konfiguracji bramy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="652c0-181">Follow hello instructions in hello [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="652c0-182">Brama jest w trybie online z ograniczoną funkcjonalnością</span><span class="sxs-lookup"><span data-stu-id="652c0-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="652c0-183">1. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-183">1. Problem</span></span>
<span data-ttu-id="652c0-184">Możesz wyświetlić stan hello hello bramy jako online z ograniczoną funkcjonalnością.</span><span class="sxs-lookup"><span data-stu-id="652c0-184">You see hello status of hello gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="652c0-185">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-185">Cause</span></span>
<span data-ttu-id="652c0-186">Wyświetlany stan hello hello brama jest w trybie online z ograniczoną funkcjonalność dla jednego z hello z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="652c0-186">You see hello status of hello gateway as online with limited functionality for one of hello following reasons:</span></span>

* <span data-ttu-id="652c0-187">Brama nie może połączyć toocloud usługi za pomocą usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="652c0-187">Gateway cannot connect toocloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="652c0-188">Usługi w chmurze nie można połączyć toogateway za pośrednictwem usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="652c0-188">Cloud service cannot connect toogateway through Service Bus.</span></span>

<span data-ttu-id="652c0-189">Gdy brama hello jest dostępna z ograniczoną funkcjonalnością, może być możliwe toouse hello kreatora kopiowania fabryki danych toocreate danych potoki kopiowania tooor danych z lokalnych magazynów danych.</span><span class="sxs-lookup"><span data-stu-id="652c0-189">When hello gateway is online with limited functionality, you might not be able toouse hello Data Factory Copy Wizard toocreate data pipelines for copying data tooor from on-premises data stores.</span></span> <span data-ttu-id="652c0-190">Jako rozwiązanie alternatywne można Edytor fabryki danych w portalu hello, Visual Studio lub Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="652c0-190">As a workaround, you can use Data Factory Editor in hello portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="652c0-191">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-191">Resolution</span></span>
<span data-ttu-id="652c0-192">Rozwiązanie tego problemu (online z ograniczoną funkcjonalnością) jest oparty na czy hello bramy nie można połączyć z usługą w chmurze toohello lub hello inny sposób.</span><span class="sxs-lookup"><span data-stu-id="652c0-192">Resolution for this issue (online with limited functionality) is based on whether hello gateway cannot connect toohello cloud service or hello other way.</span></span> <span data-ttu-id="652c0-193">Witaj następujące sekcje zawierają te rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="652c0-193">hello following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="652c0-194">2. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-194">2. Problem</span></span>
<span data-ttu-id="652c0-195">Zostanie wyświetlony następujący błąd hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-195">You see hello following error.</span></span>

`Error: Gateway cannot connect toocloud service through service bus`

![Brama nie może połączyć toocloud usługi](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="652c0-197">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-197">Cause</span></span>
<span data-ttu-id="652c0-198">Brama nie może połączyć toohello usługi w chmurze za pośrednictwem usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="652c0-198">Gateway cannot connect toohello cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="652c0-199">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-199">Resolution</span></span>
<span data-ttu-id="652c0-200">Wykonaj te kroki tooget hello bramy powrotem w tryb online:</span><span class="sxs-lookup"><span data-stu-id="652c0-200">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="652c0-201">Zezwalaj na adres IP reguły wychodzące na komputerze bramy hello i hello firmowej zapory.</span><span class="sxs-lookup"><span data-stu-id="652c0-201">Allow IP address outbound rules on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="652c0-202">Można znaleźć adres IP z dziennika zdarzeń systemu Windows hello (identyfikator == 401): próba została wprowadzona tooaccess gniazda w sposób zabroniony przez jego uprawnienia dostępu XX. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="652c0-202">You can find IP addresses from hello Windows Event Log (ID == 401): An attempt was made tooaccess a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="652c0-203">Skonfiguruj ustawienia serwera proxy na powitania bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-203">Configure proxy settings on hello gateway.</span></span> <span data-ttu-id="652c0-204">Zobacz hello [zagadnienia dotyczące serwera Proxy](#proxy-server-considerations) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="652c0-204">See hello [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="652c0-205">Włącz portów wychodzących 5671 i 9350-9354 na obu hello zapory systemu Windows na komputerze bramy hello i hello firmowej zapory.</span><span class="sxs-lookup"><span data-stu-id="652c0-205">Enable outbound ports 5671 and 9350-9354 on both hello Windows Firewall on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="652c0-206">Zobacz hello [portów i zapory](#ports-and-firewall) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="652c0-206">See hello [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="652c0-207">Ten krok jest opcjonalny, ale firma Microsoft zaleca ze względów wydajności.</span><span class="sxs-lookup"><span data-stu-id="652c0-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="652c0-208">3. Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-208">3. Problem</span></span>
<span data-ttu-id="652c0-209">Zostanie wyświetlony następujący błąd hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-209">You see hello following error.</span></span>

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="652c0-210">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-210">Cause</span></span>
<span data-ttu-id="652c0-211">Błąd przejściowy w łączności sieciowej.</span><span class="sxs-lookup"><span data-stu-id="652c0-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="652c0-212">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-212">Resolution</span></span>
<span data-ttu-id="652c0-213">Wykonaj te kroki tooget hello bramy powrotem w tryb online:</span><span class="sxs-lookup"><span data-stu-id="652c0-213">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="652c0-214">Zaczekaj kilka minut, łączności hello zostaną automatycznie odzyskane po hello błąd został usunięty.</span><span class="sxs-lookup"><span data-stu-id="652c0-214">Wait for a couple of minutes, hello connectivity will be automatically recovered when hello error is gone.</span></span>
* <span data-ttu-id="652c0-215">Jeśli hello błąd będzie się powtarzać, uruchom ponownie usługę bramy hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-215">If hello error persists, restart hello gateway service.</span></span>

## <a name="failed-tooauthor-linked-service"></a><span data-ttu-id="652c0-216">Nie powiodło się tooauthor połączone usługi</span><span class="sxs-lookup"><span data-stu-id="652c0-216">Failed tooauthor linked service</span></span>
### <a name="problem"></a><span data-ttu-id="652c0-217">Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-217">Problem</span></span>
<span data-ttu-id="652c0-218">Ten błąd może być widoczna podczas spróbuj toouse Menedżera poświadczeń w hello tooinput portalu poświadczeń dla nowej usługi połączonej lub zaktualizować poświadczenia istniejącą połączoną usługę.</span><span class="sxs-lookup"><span data-stu-id="652c0-218">You might see this error when you try toouse Credential Manager in hello portal tooinput credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

<span data-ttu-id="652c0-219">Gdy zostanie wyświetlony ten błąd, strony ustawień hello z danych Menedżera konfiguracji bramy zarządzania może wyglądać powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="652c0-219">When you see this error, hello settings page of Data Management Gateway Configuration Manager might look like hello following screenshot.</span></span>

![Nie można nawiązać połączenia bazy danych](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="652c0-221">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-221">Cause</span></span>
<span data-ttu-id="652c0-222">certyfikat SSL Hello mógł utracić na komputerze bramy hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-222">hello SSL certificate might have been lost on hello gateway machine.</span></span> <span data-ttu-id="652c0-223">komputer z bramą Hello nie można załadować hello certyfikat obecnie używany do szyfrowania SSL.</span><span class="sxs-lookup"><span data-stu-id="652c0-223">hello gateway computer cannot load hello certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="652c0-224">Może być również wyświetlany jest komunikat o błędzie w dzienniku zdarzeń hello, który jest podobne toohello następującą wiadomości.</span><span class="sxs-lookup"><span data-stu-id="652c0-224">You might also see an error message in hello event log that is similar toohello following message.</span></span>

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="652c0-225">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-225">Resolution</span></span>
<span data-ttu-id="652c0-226">Wykonaj te kroki toosolve hello problemu:</span><span class="sxs-lookup"><span data-stu-id="652c0-226">Follow these steps toosolve hello problem:</span></span>

1. <span data-ttu-id="652c0-227">Uruchom Menedżera konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="652c0-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="652c0-228">Przełącz toohello **ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="652c0-228">Switch toohello **Settings** tab.</span></span>  
3. <span data-ttu-id="652c0-229">Kliknij przycisk hello **zmiany** certyfikat SSL hello toochange przycisku.</span><span class="sxs-lookup"><span data-stu-id="652c0-229">Click hello **Change** button toochange hello SSL certificate.</span></span>

   ![Zmień przycisk certyfikat](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="652c0-231">Wybierz nowy certyfikat jako hello certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="652c0-231">Select a new certificate as hello SSL certificate.</span></span> <span data-ttu-id="652c0-232">Możesz użyć dowolnego certyfikatu SSL, który jest generowany przez użytkownika lub każdej organizacji.</span><span class="sxs-lookup"><span data-stu-id="652c0-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Określ certyfikat](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="652c0-234">Aktywność kopiowania nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="652c0-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="652c0-235">Problem</span><span class="sxs-lookup"><span data-stu-id="652c0-235">Problem</span></span>
<span data-ttu-id="652c0-236">Można zauważyć powitania po awarii "UserErrorFailedToConnectToSqlserver", po skonfigurowaniu potoku w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-236">You might notice hello following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in hello portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a><span data-ttu-id="652c0-237">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="652c0-237">Cause</span></span>
<span data-ttu-id="652c0-238">Może to mieć kilka przyczyn, i środki zaradcze różni odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="652c0-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="652c0-239">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="652c0-239">Resolution</span></span>
<span data-ttu-id="652c0-240">Zezwolenie na połączenia wychodzące TCP za pośrednictwem portu TCP/1433 na powitania po stronie klienta bramy zarządzania danymi przed połączeniem tooan bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="652c0-240">Allow outbound TCP connections over port TCP/1433 on hello Data Management Gateway client side before connecting tooan SQL database.</span></span>

<span data-ttu-id="652c0-241">Jeśli hello docelowa baza danych jest bazą danych Azure SQL, sprawdzanie programu SQL Server ustawień zapory dla platformy Azure oraz.</span><span class="sxs-lookup"><span data-stu-id="652c0-241">If hello target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="652c0-242">Zobacz powitania po sekcji tootest hello połączenia toohello na lokalnym magazynem danych.</span><span class="sxs-lookup"><span data-stu-id="652c0-242">See hello following section tootest hello connection toohello on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="652c0-243">Połączenia magazynu danych lub błędy związane z sterownika</span><span class="sxs-lookup"><span data-stu-id="652c0-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="652c0-244">Jeśli widzisz dane przechowywane połączenia lub błędy związane z sterowników, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="652c0-244">If you see data store connection or driver-related errors, complete hello following steps:</span></span>

1. <span data-ttu-id="652c0-245">Uruchom Menedżera konfiguracji bramy zarządzania danymi na maszynie bramy hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-245">Start Data Management Gateway Configuration Manager on hello gateway machine.</span></span>
2. <span data-ttu-id="652c0-246">Przełącz toohello **diagnostyki** kartę.</span><span class="sxs-lookup"><span data-stu-id="652c0-246">Switch toohello **Diagnostics** tab.</span></span>
3. <span data-ttu-id="652c0-247">W **Testuj połączenie**, Dodaj grupę hello bramę.</span><span class="sxs-lookup"><span data-stu-id="652c0-247">In **Test Connection**, add hello gateway group values.</span></span>
4. <span data-ttu-id="652c0-248">Kliknij przycisk **testu** toosee, jeśli można połączyć toohello lokalnego źródła danych na maszynie bramy hello przy użyciu hello informacje o połączeniu oraz poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="652c0-248">Click **Test** toosee if you can connect toohello on-premises data source from hello gateway machine by using hello connection information and credentials.</span></span> <span data-ttu-id="652c0-249">Jeśli połączenie testowe hello nadal kończy się niepowodzeniem po zainstalowaniu sterownika, ponowne uruchomienie hello bramy dla niego toopick się hello najnowsze zmiany.</span><span class="sxs-lookup"><span data-stu-id="652c0-249">If hello test connection still fails after you install a driver, restart hello gateway for it toopick up hello latest change.</span></span>

![Testuj połączenie na karcie diagnostyki](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="652c0-251">Dzienniki bramy</span><span class="sxs-lookup"><span data-stu-id="652c0-251">Gateway logs</span></span>
### <a name="send-gateway-logs-toomicrosoft"></a><span data-ttu-id="652c0-252">Wyślij tooMicrosoft dzienniki bramy</span><span class="sxs-lookup"><span data-stu-id="652c0-252">Send gateway logs tooMicrosoft</span></span>
<span data-ttu-id="652c0-253">Gdy skontaktować się z Microsoft Support tooget pomoc dotyczącą rozwiązywania problemów bramy, użytkownik może zostać poproszony tooshare dzienniki bramy.</span><span class="sxs-lookup"><span data-stu-id="652c0-253">When you contact Microsoft Support tooget help with troubleshooting gateway issues, you might be asked tooshare your gateway logs.</span></span> <span data-ttu-id="652c0-254">Hello wersji z hello bramy można udostępniać dzienniki wymagane bramy z dwóch kliknięcia przycisków w danych Menedżera konfiguracji bramy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="652c0-254">With hello release of hello gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="652c0-255">Przełącz toohello **diagnostyki** kartę w danych Menedżera konfiguracji bramy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="652c0-255">Switch toohello **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Karta zarządzania diagnostyki bramy danych](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="652c0-257">Kliknij przycisk **Wyślij dzienniki** hello toosee następujące okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="652c0-257">Click **Send Logs** toosee hello following dialog box.</span></span>

    ![Dzienniki zarządzania bramy wysyłanie danych](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="652c0-259">(Opcjonalnie) Kliknij przycisk **Sprawdź dzienniki** tooreview dzienniki w Podglądzie zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-259">(Optional) Click **view logs** tooreview logs in hello event viewer.</span></span>
4. <span data-ttu-id="652c0-260">(Opcjonalnie) Kliknij przycisk **prywatności** zasady zachowania poufności informacji usług tooreview firmy Microsoft w sieci web.</span><span class="sxs-lookup"><span data-stu-id="652c0-260">(Optional) Click **privacy** tooreview Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="652c0-261">Po zakończeniu są o tooupload, kliknij przycisk **Wyślij dzienniki** tooactually przesyłania dzienników hello z hello ostatnich siedmiu dni tooMicrosoft do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="652c0-261">When you are satisfied with what you are about tooupload, click **Send Logs** tooactually send hello logs from hello last seven days tooMicrosoft for troubleshooting.</span></span> <span data-ttu-id="652c0-262">Powinien zostać wyświetlony stan hello operacji wysyłania dzienników hello pokazane na powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="652c0-262">You should see hello status of hello send-logs operation as shown in hello following screenshot.</span></span>

    ![Dane zarządzania bramy wysyłania dzienników stanu](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="652c0-264">Po zakończeniu operacji hello wyświetlone okno dialogowe pokazane na powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="652c0-264">After hello operation is complete, you see a dialog box as shown in hello following screenshot.</span></span>

    ![Dane zarządzania bramy wysyłania dzienników stanu](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="652c0-266">Zapisz hello **identyfikator raportu** i udostępniać je Support firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="652c0-266">Save hello **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="652c0-267">Identyfikator raportu Hello jest używany toolocate hello bramy dzienniki przekazane do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="652c0-267">hello report ID is used toolocate hello gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="652c0-268">Identyfikator raportu Hello jest także zapisane w Podglądzie zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-268">hello report ID is also saved in hello event viewer.</span></span>  <span data-ttu-id="652c0-269">Można go znaleźć, sprawdzając identyfikator zdarzenia hello "25" i sprawdź hello daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="652c0-269">You can find it by looking at hello event ID “25”, and check hello date and time.</span></span>

    ![Dane zarządzania bramy wysyłania dzienników identyfikator raportu](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="652c0-271">Dzienniki bramy archiwum na komputerze hosta bramy</span><span class="sxs-lookup"><span data-stu-id="652c0-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="652c0-272">Istnieją sytuacje, w którym masz problemy bramy i dzienniki bramy nie mogą współużytkować bezpośrednio:</span><span class="sxs-lookup"><span data-stu-id="652c0-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="652c0-273">Ręcznie zainstaluj hello bramy i zarejestruj bramę hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-273">You manually install hello gateway and register hello gateway.</span></span>
* <span data-ttu-id="652c0-274">Możesz spróbować tooregister hello bramy za pomocą ponownie wygenerowanego klucza w danych Menedżera konfiguracji bramy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="652c0-274">You try tooregister hello gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="652c0-275">Spróbuj dzienniki toosend i nie może zostać połączona usługa hosta bramy hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-275">You try toosend logs and hello gateway host service cannot be connected.</span></span>

<span data-ttu-id="652c0-276">W tych sytuacjach można zapisać dzienniki bramy jako plik zip i udostępnić go w przypadku skontaktuj się z pomocą techniczną firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="652c0-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="652c0-277">Na przykład jeśli wystąpi błąd podczas rejestrowania bramy hello jako pokazano hello następującego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="652c0-277">For example, if you receive an error while you register hello gateway as shown in hello following screenshot.</span></span>   

![Błąd zarządzania rejestracji bramy danych](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="652c0-279">Kliknij przycisk hello **archiwum dzienniki bramy** połączyć tooarchive i zapisać dzienników, a następnie udostępnić plik zip hello pomocy technicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="652c0-279">Click hello **Archive gateway logs** link tooarchive and save logs, and then share hello zip file with Microsoft support.</span></span>

![Dzienniki zarządzania bramy archiwum danych](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="652c0-281">Zlokalizuj dzienniki bramy</span><span class="sxs-lookup"><span data-stu-id="652c0-281">Locate gateway logs</span></span>
<span data-ttu-id="652c0-282">Bramy szczegółowe informacje można znaleźć w dzienniku zdarzeń systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-282">You can find detailed gateway log information in hello Windows event logs.</span></span>

1. <span data-ttu-id="652c0-283">Uruchom system Windows **Podgląd zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="652c0-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="652c0-284">Zlokalizuj dzienniki w hello **Dzienniki aplikacji i usług** > **brama zarządzania danymi** folderu.</span><span class="sxs-lookup"><span data-stu-id="652c0-284">Locate logs in hello **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="652c0-285">Przy rozwiązywaniu problemów związanych z bramą, wyszukaj poziom zdarzenia błędów w Podglądzie zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="652c0-285">When you're troubleshooting gateway-related issues, look for error level events in hello event viewer.</span></span>

![Brama zarządzania danymi dzienniki w Podglądzie zdarzeń](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
