---
title: "Systemy z usługi Azure Logic Apps plików lokalnych tooon aaaConnect | Dokumentacja firmy Microsoft"
description: "Nawiązywanie połączenia tooon lokalnych systemów plików z przepływu pracy aplikacji logiki za pośrednictwem bramy danych lokalne powitania i łącznika systemu plików"
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
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a><span data-ttu-id="05101-104">Połącz tooon lokalnych systemów plików z aplikacji logiki z hello łącznika systemu plików</span><span class="sxs-lookup"><span data-stu-id="05101-104">Connect tooon-premises file systems from logic apps with hello File System connector</span></span>

<span data-ttu-id="05101-105">Połączenia hybrydowe chmury jest centralna toologic aplikacji, danych tak toomanage i bezpiecznego dostępu do zasobów lokalnych, aplikacje logiki można użyć bramy danych lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="05101-105">Hybrid cloud connectivity is central toologic apps, so toomanage data and securely access on-premises resources, your logic apps can use hello on-premises data gateway.</span></span> <span data-ttu-id="05101-106">W tym artykule zostanie przedstawiony sposób tooconnect tooan lokalnego systemu plików za pomocą podstawowy scenariusz: Skopiuj plik to jest tooa przekazane tooDropbox udziału plików, a następnie wyślij wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="05101-106">In this article, we show how tooconnect tooan on-premises file system with a basic scenario: copy a file that's uploaded tooDropbox tooa file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05101-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="05101-107">Prerequisites</span></span>

