---
title: "Wyeksportowanie certyfikatów emulatora DB rozwiązania Cosmos Azure | Dokumentacja firmy Microsoft"
description: "Podczas tworzenia w językach i środowisk uruchomieniowych, który nie należy używać magazynu certyfikatów systemu Windows należy wyeksportować i zarządzanie certyfikatami SSL. Ten wpis zawiera instrukcje krok po kroku."
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
ms.openlocfilehash: 4add5028d50972316902cecd8c399781c012cb77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="export-the-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="c46b6-105">Wyeksportowanie certyfikatów emulatora DB rozwiązania Cosmos Azure do użycia z programem Java, Python i Node.js</span><span class="sxs-lookup"><span data-stu-id="c46b6-105">Export the Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="c46b6-106">**Pobierz Emulator**</span><span class="sxs-lookup"><span data-stu-id="c46b6-106">**Download the Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="c46b6-107">Emulator DB rozwiązania Cosmos Azure zapewnia środowisko lokalne, które emuluje usługę Azure DB rozwiązania Cosmos do celów programistycznych, łącznie z jej użycie połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="c46b6-107">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="c46b6-108">Ten wpis pokazano, jak można wyeksportować certyfikaty SSL dla języków i środowisk uruchomieniowych, który nie jest integrowana z magazynu certyfikatów systemu Windows, takich jak Java, który używa własnego [magazyn certyfikatów](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) i języka Python, który używa [gniazda otoki](https://docs.python.org/2/library/ssl.html) i Node.js, który używa [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="c46b6-108">This post demonstrates how to export the SSL certificates for use in languages and runtimes that do not integrate with the Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="c46b6-109">Więcej o emulatora w [użyć emulatora DB rozwiązania Cosmos Azure do programowania i testowania](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="c46b6-109">You can read more about the emulator in [Use the Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="c46b6-110">Ten samouczek obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="c46b6-110">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c46b6-111">Obracanie certyfikatów</span><span class="sxs-lookup"><span data-stu-id="c46b6-111">Rotating certificates</span></span>
> * <span data-ttu-id="c46b6-112">Eksportowanie certyfikatu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="c46b6-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="c46b6-113">Poznanie certyfikatu w języku Java, Python i Node.js</span><span class="sxs-lookup"><span data-stu-id="c46b6-113">Learning how to use the certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="c46b6-114">Obracanie certyfikacji</span><span class="sxs-lookup"><span data-stu-id="c46b6-114">Certification rotation</span></span>

<span data-ttu-id="c46b6-115">Certyfikaty w lokalnym emulatorze DB rozwiązania Cosmos Azure są generowane podczas pierwszego uruchomienia emulator.</span><span class="sxs-lookup"><span data-stu-id="c46b6-115">Certificates in the Azure Cosmos DB Local Emulator are generated the first time the emulator is run.</span></span> <span data-ttu-id="c46b6-116">Istnieją dwa certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="c46b6-116">There are two certificates.</span></span> <span data-ttu-id="c46b6-117">Jeden używane do łączenia z lokalnym emulatorze i jeden do zarządzania kluczy tajnych w emulatorze.</span><span class="sxs-lookup"><span data-stu-id="c46b6-117">One used for connecting to the local emulator and one for managing secrets within the emulator.</span></span> <span data-ttu-id="c46b6-118">Certyfikat, który chcesz wyeksportować jest certyfikatu połączenia z przyjazną nazwą "DocumentDBEmulatorCertificate".</span><span class="sxs-lookup"><span data-stu-id="c46b6-118">The certificate you want to export is the connection certificate with the friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="c46b6-119">Oba certyfikaty mogą zostać wygenerowane ponownie, klikając **Resetuj dane** w sposób przedstawiony poniżej z emulatora DB rozwiązania Cosmos Azure działa w na pasku zadań systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c46b6-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in the Windows Tray.</span></span> <span data-ttu-id="c46b6-120">Ponowne generowanie certyfikatów i ich instalacji do magazynu certyfikatów Java lub używać ich w innym miejscu należy zaktualizować je, w przeciwnym razie aplikacji już nie będzie łączyć się emulatora lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c46b6-120">If you regenerate the certificates and have installed them into the Java certificate store or used them elsewhere you will need to update them, otherwise your application will no longer connect to the local emulator.</span></span>

