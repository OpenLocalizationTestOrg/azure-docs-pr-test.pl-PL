---
title: "Nawiązać połączenia z lokalnego systemu SAP w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Nawiązywanie połączenia lokalnego systemu SAP z przepływu pracy aplikacji logiki za pośrednictwem bramy danych lokalnych"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 3fea93f558d5a4ef62550fd1f6486903cb812930
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-on-premises-sap-system-from-logic-apps-with-the-sap-connector"></a><span data-ttu-id="b7f6a-103">Nawiązywanie połączenia lokalnego systemu SAP z aplikacji logiki z łącznikiem SAP</span><span class="sxs-lookup"><span data-stu-id="b7f6a-103">Connect to an on-premises SAP system from logic apps with the SAP connector</span></span> 

<span data-ttu-id="b7f6a-104">Brama lokalna danych pozwala na zarządzanie danymi i bezpieczny dostęp do zasobów, które znajdują się na obszarze.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-104">The on-premises data gateway enables you to manage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="b7f6a-105">W tym temacie przedstawiono sposób podłączenia aplikacji logiki do lokalnego systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-105">This topic shows how you can connect logic apps to an on-premises SAP system.</span></span> <span data-ttu-id="b7f6a-106">W tym przykładzie aplikację logiki żądań IDOC za pośrednictwem protokołu HTTP i wysyła odpowiedź ponownie.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-106">In this example, your logic app requests an IDOC over HTTP and sends the response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="b7f6a-107">Bieżące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="b7f6a-107">Current limitations:</span></span> 
> - <span data-ttu-id="b7f6a-108">Jeśli wszystkie kroki wymagane do odpowiedzi nie zakończy się w ramach limitu czasu aplikację logiki [limit czasu żądania](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="b7f6a-108">Your logic app times out if all steps required for the response don't finish within the [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="b7f6a-109">W tym scenariuszu może pobrać zablokowane żądania.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="b7f6a-110">Selektor plików nie są wyświetlane wszystkie dostępne pola.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-110">The file picker does not display all the available fields.</span></span> <span data-ttu-id="b7f6a-111">W tym scenariuszu można ręcznie dodać ścieżki.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7f6a-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b7f6a-112">Prerequisites</span></span>

- <span data-ttu-id="b7f6a-113">Instalowanie i Konfigurowanie r [bramy danych lokalnych](https://www.microsoft.com/download/details.aspx?id=53127) wersji 1.15.6150.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-113">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="b7f6a-114">[Jak połączyć się z bramą danych lokalnych w aplikacji logiki](http://aka.ms/logicapps-gateway) zawiera listę czynności.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-114">[How to connect to the on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="b7f6a-115">Bramy muszą można zainstalować na maszynie lokalnej, zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-115">The gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="b7f6a-116">Pobierz i zainstaluj najnowsze biblioteki klienckiej SAP na tym samym komputerze, na którym zainstalowano bramę danych.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-116">Download and install the latest SAP client library on the same machine where you installed the data gateway.</span></span> <span data-ttu-id="b7f6a-117">Użyj jednej z następujących wersji programu SAP:</span><span class="sxs-lookup"><span data-stu-id="b7f6a-117">Use any of the following SAP versions:</span></span> 
    - <span data-ttu-id="b7f6a-118">Serwerem SAP</span><span class="sxs-lookup"><span data-stu-id="b7f6a-118">SAP Server</span></span>
        - <span data-ttu-id="b7f6a-119">Dowolnego serwera SAP, który obsługuje łącznik .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="b7f6a-119">Any SAP Server that support the .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="b7f6a-120">Klient programu SAP</span><span class="sxs-lookup"><span data-stu-id="b7f6a-120">SAP Client</span></span>
        - <span data-ttu-id="b7f6a-121">Łącznik .NET programu SAP (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="b7f6a-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-to-your-sap-system"></a><span data-ttu-id="b7f6a-122">Dodaj wyzwalacze i akcje w celu nawiązania systemu SAP</span><span class="sxs-lookup"><span data-stu-id="b7f6a-122">Add triggers and actions for connecting to your SAP system</span></span>

<span data-ttu-id="b7f6a-123">Łącznik programu SAP ma działania, ale nie wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-123">The SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="b7f6a-124">Tak musimy użyć innego wyzwalacza podczas uruchamiania przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-124">So, we have to use another trigger at the start of the workflow.</span></span> 

1. <span data-ttu-id="b7f6a-125">Dodaj wyzwalacza żądanie/odpowiedź, a następnie wybierz **nowy krok**.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-125">Add the Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="b7f6a-126">Wybierz **Dodaj akcję**, a następnie wybierz łącznik programu SAP, wpisując `SAP` w polu wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="b7f6a-126">Select **Add an action**, and then select the SAP connector by typing `SAP` in the search field:</span></span>    

     ![Wybierz serwer aplikacji SAP lub serwer komunikatów SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="b7f6a-128">Wybierz [ **serwera aplikacji SAP** ](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) lub [ **serwer komunikatów SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), oparte na ustawieniach SAP.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="b7f6a-129">Nie masz istniejące połączenie, monit o jego utworzenie.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-129">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="b7f6a-130">Wybierz **Połącz za pośrednictwem bramy danych lokalnych**, a następnie wprowadź szczegóły systemu SAP:</span><span class="sxs-lookup"><span data-stu-id="b7f6a-130">Select **Connect via on-premises data gateway**, and enter the details for your SAP system:</span></span>   

       ![Dodaj ciąg połączenia SAP](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="b7f6a-132">W obszarze **bramy**, wybierz istniejącą bramę lub aby zainstalować nową bramę, **zainstalować bramę**.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-132">Under **Gateway**, select an existing gateway, or to install a new gateway, select **Install Gateway**.</span></span>

        ![Instalowanie nowej bramy](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="b7f6a-134">Po wprowadzeniu wszystkich szczegółów zaznacz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-134">After you enter all the details, select **Create**.</span></span> 
   <span data-ttu-id="b7f6a-135">Logic Apps konfiguruje i testuje połączenie, upewniając się, że połączenie działa poprawnie.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-135">Logic Apps configures and tests the connection, making sure that the connection works properly.</span></span>

4. <span data-ttu-id="b7f6a-136">Wprowadź nazwę dla połączenia SAP.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="b7f6a-137">Teraz są dostępne różne opcje SAP.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-137">The different SAP options are now available.</span></span> <span data-ttu-id="b7f6a-138">Aby znaleźć kategorię IDOC, wybierz z listy.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-138">To find your IDOC category, select from the list.</span></span> <span data-ttu-id="b7f6a-139">Ręcznie wpisać ścieżkę lub wybierz odpowiedź HTTP w **treści** pola:</span><span class="sxs-lookup"><span data-stu-id="b7f6a-139">Or manually type in the path, and select the HTTP response in the **body** field:</span></span>

     ![Akcja SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="b7f6a-141">Dodaj akcję tworzenia **odpowiedzi HTTP**.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-141">Add the action for creating an **HTTP Response**.</span></span> <span data-ttu-id="b7f6a-142">Komunikat odpowiedzi powinna być z danych wyjściowych SAP.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-142">The response message should be from the SAP output.</span></span>

7. <span data-ttu-id="b7f6a-143">Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-143">Save your logic app.</span></span> <span data-ttu-id="b7f6a-144">Przetestować, wysyłając IDOC za pomocą adresu URL wyzwalacza HTTP.</span><span class="sxs-lookup"><span data-stu-id="b7f6a-144">Test it by sending an IDOC through the HTTP trigger URL.</span></span> <span data-ttu-id="b7f6a-145">Po wysłaniu IDOC oczekiwania na odpowiedź z aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="b7f6a-145">After the IDOC is sent, wait for the response from the logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="b7f6a-146">Sprawdź informacje dotyczące sposobu [Monitoruj aplikacje logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b7f6a-146">Check out how to [monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="b7f6a-147">Teraz, gdy łącznik SAP jest dodawany do aplikacji logiki, rozpocząć eksplorowanie inne funkcje:</span><span class="sxs-lookup"><span data-stu-id="b7f6a-147">Now that the SAP connector is added to your logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="b7f6a-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="b7f6a-148">BAPI</span></span>
- <span data-ttu-id="b7f6a-149">RFC</span><span class="sxs-lookup"><span data-stu-id="b7f6a-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="b7f6a-150">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="b7f6a-150">Get help</span></span>

<span data-ttu-id="b7f6a-151">Aby zadawać pytania, odpowiadać na nie i patrzeć, co robią inni użytkownicy usługi Azure Logic Apps, odwiedź [forum usługi Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="b7f6a-151">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="b7f6a-152">Aby pomóc w ulepszaniu usługi Azure Logic Apps, przesyłaj pomysły lub głosuj na nie w [witrynie opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="b7f6a-152">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7f6a-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7f6a-153">Next steps</span></span>

- <span data-ttu-id="b7f6a-154">Dowiedz się, jak sprawdzanie poprawności, przekształcania i inne funkcje podobne BizTalk w [pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b7f6a-154">Learn how to validate, transform, and other BizTalk-like functions in the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="b7f6a-155">[Połącz się z lokalnymi danymi](../logic-apps/logic-apps-gateway-connection.md) z aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="b7f6a-155">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