- <span data-ttu-id="05101-108">Instalowanie i konfigurowanie hello najnowszych [bramy danych lokalnych](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="05101-108">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="05101-109">Instalowanie hello najnowszej bramy danych lokalnych, wersji 1.15.6150.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="05101-109">Install hello latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="05101-110">[Połączenie bramy danych lokalnych toohello](http://aka.ms/logicapps-gateway) list hello kroki.</span><span class="sxs-lookup"><span data-stu-id="05101-110">[Connect toohello on-premises data gateway](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="05101-111">Brama Hello musi zostać zainstalowana na maszynie lokalnej, przed kontynuowaniem hello pozostałe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="05101-111">hello gateway must be installed on an on-premises machine before you can continue with hello rest of hello steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a><span data-ttu-id="05101-112">Dodaj wyzwalacza i akcje podłączania tooyour systemu plików</span><span class="sxs-lookup"><span data-stu-id="05101-112">Add trigger and actions for connecting tooyour file system</span></span>

1. <span data-ttu-id="05101-113">Tworzenie aplikacji logiki, a następnie dodaj ten wyzwalacz Dropbox: **utworzenia pliku**</span><span class="sxs-lookup"><span data-stu-id="05101-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="05101-114">W obszarze hello wyzwalacza, wybierz **następnego kroku** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="05101-114">Under hello trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="05101-115">W polu wyszukiwania hello wpisz `file system` , aby wyświetlić wszystkie obsługiwane akcje hello łącznika systemu plików.</span><span class="sxs-lookup"><span data-stu-id="05101-115">In hello search box, enter `file system` so you can view all supported actions for hello File System connector.</span></span>

   ![Wyszukiwanie plików łącznika](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="05101-117">Wybierz hello **Utwórz plik** akcji i utworzyć systemu plików tooyour połączenia.</span><span class="sxs-lookup"><span data-stu-id="05101-117">Choose hello **Create file** action, and create a connection tooyour file system.</span></span>

   <span data-ttu-id="05101-118">Jeśli nie masz istniejące połączenie, to zostanie wyświetlony monit o toocreate, jeden.</span><span class="sxs-lookup"><span data-stu-id="05101-118">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="05101-119">Wybierz **Połącz za pośrednictwem bramy danych lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="05101-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="05101-120">Więcej właściwości są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="05101-120">More properties appear.</span></span>
   2. <span data-ttu-id="05101-121">Wybierz folder główny dla systemu plików.</span><span class="sxs-lookup"><span data-stu-id="05101-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="05101-122">folder główny Hello jest folderu nadrzędnego głównego hello, który jest używany dla ścieżek względnych dla wszystkich akcji związanych z pliku.</span><span class="sxs-lookup"><span data-stu-id="05101-122">hello root folder is hello main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="05101-123">Można określić folderu lokalnego na maszynie hello, w której zainstalowano bramę danych lokalne powitania lub hello folder może być udział sieciowy, który hello komputer może uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="05101-123">You can specify a local folder on hello machine where hello on-premises data gateway is installed, or hello folder can be a network share that hello machine can access.</span></span>

   3. <span data-ttu-id="05101-124">Wprowadź bramy hello hello nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="05101-124">Enter hello username and password for hello gateway.</span></span>
   4. <span data-ttu-id="05101-125">Wybierz bramę hello, która została wcześniej zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="05101-125">Select hello gateway that you previously installed.</span></span>

       ![Skonfiguruj połączenie](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="05101-127">Po podaniu wszystkich szczegółów hello wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="05101-127">After you provide all hello details, choose **Create**.</span></span> 

   <span data-ttu-id="05101-128">Logic Apps konfiguruje i testuje połączenie, upewniając się, czy hello połączenie działa poprawnie.</span><span class="sxs-lookup"><span data-stu-id="05101-128">Logic Apps configures and tests your connection, making sure that hello connection works properly.</span></span> 
   <span data-ttu-id="05101-129">Jeśli połączenie hello jest poprawnie skonfigurowane, zobaczysz opcji dla akcji hello, które wcześniej wybrano.</span><span class="sxs-lookup"><span data-stu-id="05101-129">If hello connection is set up correctly, you see options for hello action that you previously selected.</span></span> 
   <span data-ttu-id="05101-130">Łącznik programu system plików Hello jest teraz gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="05101-130">hello file system connector is now ready for use.</span></span>

4. <span data-ttu-id="05101-131">Określ czy toocopy pliki z folderu głównego toohello skrzynki dla udziału plików lokalnych.</span><span class="sxs-lookup"><span data-stu-id="05101-131">Specify that you want toocopy files from Dropbox toohello root folder for your on-premises file share.</span></span>

   ![Utworzenie pliku](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="05101-133">Po pliku hello kopie aplikacji logiki dodać akcję programu Outlook, która wysyła wiadomość e-mail, więc odpowiednich użytkowników wiedzieć o hello nowy plik.</span><span class="sxs-lookup"><span data-stu-id="05101-133">After your logic app copies hello file, add an Outlook action that sends an email so relevant users know about hello new file.</span></span> <span data-ttu-id="05101-134">Wprowadź hello adresatów, tytuł i treść wiadomości e-mail hello.</span><span class="sxs-lookup"><span data-stu-id="05101-134">Enter hello recipients, title, and body of hello email.</span></span> 

   <span data-ttu-id="05101-135">W hello dynamiczne selektora zawartości można wybrać danych wyjściowych z hello pliku łącznika, dodając więcej szczegółów toohello e-mail.</span><span class="sxs-lookup"><span data-stu-id="05101-135">In hello dynamic content selector, you can choose data outputs from hello file connector so you can add more details toohello email.</span></span>

   ![Wysłanie wiadomości e-mail](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="05101-137">Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="05101-137">Save your logic app.</span></span> <span data-ttu-id="05101-138">Testowanie aplikacji, przekazując tooDropbox pliku.</span><span class="sxs-lookup"><span data-stu-id="05101-138">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="05101-139">Hello pliku należy uzyskać udział pliku lokalnego toohello skopiowane, a użytkownik powinien otrzymywać wiadomość e-mail o hello operacji.</span><span class="sxs-lookup"><span data-stu-id="05101-139">hello file should get copied toohello on-premises file share, and you should receive an email about hello operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="05101-140">Dowiedz się, jak za[Monitoruj aplikacje logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="05101-140">Learn how too[monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="05101-141">Gratulacje, masz teraz pracy aplikacji logiki podłączoną tooyour lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="05101-141">Congratulations, you now have a working logic app that can connect tooyour on-premises file system.</span></span> <span data-ttu-id="05101-142">Spróbuj eksploracji inne funkcje, które hello oferty łącznika, na przykład:</span><span class="sxs-lookup"><span data-stu-id="05101-142">Try exploring other functionalities that hello connector offers, for example:</span></span>

- <span data-ttu-id="05101-143">Utwórz plik</span><span class="sxs-lookup"><span data-stu-id="05101-143">Create file</span></span>
- <span data-ttu-id="05101-144">Wyświetl listę plików w folderze</span><span class="sxs-lookup"><span data-stu-id="05101-144">List files in folder</span></span>
- <span data-ttu-id="05101-145">Dołącz plik</span><span class="sxs-lookup"><span data-stu-id="05101-145">Append file</span></span>
- <span data-ttu-id="05101-146">Usuń plik</span><span class="sxs-lookup"><span data-stu-id="05101-146">Delete file</span></span>
- <span data-ttu-id="05101-147">Pobierz zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="05101-147">Get file content</span></span>
- <span data-ttu-id="05101-148">Pobierz zawartość pliku przy użyciu ścieżki</span><span class="sxs-lookup"><span data-stu-id="05101-148">Get file content using path</span></span>
- <span data-ttu-id="05101-149">Pobierz plik metadanych</span><span class="sxs-lookup"><span data-stu-id="05101-149">Get file metadata</span></span>
- <span data-ttu-id="05101-150">Pobierz metadane pliku przy użyciu ścieżki</span><span class="sxs-lookup"><span data-stu-id="05101-150">Get file metadata using path</span></span>
- <span data-ttu-id="05101-151">Wyświetl listę plików w folderze głównym</span><span class="sxs-lookup"><span data-stu-id="05101-151">List files in root folder</span></span>
- <span data-ttu-id="05101-152">Plik aktualizacji</span><span class="sxs-lookup"><span data-stu-id="05101-152">Update file</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="05101-153">Widok hello swagger</span><span class="sxs-lookup"><span data-stu-id="05101-153">View hello swagger</span></span>
<span data-ttu-id="05101-154">Zobacz hello [swagger szczegóły](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="05101-154">See hello [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="05101-155">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="05101-155">Get help</span></span>

<span data-ttu-id="05101-156">pytania tooask odpowiedzi na pytania i Dowiedz się, jakie inne usługi Azure Logic Apps robią użytkownicy, odwiedź stronę hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="05101-156">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="05101-157">toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="05101-157">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05101-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05101-158">Next steps</span></span>

- <span data-ttu-id="05101-159">[Połącz dane lokalne tooon](../logic-apps/logic-apps-gateway-connection.md) z aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="05101-159">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="05101-160">Dowiedz się więcej o [integracji przedsiębiorstwa](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="05101-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
