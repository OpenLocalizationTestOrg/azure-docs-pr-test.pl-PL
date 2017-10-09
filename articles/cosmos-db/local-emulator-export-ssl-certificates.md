---
title: "aaaExport hello Azure rozwiązania Cosmos DB emulatora certyfikatów | Dokumentacja firmy Microsoft"
description: "Podczas tworzenia w językach i środowisk uruchomieniowych, który nie należy używać magazynu certyfikatów systemu Windows hello będą potrzebne tooexport i zarządzać nimi hello certyfikatów SSL. Ten wpis zawiera instrukcje krok po kroku."
services: cosmos-db
documentationcenter: 
keywords: "Emulator usługi Azure rozwiązania Cosmos bazy danych"
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="5f1b9-105">Eksportuj hello Azure rozwiązania Cosmos DB emulatora certyfikatów do użytku z języka Java, Python i Node.js</span><span class="sxs-lookup"><span data-stu-id="5f1b9-105">Export hello Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="5f1b9-106">**Pobierz hello emulatora**</span><span class="sxs-lookup"><span data-stu-id="5f1b9-106">**Download hello Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="5f1b9-107">Hello Azure rozwiązania Cosmos DB emulatora zapewnia środowisko lokalne, które emuluje hello Azure DB rozwiązania Cosmos usługi do celów programistycznych, łącznie z jej użycie połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-107">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="5f1b9-108">Ten wpis pokazano, jak tooexport hello SSL certyfikatów do użytku w językach i środowisk uruchomieniowych, który nie jest integrowana z magazynu certyfikatów systemu Windows, takich jak Java, który używa własnego hello [magazyn certyfikatów](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) i języka Python, który używa [gniazda otoki](https://docs.python.org/2/library/ssl.html) i Node.js, który używa [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="5f1b9-108">This post demonstrates how tooexport hello SSL certificates for use in languages and runtimes that do not integrate with hello Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="5f1b9-109">Więcej o emulator hello w [Użyj hello Azure rozwiązania Cosmos DB emulatora do projektowania i testowania](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="5f1b9-109">You can read more about hello emulator in [Use hello Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="5f1b9-110">Ten samouczek obejmuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="5f1b9-110">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5f1b9-111">Obracanie certyfikatów</span><span class="sxs-lookup"><span data-stu-id="5f1b9-111">Rotating certificates</span></span>
> * <span data-ttu-id="5f1b9-112">Eksportowanie certyfikatu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="5f1b9-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="5f1b9-113">Learning, jak toouse hello certyfikatu w języku Java, Python i Node.js</span><span class="sxs-lookup"><span data-stu-id="5f1b9-113">Learning how toouse hello certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="5f1b9-114">Obracanie certyfikacji</span><span class="sxs-lookup"><span data-stu-id="5f1b9-114">Certification rotation</span></span>

<span data-ttu-id="5f1b9-115">Certyfikaty hello emulatora lokalnej bazy danych usługi Azure rozwiązania Cosmos są generowane hello emulatora hello jest uruchamiany po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-115">Certificates in hello Azure Cosmos DB Local Emulator are generated hello first time hello emulator is run.</span></span> <span data-ttu-id="5f1b9-116">Istnieją dwa certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-116">There are two certificates.</span></span> <span data-ttu-id="5f1b9-117">Jeden służące do połączenia z lokalnym emulatorze toohello i jeden do zarządzania kluczy tajnych w emulatorze hello.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-117">One used for connecting toohello local emulator and one for managing secrets within hello emulator.</span></span> <span data-ttu-id="5f1b9-118">Hello certyfikatów, które chcesz tooexport jest hello połączenia certyfikat o przyjaznej nazwie hello "DocumentDBEmulatorCertificate".</span><span class="sxs-lookup"><span data-stu-id="5f1b9-118">hello certificate you want tooexport is hello connection certificate with hello friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="5f1b9-119">Oba certyfikaty mogą zostać wygenerowane ponownie, klikając **Resetuj dane** w sposób przedstawiony poniżej z emulatora DB rozwiązania Cosmos Azure działa w hello na pasku zadań systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in hello Windows Tray.</span></span> <span data-ttu-id="5f1b9-120">Jeśli ponownie wygenerować certyfikaty hello i zainstalować je w magazynie certyfikatów hello Java lub używane w innych miejscach należy tooupdate ich, w przeciwnym razie aplikacja już połączyć toohello emulatora lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-120">If you regenerate hello certificates and have installed them into hello Java certificate store or used them elsewhere you will need tooupdate them, otherwise your application will no longer connect toohello local emulator.</span></span>

