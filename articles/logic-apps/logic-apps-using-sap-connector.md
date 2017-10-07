---
title: aaaConnect tooan lokalnego systemu SAP w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft
description: "Połącz z przepływu pracy aplikacji logiki za pośrednictwem bramy danych lokalne powitania tooan lokalnego systemu SAP"
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
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a><span data-ttu-id="c2487-103">Połącz z aplikacji logiki z łącznikiem SAP hello tooan lokalnego systemu SAP</span><span class="sxs-lookup"><span data-stu-id="c2487-103">Connect tooan on-premises SAP system from logic apps with hello SAP connector</span></span> 

<span data-ttu-id="c2487-104">Brama danych lokalne powitania pozwala toomanage danych i bezpieczny dostęp do zasobów, które znajdują się na obszarze.</span><span class="sxs-lookup"><span data-stu-id="c2487-104">hello on-premises data gateway enables you toomanage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="c2487-105">W tym temacie przedstawiono, jak można łączyć logic apps tooan lokalnego SAP systemu.</span><span class="sxs-lookup"><span data-stu-id="c2487-105">This topic shows how you can connect logic apps tooan on-premises SAP system.</span></span> <span data-ttu-id="c2487-106">W tym przykładzie aplikację logiki żądań IDOC za pośrednictwem protokołu HTTP i wysyła odpowiedź hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="c2487-106">In this example, your logic app requests an IDOC over HTTP and sends hello response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="c2487-107">Bieżące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="c2487-107">Current limitations:</span></span> 
> - <span data-ttu-id="c2487-108">Jeśli wszystkie kroki wymagane do odpowiedzi hello nie zakończy się w obrębie hello limitu czasu aplikację logiki [limit czasu żądania](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="c2487-108">Your logic app times out if all steps required for hello response don't finish within hello [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="c2487-109">W tym scenariuszu może pobrać zablokowane żądania.</span><span class="sxs-lookup"><span data-stu-id="c2487-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="c2487-110">selektor plików Hello nie są wyświetlane wszystkie dostępne pola hello.</span><span class="sxs-lookup"><span data-stu-id="c2487-110">hello file picker does not display all hello available fields.</span></span> <span data-ttu-id="c2487-111">W tym scenariuszu można ręcznie dodać ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c2487-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2487-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c2487-112">Prerequisites</span></span>

- <span data-ttu-id="c2487-113">Instalowanie i konfigurowanie hello najnowszych [bramy danych lokalnych](https://www.microsoft.com/download/details.aspx?id=53127) wersji 1.15.6150.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c2487-113">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="c2487-114">[Jak tooconnect toohello lokalną bramę danych w aplikacji logiki](http://aka.ms/logicapps-gateway) list hello kroki.</span><span class="sxs-lookup"><span data-stu-id="c2487-114">[How tooconnect toohello on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="c2487-115">Brama Hello musi zostać zainstalowana na maszynie lokalnej, zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="c2487-115">hello gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="c2487-116">Pobierz i zainstaluj hello najnowsze SAP biblioteki klienta na powitania sam komputera, w którym zainstalowano bramę danych hello.</span><span class="sxs-lookup"><span data-stu-id="c2487-116">Download and install hello latest SAP client library on hello same machine where you installed hello data gateway.</span></span> <span data-ttu-id="c2487-117">Użyj dowolnej z hello następujące wersje programu SAP:</span><span class="sxs-lookup"><span data-stu-id="c2487-117">Use any of hello following SAP versions:</span></span> 
    - <span data-ttu-id="c2487-118">Serwerem SAP</span><span class="sxs-lookup"><span data-stu-id="c2487-118">SAP Server</span></span>
        - <span data-ttu-id="c2487-119">Dowolnego serwera SAP hello tej obsługi łącznika .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="c2487-119">Any SAP Server that support hello .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="c2487-120">Klient programu SAP</span><span class="sxs-lookup"><span data-stu-id="c2487-120">SAP Client</span></span>
        - <span data-ttu-id="c2487-121">Łącznik .NET programu SAP (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="c2487-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a><span data-ttu-id="c2487-122">Dodaj wyzwalacze i akcje podłączania tooyour systemu SAP</span><span class="sxs-lookup"><span data-stu-id="c2487-122">Add triggers and actions for connecting tooyour SAP system</span></span>

<span data-ttu-id="c2487-123">Łącznik programu SAP Hello ma działania, ale nie wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="c2487-123">hello SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="c2487-124">Tak mamy toouse inny wyzwalacz na początku hello hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="c2487-124">So, we have toouse another trigger at hello start of hello workflow.</span></span> 

1. <span data-ttu-id="c2487-125">Dodaj hello wyzwalacza żądanie/odpowiedź, a następnie wybierz **nowy krok**.</span><span class="sxs-lookup"><span data-stu-id="c2487-125">Add hello Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="c2487-126">Wybierz **Dodaj akcję**, a następnie wybierz łącznik SAP hello wpisując `SAP` w polu wyszukiwania hello:</span><span class="sxs-lookup"><span data-stu-id="c2487-126">Select **Add an action**, and then select hello SAP connector by typing `SAP` in hello search field:</span></span>    

     ![Wybierz serwer aplikacji SAP lub serwer komunikatów SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="c2487-128">Wybierz [ **serwera aplikacji SAP** ](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) lub [ **serwer komunikatów SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), oparte na ustawieniach SAP.</span><span class="sxs-lookup"><span data-stu-id="c2487-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="c2487-129">Jeśli nie masz istniejące połączenie, to zostanie wyświetlony monit o toocreate, jeden.</span><span class="sxs-lookup"><span data-stu-id="c2487-129">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="c2487-130">Wybierz **Połącz za pośrednictwem bramy danych lokalnych**, a następnie wprowadź szczegóły hello systemu SAP:</span><span class="sxs-lookup"><span data-stu-id="c2487-130">Select **Connect via on-premises data gateway**, and enter hello details for your SAP system:</span></span>   

       ![Dodaj tooSAP ciąg połączenia](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="c2487-132">W obszarze **bramy**, wybierz istniejącą bramę lub tooinstall nową bramę, wybierz **zainstalować bramę**.</span><span class="sxs-lookup"><span data-stu-id="c2487-132">Under **Gateway**, select an existing gateway, or tooinstall a new gateway, select **Install Gateway**.</span></span>

        ![Instalowanie nowej bramy](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="c2487-134">Po wprowadzeniu wszystkich szczegółów hello wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c2487-134">After you enter all hello details, select **Create**.</span></span> 
   <span data-ttu-id="c2487-135">Logic Apps konfiguruje i testuje połączenie hello, upewniając się, czy hello połączenie działa poprawnie.</span><span class="sxs-lookup"><span data-stu-id="c2487-135">Logic Apps configures and tests hello connection, making sure that hello connection works properly.</span></span>

4. <span data-ttu-id="c2487-136">Wprowadź nazwę dla połączenia SAP.</span><span class="sxs-lookup"><span data-stu-id="c2487-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="c2487-137">obecnie dostępne są różne opcje SAP Hello.</span><span class="sxs-lookup"><span data-stu-id="c2487-137">hello different SAP options are now available.</span></span> <span data-ttu-id="c2487-138">toofind IDOC kategorii, wybierz z listy hello.</span><span class="sxs-lookup"><span data-stu-id="c2487-138">toofind your IDOC category, select from hello list.</span></span> <span data-ttu-id="c2487-139">Lub ręcznie wpisać ścieżkę hello i odpowiedź wybierz hello HTTP w hello **treści** pola:</span><span class="sxs-lookup"><span data-stu-id="c2487-139">Or manually type in hello path, and select hello HTTP response in hello **body** field:</span></span>

     ![Akcja SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="c2487-141">Dodaj akcję hello tworzenia **odpowiedzi HTTP**.</span><span class="sxs-lookup"><span data-stu-id="c2487-141">Add hello action for creating an **HTTP Response**.</span></span> <span data-ttu-id="c2487-142">komunikat odpowiedzi Hello powinien być z hello SAP w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c2487-142">hello response message should be from hello SAP output.</span></span>

7. <span data-ttu-id="c2487-143">Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="c2487-143">Save your logic app.</span></span> <span data-ttu-id="c2487-144">Przetestować, wysyłając IDOC za pomocą adresu URL wyzwalacza hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="c2487-144">Test it by sending an IDOC through hello HTTP trigger URL.</span></span> <span data-ttu-id="c2487-145">Po hello wysłania IDOC poczekaj, aż hello odpowiedzi z aplikacji logiki hello:</span><span class="sxs-lookup"><span data-stu-id="c2487-145">After hello IDOC is sent, wait for hello response from hello logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="c2487-146">Sprawdź, jak za[Monitoruj aplikacje logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c2487-146">Check out how too[monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="c2487-147">Teraz, gdy łącznik SAP hello jest dodawany tooyour aplikacji logiki, rozpocząć eksplorowanie inne funkcje:</span><span class="sxs-lookup"><span data-stu-id="c2487-147">Now that hello SAP connector is added tooyour logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="c2487-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="c2487-148">BAPI</span></span>
- <span data-ttu-id="c2487-149">RFC</span><span class="sxs-lookup"><span data-stu-id="c2487-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="c2487-150">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="c2487-150">Get help</span></span>

<span data-ttu-id="c2487-151">pytania tooask odpowiedzi na pytania i Dowiedz się, jakie inne usługi Azure Logic Apps robią użytkownicy, odwiedź stronę hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="c2487-151">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="c2487-152">toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="c2487-152">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2487-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2487-153">Next steps</span></span>

- <span data-ttu-id="c2487-154">Dowiedz się, jak toovalidate, przekształcanie i inne funkcje BizTalk przypominającej hello [pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2487-154">Learn how toovalidate, transform, and other BizTalk-like functions in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="c2487-155">[Połącz dane lokalne tooon](../logic-apps/logic-apps-gateway-connection.md) z aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="c2487-155">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
