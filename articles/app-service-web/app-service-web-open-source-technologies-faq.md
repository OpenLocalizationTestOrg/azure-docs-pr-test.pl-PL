---
title: "aplikacje sieci web technologii źródła aaaOpen często zadawane pytania dotyczące usługi Azure | Dokumentacja firmy Microsoft"
description: Uzyskaj odpowiedzi toofrequently zadawane pytania na temat technologii open source w funkcji Web Apps hello Azure App Service.
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="83e38-103">Technologie open source często zadawane pytania dotyczące aplikacji sieci Web na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="83e38-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="83e38-104">Ten artykuł zawiera toofrequently odpowiedzi zadawane pytania (FAQ) dotyczące problemów z technologii open source hello [funkcja Web Apps usługi Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="83e38-104">This article has answers toofrequently asked questions (FAQs) about issues with open-source technologies for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="83e38-105">Baza danych ClearDB jest wyłączony.</span><span class="sxs-lookup"><span data-stu-id="83e38-105">My ClearDB database is down.</span></span> <span data-ttu-id="83e38-106">Jak rozwiązać ten problem?</span><span class="sxs-lookup"><span data-stu-id="83e38-106">How do I resolve this?</span></span>

<span data-ttu-id="83e38-107">W przypadku problemów związanych z bazy danych, skontaktuj się z [Obsługa ClearDB](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="83e38-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="83e38-108">Aby uzyskać odpowiedzi na pytania toocommon o ClearDB, zobacz [ClearDB — często zadawane pytania](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="83e38-108">For answers toocommon questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a><span data-ttu-id="83e38-109">Dlaczego mojej bazy danych ClearDB nie jest wymieniony w portalu hello?</span><span class="sxs-lookup"><span data-stu-id="83e38-109">Why isn't my ClearDB database listed in hello portal?</span></span>

<span data-ttu-id="83e38-110">Jeśli utworzysz bazę danych ClearDB w hello [portalu Azure](http://portal.azure.com/), hello bazy danych nie jest wyświetlane w hello [klasycznego portalu Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="83e38-110">If you create a ClearDB database in hello [Azure portal](http://portal.azure.com/), hello database doesn't appear in hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="83e38-111">toowork obejścia tego problemu, może ręcznie połączyć aplikację sieci web toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="83e38-111">toowork around this, you can manually link your database toohello web app.</span></span>

<span data-ttu-id="83e38-112">Podobnie jeśli utworzysz bazę danych ClearDB w hello [klasycznego portalu Azure](http://manage.windowsazure.com/), nie zobaczysz bazy danych w hello [portalu Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="83e38-112">Similarly, if you create a ClearDB database in hello [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in hello [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="83e38-113">W takim przypadku obejście nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="83e38-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="83e38-114">Aby uzyskać więcej informacji, zobacz [często zadawane pytania dotyczące bazy danych ClearDB MySQL z usługi aplikacji Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="83e38-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="83e38-115">Dlaczego nie migracji bazy danych ClearDB podczas migracji mojej subskrypcji?</span><span class="sxs-lookup"><span data-stu-id="83e38-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="83e38-116">Podczas przeprowadzania migracji zasobów w subskrypcjach, mają zastosowanie następujące ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="83e38-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="83e38-117">Baza danych ClearDB MySQL jest usługi innej firmy i nie są migrowane podczas migracji subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="83e38-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="83e38-118">Jeśli nie zarządzasz hello migracji bazy danych MySQL, przed przeprowadzeniem migracji zasobów platformy Azure, bazy danych ClearDB MySQL mogą być niedostępne.</span><span class="sxs-lookup"><span data-stu-id="83e38-118">If you don't manage hello migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="83e38-119">tooavoid to najpierw ręcznie należy zmigrować bazę danych ClearDB, a następnie przeprowadzić migrację hello subskrypcji platformy Azure dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="83e38-119">tooavoid this, first, manually migrate your ClearDB database, and then migrate hello Azure subscription for your web app.</span></span>

<span data-ttu-id="83e38-120">Aby uzyskać więcej informacji, zobacz [często zadawane pytania dotyczące bazy danych ClearDB MySQL z usługi aplikacji Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="83e38-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a><span data-ttu-id="83e38-121">Jak włączyć rejestrowanie problemów PHP tootroubleshoot PHP</span><span class="sxs-lookup"><span data-stu-id="83e38-121">How do I turn on PHP logging tootroubleshoot PHP issues?</span></span>

<span data-ttu-id="83e38-122">tooturn PHP rejestrowania:</span><span class="sxs-lookup"><span data-stu-id="83e38-122">tooturn on PHP logging:</span></span>

1. <span data-ttu-id="83e38-123">Zaloguj się tooyour [Kudu witryny sieci Web](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="83e38-123">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="83e38-124">W menu u góry hello, wybierz **konsoli debugowania** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="83e38-124">In hello top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="83e38-125">Wybierz hello **lokacji** folderu.</span><span class="sxs-lookup"><span data-stu-id="83e38-125">Select hello **Site** folder.</span></span>
4. <span data-ttu-id="83e38-126">Wybierz hello **wwwroot** folderu.</span><span class="sxs-lookup"><span data-stu-id="83e38-126">Select hello **wwwroot** folder.</span></span>
5. <span data-ttu-id="83e38-127">Wybierz hello  **+**  ikonę, a następnie wybierz **nowy plik**.</span><span class="sxs-lookup"><span data-stu-id="83e38-127">Select hello **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="83e38-128">Ustaw nazwę pliku hello zbyt**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="83e38-128">Set hello file name too**.user.ini**.</span></span>
7. <span data-ttu-id="83e38-129">Wybierz ikonę ołówka hello obok zbyt**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="83e38-129">Select hello pencil icon next too**.user.ini**.</span></span>
8. <span data-ttu-id="83e38-130">W pliku hello Dodaj ten kod:`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="83e38-130">In hello file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="83e38-131">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="83e38-131">Select **Save**.</span></span>
10. <span data-ttu-id="83e38-132">Wybierz ikonę ołówka hello obok zbyt**wp config.php**.</span><span class="sxs-lookup"><span data-stu-id="83e38-132">Select hello pencil icon next too**wp-config.php**.</span></span>
11. <span data-ttu-id="83e38-133">Zmień toohello tekst hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="83e38-133">Change hello text toohello following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="83e38-134">Witaj portalu Azure, w menu aplikacji sieci web hello, ponownie uruchomić aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="83e38-134">In hello Azure portal, in hello web app menu, restart your web app.</span></span>

<span data-ttu-id="83e38-135">Aby uzyskać więcej informacji, zobacz [dzienniki błędów włączyć WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="83e38-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="83e38-136">Jak rejestrować błędów aplikacji Python w aplikacjach, które znajdują się w usłudze App Service?</span><span class="sxs-lookup"><span data-stu-id="83e38-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="83e38-137">błędów aplikacji Python toocapture:</span><span class="sxs-lookup"><span data-stu-id="83e38-137">toocapture Python application errors:</span></span>

1. <span data-ttu-id="83e38-138">Witaj portalu Azure w aplikacji sieci web wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="83e38-138">In hello Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="83e38-139">Na powitania **ustawienia** wybierz opcję **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="83e38-139">On hello **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="83e38-140">W obszarze **ustawień aplikacji**, wprowadź powitania po parę klucza i wartości:</span><span class="sxs-lookup"><span data-stu-id="83e38-140">Under **App settings**, enter hello following key/value pair:</span></span>
    * <span data-ttu-id="83e38-141">Klucz: WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="83e38-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="83e38-142">Wartość: D:\home\site\wwwroot\logs.txt (wprowadź wybrana nazwa pliku)</span><span class="sxs-lookup"><span data-stu-id="83e38-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="83e38-143">Błędy w pliku logs.txt hello w folderze wwwroot hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="83e38-143">You should now see errors in hello logs.txt file in hello wwwroot folder.</span></span>

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="83e38-144">Jak zmienić wersję hello hello aplikacji Node.js, który znajduje się w usłudze App Service?</span><span class="sxs-lookup"><span data-stu-id="83e38-144">How do I change hello version of hello Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="83e38-145">Wersja hello toochange hello aplikacji Node.js, można użyć jednego z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="83e38-145">toochange hello version of hello Node.js application, you can use one of hello following options:</span></span>

*   <span data-ttu-id="83e38-146">W portalu Azure hello, użyj **ustawień aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="83e38-146">In hello Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="83e38-147">W hello portalu Azure Przejdź tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="83e38-147">In hello Azure portal, go tooyour web app.</span></span>
    2. <span data-ttu-id="83e38-148">Na powitania **ustawienia** bloku, wybierz opcję **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="83e38-148">On hello **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="83e38-149">W **ustawień aplikacji**, mogą obejmować WEBSITE_NODE_DEFAULT_VERSION jako klucz hello i hello wersji środowiska node.js ma jako wartość hello.</span><span class="sxs-lookup"><span data-stu-id="83e38-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as hello key, and hello version of Node.js you want as hello value.</span></span>
    4. <span data-ttu-id="83e38-150">Przejdź tooyour [konsoli Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="83e38-150">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="83e38-151">toocheck hello wersji środowiska Node.js, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="83e38-151">toocheck hello Node.js version, enter hello following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="83e38-152">Zmodyfikuj plik iisnode.yml udostępniany hello.</span><span class="sxs-lookup"><span data-stu-id="83e38-152">Modify hello iisnode.yml file.</span></span> <span data-ttu-id="83e38-153">Zmiana wersji środowiska Node.js hello w plik iisnode.yml udostępniany hello jedynie ustawia środowisko uruchomieniowe hello tego programu iisnode używa.</span><span class="sxs-lookup"><span data-stu-id="83e38-153">Changing hello Node.js version in hello iisnode.yml file only sets hello runtime environment that iisnode uses.</span></span> <span data-ttu-id="83e38-154">Twoje cmd Kudu i inne nadal używać hello wersji środowiska Node.js, który jest ustawiony w **ustawień aplikacji** w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="83e38-154">Your Kudu cmd and others still use hello Node.js version that is set in **App settings** in hello Azure portal.</span></span>

    <span data-ttu-id="83e38-155">Plik iisnode.yml hello tooset ręcznie utworzyć plik iisnode.yml udostępniany w folderze głównym aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83e38-155">tooset hello iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="83e38-156">W pliku hello obejmują powitania po wierszu:</span><span class="sxs-lookup"><span data-stu-id="83e38-156">In hello file, include hello following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="83e38-157">Ustaw hello plik iisnode.yml udostępniany przy użyciu pliku package.json podczas wdrażania kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="83e38-157">Set hello iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="83e38-158">Witaj procesu wdrażania kontroli źródła Azure obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="83e38-158">hello Azure source control deployment process involves hello following steps:</span></span>
    1. <span data-ttu-id="83e38-159">Przenosi toohello zawartości aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="83e38-159">Moves content toohello Azure web app.</span></span>
    2. <span data-ttu-id="83e38-160">Tworzy domyślny skrypt wdrożenia, jeśli nie ma takiego (pliku deploy.cmd, .deployment pliki) w folderze głównym aplikacji hello w sieci web.</span><span class="sxs-lookup"><span data-stu-id="83e38-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in hello web app root folder.</span></span>
    3. <span data-ttu-id="83e38-161">Uruchamia skrypt wdrożenia, w którym tworzy plik iisnode.yml udostępniany Jeśli wspomina hello wersji środowiska Node.js w pliku package.json hello > aparatu`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="83e38-161">Runs a deployment script in which it creates an iisnode.yml file if you mention hello Node.js version in hello package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="83e38-162">Plik iisnode.yml udostępniany Hello ma powitania po wierszu kodu:</span><span class="sxs-lookup"><span data-stu-id="83e38-162">hello iisnode.yml file has hello following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="83e38-163">Wiadomości powitania "Błąd podczas nawiązywania połączenia z bazą danych" widoczne w mojej aplikacji WordPress, który znajduje się w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="83e38-163">I see hello message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="83e38-164">Jak rozwiązać ten problem?</span><span class="sxs-lookup"><span data-stu-id="83e38-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="83e38-165">Jeśli widzisz ten błąd w aplikacji Azure WordPress, tooenable php_errors.log i debug.log pełną hello kroki szczegółowo w [dzienniki błędów włączyć WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="83e38-165">If you see this error in your Azure WordPress app, tooenable php_errors.log and debug.log, complete hello steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="83e38-166">Po włączeniu hello dzienniki, występuje błąd hello, a następnie sprawdź toosee dzienniki hello, w przypadku korzystania z połączeń:</span><span class="sxs-lookup"><span data-stu-id="83e38-166">When hello logs are enabled, reproduce hello error, and then check hello logs toosee if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="83e38-167">Jeśli zostanie wyświetlony ten błąd w plikach debug.log lub php_errors.log aplikacji przekracza hello liczbę połączeń.</span><span class="sxs-lookup"><span data-stu-id="83e38-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding hello number of connections.</span></span> <span data-ttu-id="83e38-168">Jeśli przechowujesz na ClearDB Sprawdź hello liczbę połączeń, które są dostępne w Twojej [plan usługi](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="83e38-168">If you’re hosting on ClearDB, verify hello number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="83e38-169">Jak debugować aplikację Node.js, która jest hostowana w usłudze App Service?</span><span class="sxs-lookup"><span data-stu-id="83e38-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="83e38-170">Przejdź tooyour [konsoli Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="83e38-170">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="83e38-171">Folder Dzienniki aplikacji przejdź tooyour (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="83e38-171">Go tooyour application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="83e38-172">W pliku logging_errors.txt hello Sprawdź, czy zawartość.</span><span class="sxs-lookup"><span data-stu-id="83e38-172">In hello logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="83e38-173">Jak zainstalować natywnych modułów środowiska Python w aplikacji sieci web usługi aplikacji lub aplikacji interfejsu API?</span><span class="sxs-lookup"><span data-stu-id="83e38-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="83e38-174">Niektóre pakiety mogą nie zainstalować przy użyciu narzędzia pip na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="83e38-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="83e38-175">Pakiet HELLO mogą nie być dostępne na powitania indeksu pakietów języka Python lub kompilatora mogą być wymagane (kompilator nie jest dostępna na komputerze hello, na którym działa aplikacja sieci web hello w usłudze App Service).</span><span class="sxs-lookup"><span data-stu-id="83e38-175">hello package might not be available on hello Python Package Index, or a compiler might be required (a compiler is not available on hello computer that is running hello web app in App Service).</span></span> <span data-ttu-id="83e38-176">Informacje dotyczące instalowania modułów macierzystych z usługi aplikacji — aplikacje sieci web i aplikacji API apps, zobacz [zainstalować modułów środowiska Python w usłudze App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="83e38-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a><span data-ttu-id="83e38-177">Jak wdrożyć tooApp aplikacji Django usługi przy użyciu usługi Git i hello nowej wersji języka Python?</span><span class="sxs-lookup"><span data-stu-id="83e38-177">How do I deploy a Django app tooApp Service by using Git and hello new version of Python?</span></span>

<span data-ttu-id="83e38-178">Aby uzyskać informacje o instalowaniu Django, zobacz [wdrażanie tooApp aplikacji Django usługi](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="83e38-178">For information about installing Django, see [Deploying a Django app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-hello-tomcat-log-files-located"></a><span data-ttu-id="83e38-179">Gdzie znajdują się pliki dziennika Tomcat hello znajdujące się?</span><span class="sxs-lookup"><span data-stu-id="83e38-179">Where are hello Tomcat log files located?</span></span>

<span data-ttu-id="83e38-180">Dla portalu Azure Marketplace i wdrożeń niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="83e38-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="83e38-181">Lokalizacja folderu: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="83e38-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="83e38-182">Pliki odsetek:</span><span class="sxs-lookup"><span data-stu-id="83e38-182">Files of interest:</span></span>
    * <span data-ttu-id="83e38-183">catalina. *rrrr mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="83e38-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="83e38-184">Menedżer hosta. *rrrr mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="83e38-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="83e38-185">localhost. *rrrr mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="83e38-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="83e38-186">Menedżer. *rrrr mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="83e38-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="83e38-187">site_access_log. *rrrr mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="83e38-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="83e38-188">Dla portalu **ustawień aplikacji** wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="83e38-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="83e38-189">Lokalizacja folderu: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="83e38-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="83e38-190">Pliki odsetek:</span><span class="sxs-lookup"><span data-stu-id="83e38-190">Files of interest:</span></span>
    * <span data-ttu-id="83e38-191">catalina. *rrrr mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="83e38-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="83e38-192">Menedżer hosta. *rrrr mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="83e38-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="83e38-193">localhost. *rrrr mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="83e38-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="83e38-194">Menedżer. *rrrr mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="83e38-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="83e38-195">site_access_log. *rrrr mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="83e38-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="83e38-196">Jak rozwiązywać problemy z błędami połączeń sterownik JDBC</span><span class="sxs-lookup"><span data-stu-id="83e38-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="83e38-197">Można napotkać następujące wiadomości w dziennikach Tomcat hello:</span><span class="sxs-lookup"><span data-stu-id="83e38-197">You might see hello following message in your Tomcat logs:</span></span>

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="83e38-198">Błąd hello tooresolve:</span><span class="sxs-lookup"><span data-stu-id="83e38-198">tooresolve hello error:</span></span>

1. <span data-ttu-id="83e38-199">Usuń plik sqljdbc*.jar hello z folderu aplikacji/lib.</span><span class="sxs-lookup"><span data-stu-id="83e38-199">Remove hello sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="83e38-200">Jeśli używasz hello niestandardowych Tomcat lub Azure Marketplace Tomcat serwer sieci web, należy skopiować ten folder lib JAR pliku toohello Tomcat.</span><span class="sxs-lookup"><span data-stu-id="83e38-200">If you are using hello custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file toohello Tomcat lib folder.</span></span>
3. <span data-ttu-id="83e38-201">Jeśli włączasz Java z portalu Azure hello (wybierz **Java 1.8** > **serwera Tomcat**), plik jar sqljdbc.* hello kopiowania w folderze hello jest równoległe tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83e38-201">If you are enabling Java from hello Azure portal (select **Java 1.8** > **Tomcat server**), copy hello sqljdbc.* jar file in hello folder that's parallel tooyour app.</span></span> <span data-ttu-id="83e38-202">Następnie należy dodać hello następującego pliku web.config toohello ustawienie ścieżki klasy:</span><span class="sxs-lookup"><span data-stu-id="83e38-202">Then, add hello following classpath setting toohello web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a><span data-ttu-id="83e38-203">Dlaczego Zobacz błędy, gdy próbuję pliki dziennika na żywo toocopy?</span><span class="sxs-lookup"><span data-stu-id="83e38-203">Why do I see errors when I attempt toocopy live log files?</span></span>

<span data-ttu-id="83e38-204">Jeśli pliki dziennika na żywo toocopy dla aplikacji Java (na przykład Tomcat), można napotkać tego błędu FTP:</span><span class="sxs-lookup"><span data-stu-id="83e38-204">If you try toocopy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

<span data-ttu-id="83e38-205">komunikat o błędzie Hello mogą się różnić w zależności od klienta hello FTP.</span><span class="sxs-lookup"><span data-stu-id="83e38-205">hello error message might vary, depending on hello FTP client.</span></span>

<span data-ttu-id="83e38-206">Wszystkie aplikacje Java mają to blokującego problem.</span><span class="sxs-lookup"><span data-stu-id="83e38-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="83e38-207">Tylko Kudu obsługuje pobieranie tego pliku w uruchomionej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="83e38-207">Only Kudu supports downloading this file while hello app is running.</span></span>

<span data-ttu-id="83e38-208">Zatrzymywanie aplikacji hello zezwala na dostęp FTP toothese plików.</span><span class="sxs-lookup"><span data-stu-id="83e38-208">Stopping hello app allows FTP access toothese files.</span></span>

<span data-ttu-id="83e38-209">Inne obejście jest toowrite zadania WebJob, który jest uruchamiany zgodnie z harmonogramem i kopii tych plików tooa innego katalogu.</span><span class="sxs-lookup"><span data-stu-id="83e38-209">Another workaround is toowrite a WebJob that runs on a schedule and copies these files tooa different directory.</span></span> <span data-ttu-id="83e38-210">Aby uzyskać przykładowy projekt, zobacz hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) projektu.</span><span class="sxs-lookup"><span data-stu-id="83e38-210">For a sample project, see hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-hello-log-files-for-jetty"></a><span data-ttu-id="83e38-211">Gdzie znaleźć hello plików dziennika dla Jetty?</span><span class="sxs-lookup"><span data-stu-id="83e38-211">Where do I find hello log files for Jetty?</span></span>

<span data-ttu-id="83e38-212">Marketplace i wdrożeń niestandardowych hello plik dziennika znajduje się w folderze D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs hello.</span><span class="sxs-lookup"><span data-stu-id="83e38-212">For Marketplace and custom deployments, hello log file is in hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="83e38-213">Należy pamiętać, że lokalizacja folderu hello zależy od wersji hello Jetty używasz.</span><span class="sxs-lookup"><span data-stu-id="83e38-213">Note that hello folder location depends on hello version of Jetty you are using.</span></span> <span data-ttu-id="83e38-214">Na przykład ścieżka hello podane tu dla Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="83e38-214">For example, hello path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="83e38-215">Wyszukaj jetty_*YYYY_MM_DD*. stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="83e38-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="83e38-216">W przypadku wdrożeń aplikacji ustawienia portalu plik dziennika hello jest D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="83e38-216">For portal App Setting deployments, hello log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="83e38-217">Wyszukaj jetty_*YYYY_MM_DD*. stderrout.log</span><span class="sxs-lookup"><span data-stu-id="83e38-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="83e38-218">Z mojej aplikacji sieci web platformy Azure można wysłać wiadomości e-mail?</span><span class="sxs-lookup"><span data-stu-id="83e38-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="83e38-219">Usługa aplikacji nie ma funkcji wbudowanych poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="83e38-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="83e38-220">Dla niektórych dobrej alternatyw do wysyłania wiadomości e-mail z aplikacji, zobacz ten [przepełnienie stosu dyskusji](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="83e38-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a><span data-ttu-id="83e38-221">Dlaczego Moja witryna WordPress Przekierowywanie adresu URL tooanother?</span><span class="sxs-lookup"><span data-stu-id="83e38-221">Why does my WordPress site redirect tooanother URL?</span></span>

<span data-ttu-id="83e38-222">Jeśli niedawno migracji tooAzure WordPress może przekierować toohello starego adresu URL domeny.</span><span class="sxs-lookup"><span data-stu-id="83e38-222">If you have recently migrated tooAzure, WordPress might redirect toohello old domain URL.</span></span> <span data-ttu-id="83e38-223">Jest to spowodowane przez ustawienie w bazie danych MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="83e38-223">This is caused by a setting in hello MySQL database.</span></span>

<span data-ttu-id="83e38-224">WordPress Buddy + jest rozszerzeniem lokacji Azure, której można adresem URL przekierowania hello tooupdate bezpośrednio w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="83e38-224">WordPress Buddy+ is an Azure Site Extension that you can use tooupdate hello redirection URL directly in hello database.</span></span> <span data-ttu-id="83e38-225">Aby uzyskać więcej informacji o używaniu WordPress Buddy +, zobacz [WordPress narzędzia i MySQL migracji Buddy + z WordPress](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="83e38-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="83e38-226">Alternatywnie, jeśli wolisz toomanually adresu URL przekierowania hello usługi aktualizacji za pomocą zapytania SQL lub PHPMyAdmin, zobacz [WordPress: przekierowywanie adresu URL toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="83e38-226">Alternatively, if you prefer toomanually update hello redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting toowrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="83e38-227">Jak zmienić hasło logowania WordPress?</span><span class="sxs-lookup"><span data-stu-id="83e38-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="83e38-228">Jeśli pamiętasz hasła logowania WordPress, możesz użyć WordPress Buddy + tooupdate go.</span><span class="sxs-lookup"><span data-stu-id="83e38-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ tooupdate it.</span></span> <span data-ttu-id="83e38-229">hasło, hello install WordPress Buddy + Azure lokacji rozszerzenia, a następnie pełne hello kroki opisane w tooreset [WordPress narzędzia i MySQL migracji Buddy + z WordPress](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="83e38-229">tooreset your password, install hello WordPress Buddy+ Azure Site Extension, and then complete hello steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a><span data-ttu-id="83e38-230">Nie można zalogować tooWordPress.</span><span class="sxs-lookup"><span data-stu-id="83e38-230">I can't sign in tooWordPress.</span></span> <span data-ttu-id="83e38-231">Jak rozwiązać ten problem?</span><span class="sxs-lookup"><span data-stu-id="83e38-231">How do I resolve this?</span></span>

<span data-ttu-id="83e38-232">Jeśli okaże się zablokowane WordPress po zainstalowaniu ostatnio wtyczkę, może być uszkodzony wtyczki.</span><span class="sxs-lookup"><span data-stu-id="83e38-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="83e38-233">WordPress Buddy + jest rozszerzeniem lokacji Azure, które mogą pomóc Wyłącz wtyczki w WordPress.</span><span class="sxs-lookup"><span data-stu-id="83e38-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="83e38-234">Aby uzyskać więcej informacji, zobacz [WordPress narzędzia i MySQL migracji Buddy + z WordPress](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="83e38-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="83e38-235">Jak przeprowadzić migrację bazy danych WordPress?</span><span class="sxs-lookup"><span data-stu-id="83e38-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="83e38-236">Istnieje wiele opcji migrowania danych MySQL hello jest połączonych tooyour WordPress witryny sieci Web:</span><span class="sxs-lookup"><span data-stu-id="83e38-236">You have multiple options for migrating hello MySQL database that's connected tooyour WordPress website:</span></span>

* <span data-ttu-id="83e38-237">Deweloperzy: Użyj hello [wiersza polecenia lub PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="83e38-237">Developers: Use hello [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="83e38-238">Innych niż deweloperów: Użyj [WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="83e38-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="83e38-239">Sposób pomóc zabezpieczyć WordPress</span><span class="sxs-lookup"><span data-stu-id="83e38-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="83e38-240">toolearn o najlepsze rozwiązania dotyczące WordPress, zobacz [najlepszych rozwiązaniach dotyczących zabezpieczeń WordPress na platformie Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="83e38-240">toolearn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="83e38-241">Próbuję toouse PHPMyAdmin i pojawia się komunikat hello "Odmowa dostępu".</span><span class="sxs-lookup"><span data-stu-id="83e38-241">I am trying toouse PHPMyAdmin, and I see hello message “Access denied.”</span></span> <span data-ttu-id="83e38-242">Jak rozwiązać ten problem?</span><span class="sxs-lookup"><span data-stu-id="83e38-242">How do I resolve this?</span></span>

<span data-ttu-id="83e38-243">Ten problem może wystąpić, jeśli funkcja w aplikacji MySQL hello nie jest jeszcze uruchomiona w tym wystąpieniu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83e38-243">You might experience this issue if hello MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="83e38-244">tooresolve hello problem, spróbuj tooaccess witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="83e38-244">tooresolve hello issue, try tooaccess your website.</span></span> <span data-ttu-id="83e38-245">Spowoduje to uruchomienie procesów hello wymagane, w tym procesie hello MySQL w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83e38-245">This starts hello required processes, including hello MySQL in-app process.</span></span> <span data-ttu-id="83e38-246">na liście tooverify czy MySQL działa w aplikacji, w Eksploratorze procesu upewnij się, że mysqld.exe hello procesów.</span><span class="sxs-lookup"><span data-stu-id="83e38-246">tooverify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in hello processes.</span></span>

<span data-ttu-id="83e38-247">Po upewnieniu się, że działa MySQL w aplikacji, spróbuj toouse PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="83e38-247">After you ensure that MySQL in-app is running, try toouse PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="83e38-248">Błąd HTTP 403 I spróbuj tooimport lub eksportu bazy danych MySQL w aplikacji przy użyciu PHPMyadmin.</span><span class="sxs-lookup"><span data-stu-id="83e38-248">I get an HTTP 403 error when I try tooimport or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="83e38-249">Jak rozwiązać ten problem?</span><span class="sxs-lookup"><span data-stu-id="83e38-249">How do I resolve this?</span></span>

<span data-ttu-id="83e38-250">Jeśli używasz starszej wersji przeglądarki Chrome, mogą występować znaną usterką.</span><span class="sxs-lookup"><span data-stu-id="83e38-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="83e38-251">tooresolve hello problem uaktualnienia tooa nowszej wersji programu Chrome.</span><span class="sxs-lookup"><span data-stu-id="83e38-251">tooresolve hello issue, upgrade tooa newer version of Chrome.</span></span> <span data-ttu-id="83e38-252">Spróbuj również przy użyciu innej przeglądarki, takich jak program Internet Explorer lub Edge, gdzie hello problem nie występuje.</span><span class="sxs-lookup"><span data-stu-id="83e38-252">Also try using a different browser, like Internet Explorer or Edge, where hello issue does not occur.</span></span>