![Resetuj Azure DB rozwiązania Cosmos emulatora lokalne dane](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="5f1b9-122">Jak tooexport hello certyfikat SSL DB rozwiązania Cosmos Azure</span><span class="sxs-lookup"><span data-stu-id="5f1b9-122">How tooexport hello Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="5f1b9-123">Uruchom Menedżera certyfikatów systemu Windows hello, uruchamiając certlm.msc i przejdź toohello osobiste -> folderu certyfikatów i otwórz hello certyfikat o przyjaznej nazwie hello **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-123">Start hello Windows Certificate manager by running certlm.msc and navigate toohello Personal->Certificates folder and open hello certificate with hello friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Krok 1 eksportu Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="5f1b9-125">Polecenie **szczegóły** następnie **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-125">Click on **Details** then **OK**.</span></span>

    ![Krok 2 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="5f1b9-127">Kliknij przycisk **skopiuj tooFile...** .</span><span class="sxs-lookup"><span data-stu-id="5f1b9-127">Click **Copy tooFile...**.</span></span>

    ![Krok 3 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="5f1b9-129">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-129">Click **Next**.</span></span>

    ![Krok 4 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="5f1b9-131">Kliknij przycisk **nie eksportuj klucza prywatnego**, następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Krok 5 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="5f1b9-133">Polecenie **certyfikat x.509 szyfrowany algorytmem Base-64 (. CER)** , a następnie **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Krok 6 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="5f1b9-135">Nadaj nazwę hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-135">Give hello certificate a name.</span></span> <span data-ttu-id="5f1b9-136">W takim przypadku **documentdbemulatorcert** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Krok 7 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="5f1b9-138">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-138">Click **Finish**.</span></span>

    ![Krok 8 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a><span data-ttu-id="5f1b9-140">Jak toouse hello certyfikatu w języku Java</span><span class="sxs-lookup"><span data-stu-id="5f1b9-140">How toouse hello certificate in Java</span></span>

<span data-ttu-id="5f1b9-141">Podczas uruchamiania aplikacji Java lub aplikacji bazy danych MongoDB, które używają klienta Java hello jest łatwiejsze certyfikat hello tooinstall do magazynu certyfikatów domyślnego języka Java hello niż hello przekazywanie "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" flag.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-141">When running Java applications or MongoDB applications that use hello Java client it is easier tooinstall hello certificate into hello Java default certificate store than passing hello "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="5f1b9-142">Na przykład hello uwzględnione [aplikacji Java pokaz](https://localhost:8081/_explorer/index.html) zależy od hello domyślnym magazynie certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-142">For example hello included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on hello default certificate store.</span></span>

<span data-ttu-id="5f1b9-143">Postępuj zgodnie z instrukcjami hello hello [Dodawanie toohello certyfikatów, w magazynie certyfikatów urzędu certyfikacji Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certyfikatu do magazynu certyfikatów systemu hello domyślnego języka Java.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-143">Follow hello instructions in hello [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificate into hello default Java certificate store.</span></span> <span data-ttu-id="5f1b9-144">Zwróć Pamiętaj można pracować w katalogu % JAVA_HOME % hello podczas uruchamiania keytool.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-144">Keep in mind you will be working in hello %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="5f1b9-145">Raz Witaj "CosmosDBEmulatorCertificate" SSL jest instalowany certyfikat aplikacji powinny być możliwe tooconnect i użyj hello lokalnym emulatorze DB rozwiązania Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-145">Once hello "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able tooconnect and use hello local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="5f1b9-146">Jeśli będziesz kontynuować toohave problem może być toofollow hello [debugowania połączeń SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) artykułu.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-146">If you continue toohave trouble you may want toofollow hello [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="5f1b9-147">Jest bardzo prawdopodobne hello certyfikat nie jest zainstalowany w magazynie %JAVA_HOME%/jre/lib/security/cacerts hello.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-147">It is very likely hello certificate is not installed into hello %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="5f1b9-148">Na przykład, jeśli masz wiele zainstalowanych wersji programu Java aplikacji może używać magazynu cacerts innego niż hello jedną zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than hello one you updated.</span></span>

## <a name="how-toouse-hello-certificate-in-python"></a><span data-ttu-id="5f1b9-149">Jak toouse hello certyfikatu w języku Python</span><span class="sxs-lookup"><span data-stu-id="5f1b9-149">How toouse hello certificate in Python</span></span>

<span data-ttu-id="5f1b9-150">Przez domyślny hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) hello interfejsu API usługi DocumentDB zostanie nie próbuj i używać certyfikatu SSL hello podczas łączenia z lokalnym emulatorze toohello.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-150">By default hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="5f1b9-151">Jeśli jednak chcesz toouse SSL weryfikacji można wykonać przykłady hello w hello [Python gniazda otoki](https://docs.python.org/2/library/ssl.html) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-151">If however you want toouse SSL validation you can follow hello examples in hello [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-toouse-hello-certificate-in-nodejs"></a><span data-ttu-id="5f1b9-152">Jak toouse hello certyfikat w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="5f1b9-152">How toouse hello certificate in Node.js</span></span>

<span data-ttu-id="5f1b9-153">Przez domyślny hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) hello interfejsu API usługi DocumentDB zostanie nie próbuj i używać certyfikatu SSL hello podczas łączenia z lokalnym emulatorze toohello.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-153">By default hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="5f1b9-154">Jeśli jednak chcesz toouse SSL weryfikacji można wykonać przykłady hello w hello [dokumentacji Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="5f1b9-154">If however you want toouse SSL validation you can follow hello examples in hello [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f1b9-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f1b9-155">Next steps</span></span>

<span data-ttu-id="5f1b9-156">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5f1b9-156">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5f1b9-157">Obrócony certyfikatów</span><span class="sxs-lookup"><span data-stu-id="5f1b9-157">Rotated certificates</span></span>
> * <span data-ttu-id="5f1b9-158">Witaj wyeksportowany certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="5f1b9-158">Exported hello SSL certificate</span></span>
> * <span data-ttu-id="5f1b9-159">Przedstawiono sposób toouse hello certyfikatu w języku Java, Python i Node.js</span><span class="sxs-lookup"><span data-stu-id="5f1b9-159">Learned how toouse hello certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="5f1b9-160">Można teraz kontynuować toohello pojęcia sekcji, aby uzyskać więcej informacji na temat rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5f1b9-160">You can now proceed toohello Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5f1b9-161">Dystrybucja globalna</span><span class="sxs-lookup"><span data-stu-id="5f1b9-161">Global distribution</span></span>](distribute-data-globally.md) 
