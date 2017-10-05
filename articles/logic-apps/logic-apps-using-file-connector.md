---
title: "Nawiązywanie połączenia systemów plików lokalnych z usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Nawiązywanie połączenia systemów plików lokalnych z przepływu pracy aplikacji logiki za pomocą bramy danych lokalnych i łącznika systemu plików"
keywords: "systemy plików"
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: f33e7c58103c57e17e4e273caba1ab9b83f0cd2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a><span data-ttu-id="84cea-104">Nawiązywanie połączenia systemów lokalnych plików z aplikacji logiki w usłudze łącznika systemu plików</span><span class="sxs-lookup"><span data-stu-id="84cea-104">Connect to on-premises file systems from logic apps with the File System connector</span></span>

<span data-ttu-id="84cea-105">Połączenia hybrydowe chmury jest centralnej do aplikacji logiki, więc można zarządzać danymi i bezpieczny dostęp do zasobów lokalnych, aplikacje logiki można użyć bramy danych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="84cea-105">Hybrid cloud connectivity is central to logic apps, so to manage data and securely access on-premises resources, your logic apps can use the on-premises data gateway.</span></span> <span data-ttu-id="84cea-106">W tym artykule zostanie przedstawiony sposób nawiązywania połączenia z lokalnego systemu plików ze scenariuszem podstawowe: skopiować plik, który jest przekazywany do usługi Dropbox do udziału plików, a następnie wyślij wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="84cea-106">In this article, we show how to connect to an on-premises file system with a basic scenario: copy a file that's uploaded to Dropbox to a file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84cea-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="84cea-107">Prerequisites</span></span>