![Resetuj Azure DB rozwiązania Cosmos emulatora lokalne dane](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-to-export-the-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="c46b6-122">Jak wyeksportować certyfikat protokołu SSL DB rozwiązania Cosmos Azure</span><span class="sxs-lookup"><span data-stu-id="c46b6-122">How to export the Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="c46b6-123">Uruchom Menedżera certyfikatów systemu Windows przez systemem certlm.msc i przejdź do folderu certyfikatów osobiste-> i otwórz certyfikat o przyjaznej nazwie **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="c46b6-123">Start the Windows Certificate manager by running certlm.msc and navigate to the Personal->Certificates folder and open the certificate with the friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Krok 1 eksportu Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="c46b6-125">Polecenie **szczegóły** następnie **OK**.</span><span class="sxs-lookup"><span data-stu-id="c46b6-125">Click on **Details** then **OK**.</span></span>

    ![Krok 2 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="c46b6-127">Kliknij przycisk **Kopiuj do pliku...** .</span><span class="sxs-lookup"><span data-stu-id="c46b6-127">Click **Copy to File...**.</span></span>

    ![Krok 3 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="c46b6-129">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="c46b6-129">Click **Next**.</span></span>

    ![Krok 4 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="c46b6-131">Kliknij przycisk **nie eksportuj klucza prywatnego**, następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c46b6-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Krok 5 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="c46b6-133">Polecenie **certyfikat x.509 szyfrowany algorytmem Base-64 (. CER)** , a następnie **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c46b6-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Krok 6 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="c46b6-135">Nadaj nazwę certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c46b6-135">Give the certificate a name.</span></span> <span data-ttu-id="c46b6-136">W takim przypadku **documentdbemulatorcert** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c46b6-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Krok 7 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="c46b6-138">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="c46b6-138">Click **Finish**.</span></span>

    ![Krok 8 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-to-use-the-certificate-in-java"></a><span data-ttu-id="c46b6-140">Sposób użycia certyfikatu w języku Java</span><span class="sxs-lookup"><span data-stu-id="c46b6-140">How to use the certificate in Java</span></span>

<span data-ttu-id="c46b6-141">Podczas uruchamiania aplikacji Java lub aplikacji bazy danych MongoDB, które używają klienta Java łatwiej Zainstaluj certyfikat w domyślnym magazynie certyfikatów Java niż przekazywanie "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword = "<password>" flag.</span><span class="sxs-lookup"><span data-stu-id="c46b6-141">When running Java applications or MongoDB applications that use the Java client it is easier to install the certificate into the Java default certificate store than passing the "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="c46b6-142">Na przykład dołączonej [aplikacji Java pokaz](https://localhost:8081/_explorer/index.html) zależy od domyślnym magazynie certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="c46b6-142">For example the included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on the default certificate store.</span></span>

<span data-ttu-id="c46b6-143">Postępuj zgodnie z instrukcjami [Dodawanie certyfikatu do magazynu certyfikatów urzędu certyfikacji Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) można zaimportować certyfikatu X.509 w domyślnym magazynie certyfikatów Java.</span><span class="sxs-lookup"><span data-stu-id="c46b6-143">Follow the instructions in the [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) to import the X.509 certificate into the default Java certificate store.</span></span> <span data-ttu-id="c46b6-144">Zwróć Pamiętaj można pracować w katalogu % JAVA_HOME % podczas uruchamiania keytool.</span><span class="sxs-lookup"><span data-stu-id="c46b6-144">Keep in mind you will be working in the %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="c46b6-145">Po "CosmosDBEmulatorCertificate" SSL jest instalowany certyfikat aplikacji powinno być możliwe do nawiązywania połączeń i użyć lokalnego emulatora DB rozwiązania Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="c46b6-145">Once the "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able to connect and use the local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="c46b6-146">Jeśli nadal występują problemy można wykonać [debugowania połączeń SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c46b6-146">If you continue to have trouble you may want to follow the [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="c46b6-147">Jest bardzo prawdopodobne, certyfikat nie został zainstalowany w magazynie %JAVA_HOME%/jre/lib/security/cacerts.</span><span class="sxs-lookup"><span data-stu-id="c46b6-147">It is very likely the certificate is not installed into the %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="c46b6-148">Na przykład, jeśli masz wiele zainstalowanych wersji programu Java aplikacji może używać magazynu cacerts innego niż zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="c46b6-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than the one you updated.</span></span>

## <a name="how-to-use-the-certificate-in-python"></a><span data-ttu-id="c46b6-149">Sposób użycia certyfikatu w języku Python</span><span class="sxs-lookup"><span data-stu-id="c46b6-149">How to use the certificate in Python</span></span>

<span data-ttu-id="c46b6-150">Domyślnie [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) interfejsu API usługi DocumentDB nie będą spróbuj i użyć certyfikatu SSL, podczas nawiązywania połączenia z lokalnym emulatora.</span><span class="sxs-lookup"><span data-stu-id="c46b6-150">By default the [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for the DocumentDB API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="c46b6-151">Jeśli jednak chcesz używać protokołu SSL weryfikacji można wykonać w przykładach w [Python gniazda otoki](https://docs.python.org/2/library/ssl.html) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="c46b6-151">If however you want to use SSL validation you can follow the examples in the [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-to-use-the-certificate-in-nodejs"></a><span data-ttu-id="c46b6-152">Sposób użycia certyfikatu w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="c46b6-152">How to use the certificate in Node.js</span></span>

<span data-ttu-id="c46b6-153">Domyślnie [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) interfejsu API usługi DocumentDB nie będą spróbuj i użyć certyfikatu SSL, podczas nawiązywania połączenia z lokalnym emulatora.</span><span class="sxs-lookup"><span data-stu-id="c46b6-153">By default the [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for the DocumentDB API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="c46b6-154">Jeśli jednak chcesz używać protokołu SSL weryfikacji można wykonać w przykładach w [dokumentacji Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="c46b6-154">If however you want to use SSL validation you can follow the examples in the [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c46b6-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c46b6-155">Next steps</span></span>

<span data-ttu-id="c46b6-156">W tym samouczku wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="c46b6-156">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c46b6-157">Obrócony certyfikatów</span><span class="sxs-lookup"><span data-stu-id="c46b6-157">Rotated certificates</span></span>
> * <span data-ttu-id="c46b6-158">Wyeksportowany certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="c46b6-158">Exported the SSL certificate</span></span>
> * <span data-ttu-id="c46b6-159">Przedstawiono sposób używania certyfikatu w języku Java, Python i Node.js</span><span class="sxs-lookup"><span data-stu-id="c46b6-159">Learned how to use the certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="c46b6-160">Możesz teraz przejść do sekcji pojęcia, aby uzyskać więcej informacji na temat rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c46b6-160">You can now proceed to the Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c46b6-161">Dystrybucja globalna</span><span class="sxs-lookup"><span data-stu-id="c46b6-161">Global distribution</span></span>](distribute-data-globally.md) 