- <span data-ttu-id="84cea-108">Instalowanie i Konfigurowanie r [bramy danych lokalnych](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="84cea-108">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="84cea-109">Zainstaluj najnowszą bramę danych lokalnych, wersji 1.15.6150.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="84cea-109">Install the latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="84cea-110">[Łączenie się z bramą danych lokalnych](http://aka.ms/logicapps-gateway) zawiera listę czynności.</span><span class="sxs-lookup"><span data-stu-id="84cea-110">[Connect to the on-premises data gateway](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="84cea-111">Brama musi zainstalowana na maszynie lokalnej, zanim będzie można kontynuować z pozostałych kroków.</span><span class="sxs-lookup"><span data-stu-id="84cea-111">The gateway must be installed on an on-premises machine before you can continue with the rest of the steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a><span data-ttu-id="84cea-112">Dodaj wyzwalacza oraz do nawiązywania połączenia z systemu plików</span><span class="sxs-lookup"><span data-stu-id="84cea-112">Add trigger and actions for connecting to your file system</span></span>

1. <span data-ttu-id="84cea-113">Tworzenie aplikacji logiki, a następnie dodaj ten wyzwalacz Dropbox: **utworzenia pliku**</span><span class="sxs-lookup"><span data-stu-id="84cea-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="84cea-114">W obszarze wyzwalacza, wybierz **następnego kroku** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="84cea-114">Under the trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="84cea-115">W polu wyszukiwania wprowadź `file system` , aby wyświetlić wszystkie obsługiwane akcje dla łącznika systemu plików.</span><span class="sxs-lookup"><span data-stu-id="84cea-115">In the search box, enter `file system` so you can view all supported actions for the File System connector.</span></span>

   ![Wyszukiwanie plików łącznika](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="84cea-117">Wybierz **Utwórz plik** akcji i utworzyć połączenie z systemu plików.</span><span class="sxs-lookup"><span data-stu-id="84cea-117">Choose the **Create file** action, and create a connection to your file system.</span></span>

   <span data-ttu-id="84cea-118">Nie masz istniejące połączenie, monit o jego utworzenie.</span><span class="sxs-lookup"><span data-stu-id="84cea-118">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="84cea-119">Wybierz **Połącz za pośrednictwem bramy danych lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="84cea-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="84cea-120">Więcej właściwości są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="84cea-120">More properties appear.</span></span>
   2. <span data-ttu-id="84cea-121">Wybierz folder główny dla systemu plików.</span><span class="sxs-lookup"><span data-stu-id="84cea-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="84cea-122">Folder główny jest folderu nadrzędnego głównego, który jest używany dla ścieżek względnych dla wszystkich akcji związanych z pliku.</span><span class="sxs-lookup"><span data-stu-id="84cea-122">The root folder is the main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="84cea-123">Można określić lokalny folder na komputerze, na którym zainstalowano bramę danych lokalnych lub może to być udział sieciowy, który ma dostęp maszyna.</span><span class="sxs-lookup"><span data-stu-id="84cea-123">You can specify a local folder on the machine where the on-premises data gateway is installed, or the folder can be a network share that the machine can access.</span></span>

   3. <span data-ttu-id="84cea-124">Wprowadź nazwę użytkownika i hasło dla bramy.</span><span class="sxs-lookup"><span data-stu-id="84cea-124">Enter the username and password for the gateway.</span></span>
   4. <span data-ttu-id="84cea-125">Wybierz bramę, która została wcześniej zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="84cea-125">Select the gateway that you previously installed.</span></span>

       ![Skonfiguruj połączenie](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="84cea-127">Po podaniu wszystkie szczegóły, wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="84cea-127">After you provide all the details, choose **Create**.</span></span> 

   <span data-ttu-id="84cea-128">Logic Apps konfiguruje i testuje połączenie, upewniając się, że połączenie działa poprawnie.</span><span class="sxs-lookup"><span data-stu-id="84cea-128">Logic Apps configures and tests your connection, making sure that the connection works properly.</span></span> 
   <span data-ttu-id="84cea-129">Jeśli połączenie jest poprawnie skonfigurowane, zobaczysz opcji dla akcji, która wcześniej została zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="84cea-129">If the connection is set up correctly, you see options for the action that you previously selected.</span></span> 
   <span data-ttu-id="84cea-130">Łącznik systemu plików jest teraz gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="84cea-130">The file system connector is now ready for use.</span></span>

4. <span data-ttu-id="84cea-131">Określ chcesz skopiować pliki z Dropbox do folderu głównego dla udziału plików lokalnych.</span><span class="sxs-lookup"><span data-stu-id="84cea-131">Specify that you want to copy files from Dropbox to the root folder for your on-premises file share.</span></span>

   ![Utworzenie pliku](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="84cea-133">Po aplikację logiki kopiuje plik, należy dodać akcję programu Outlook, która wysyła wiadomość e-mail, więc odpowiednich użytkowników wiedzieć o nowy plik.</span><span class="sxs-lookup"><span data-stu-id="84cea-133">After your logic app copies the file, add an Outlook action that sends an email so relevant users know about the new file.</span></span> <span data-ttu-id="84cea-134">Wprowadź adresatów, tytuł i treść wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="84cea-134">Enter the recipients, title, and body of the email.</span></span> 

   <span data-ttu-id="84cea-135">W selektorze zawartości dynamicznej można danych wyjściowych z łącznika plików, dodając więcej szczegółowych informacji do wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="84cea-135">In the dynamic content selector, you can choose data outputs from the file connector so you can add more details to the email.</span></span>

   ![Wysłanie wiadomości e-mail](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="84cea-137">Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="84cea-137">Save your logic app.</span></span> <span data-ttu-id="84cea-138">Testowanie aplikacji, przekazując plik do skrzynki.</span><span class="sxs-lookup"><span data-stu-id="84cea-138">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="84cea-139">Plik powinien pobrać skopiowane do udziału pliku lokalnego, a użytkownik powinien otrzymywać wiadomości e-mail dotyczące działania.</span><span class="sxs-lookup"><span data-stu-id="84cea-139">The file should get copied to the on-premises file share, and you should receive an email about the operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="84cea-140">Dowiedz się, jak [Monitoruj aplikacje logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="84cea-140">Learn how to [monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="84cea-141">Gratulacje, masz teraz pracy aplikacji logiki, który może łączyć się z lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="84cea-141">Congratulations, you now have a working logic app that can connect to your on-premises file system.</span></span> <span data-ttu-id="84cea-142">Spróbuj eksploracji inne funkcje, które oferuje łącznika, na przykład:</span><span class="sxs-lookup"><span data-stu-id="84cea-142">Try exploring other functionalities that the connector offers, for example:</span></span>

- <span data-ttu-id="84cea-143">Utwórz plik</span><span class="sxs-lookup"><span data-stu-id="84cea-143">Create file</span></span>
- <span data-ttu-id="84cea-144">Wyświetl listę plików w folderze</span><span class="sxs-lookup"><span data-stu-id="84cea-144">List files in folder</span></span>
- <span data-ttu-id="84cea-145">Dołącz plik</span><span class="sxs-lookup"><span data-stu-id="84cea-145">Append file</span></span>
- <span data-ttu-id="84cea-146">Usuń plik</span><span class="sxs-lookup"><span data-stu-id="84cea-146">Delete file</span></span>
- <span data-ttu-id="84cea-147">Pobierz zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="84cea-147">Get file content</span></span>
- <span data-ttu-id="84cea-148">Pobierz zawartość pliku przy użyciu ścieżki</span><span class="sxs-lookup"><span data-stu-id="84cea-148">Get file content using path</span></span>
- <span data-ttu-id="84cea-149">Pobierz plik metadanych</span><span class="sxs-lookup"><span data-stu-id="84cea-149">Get file metadata</span></span>
- <span data-ttu-id="84cea-150">Pobierz metadane pliku przy użyciu ścieżki</span><span class="sxs-lookup"><span data-stu-id="84cea-150">Get file metadata using path</span></span>
- <span data-ttu-id="84cea-151">Wyświetl listę plików w folderze głównym</span><span class="sxs-lookup"><span data-stu-id="84cea-151">List files in root folder</span></span>
- <span data-ttu-id="84cea-152">Plik aktualizacji</span><span class="sxs-lookup"><span data-stu-id="84cea-152">Update file</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="84cea-153">Wyświetlanie struktury swagger</span><span class="sxs-lookup"><span data-stu-id="84cea-153">View the swagger</span></span>
<span data-ttu-id="84cea-154">Zobacz [swagger szczegóły](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="84cea-154">See the [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="84cea-155">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="84cea-155">Get help</span></span>

<span data-ttu-id="84cea-156">Aby zadawać pytania, odpowiadać na nie i patrzeć, co robią inni użytkownicy usługi Azure Logic Apps, odwiedź [forum usługi Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="84cea-156">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="84cea-157">Aby pomóc w ulepszaniu usługi Azure Logic Apps, przesyłaj pomysły lub głosuj na nie w [witrynie opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="84cea-157">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="84cea-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84cea-158">Next steps</span></span>

- <span data-ttu-id="84cea-159">[Połącz się z lokalnymi danymi](../logic-apps/logic-apps-gateway-connection.md) z aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="84cea-159">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="84cea-160">Dowiedz się więcej o [integracji przedsiębiorstwa](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="84cea-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
