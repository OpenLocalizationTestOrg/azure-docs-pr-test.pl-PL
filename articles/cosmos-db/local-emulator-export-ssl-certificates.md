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
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>Eksportuj hello Azure rozwiązania Cosmos DB emulatora certyfikatów do użytku z języka Java, Python i Node.js

[**Pobierz hello emulatora**](https://aka.ms/cosmosdb-emulator)

Hello Azure rozwiązania Cosmos DB emulatora zapewnia środowisko lokalne, które emuluje hello Azure DB rozwiązania Cosmos usługi do celów programistycznych, łącznie z jej użycie połączenia SSL. Ten wpis pokazano, jak tooexport hello SSL certyfikatów do użytku w językach i środowisk uruchomieniowych, który nie jest integrowana z magazynu certyfikatów systemu Windows, takich jak Java, który używa własnego hello [magazyn certyfikatów](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) i języka Python, który używa [gniazda otoki](https://docs.python.org/2/library/ssl.html) i Node.js, który używa [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback). Więcej o emulator hello w [Użyj hello Azure rozwiązania Cosmos DB emulatora do projektowania i testowania](./local-emulator.md).

Ten samouczek obejmuje hello następujące zadania:

> [!div class="checklist"]
> * Obracanie certyfikatów
> * Eksportowanie certyfikatu protokołu SSL
> * Learning, jak toouse hello certyfikatu w języku Java, Python i Node.js

## <a name="certification-rotation"></a>Obracanie certyfikacji

Certyfikaty hello emulatora lokalnej bazy danych usługi Azure rozwiązania Cosmos są generowane hello emulatora hello jest uruchamiany po raz pierwszy. Istnieją dwa certyfikaty. Jeden służące do połączenia z lokalnym emulatorze toohello i jeden do zarządzania kluczy tajnych w emulatorze hello. Hello certyfikatów, które chcesz tooexport jest hello połączenia certyfikat o przyjaznej nazwie hello "DocumentDBEmulatorCertificate".

Oba certyfikaty mogą zostać wygenerowane ponownie, klikając **Resetuj dane** w sposób przedstawiony poniżej z emulatora DB rozwiązania Cosmos Azure działa w hello na pasku zadań systemu Windows. Jeśli ponownie wygenerować certyfikaty hello i zainstalować je w magazynie certyfikatów hello Java lub używane w innych miejscach należy tooupdate ich, w przeciwnym razie aplikacja już połączyć toohello emulatora lokalnego.

![Resetuj Azure DB rozwiązania Cosmos emulatora lokalne dane](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a>Jak tooexport hello certyfikat SSL DB rozwiązania Cosmos Azure

1. Uruchom Menedżera certyfikatów systemu Windows hello, uruchamiając certlm.msc i przejdź toohello osobiste -> folderu certyfikatów i otwórz hello certyfikat o przyjaznej nazwie hello **DocumentDbEmulatorCertificate**.

    ![Krok 1 eksportu Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. Polecenie **szczegóły** następnie **OK**.

    ![Krok 2 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. Kliknij przycisk **skopiuj tooFile...** .

    ![Krok 3 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. Kliknij przycisk **Dalej**.

    ![Krok 4 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. Kliknij przycisk **nie eksportuj klucza prywatnego**, następnie kliknij przycisk **dalej**.

    ![Krok 5 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. Polecenie **certyfikat x.509 szyfrowany algorytmem Base-64 (. CER)** , a następnie **dalej**.

    ![Krok 6 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. Nadaj nazwę hello certyfikatu. W takim przypadku **documentdbemulatorcert** , a następnie kliknij przycisk **dalej**.

    ![Krok 7 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. Kliknij przycisk **Zakończ**.

    ![Krok 8 wyeksportować Azure emulator lokalnej bazy danych rozwiązania Cosmos](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a>Jak toouse hello certyfikatu w języku Java

Podczas uruchamiania aplikacji Java lub aplikacji bazy danych MongoDB, które używają klienta Java hello jest łatwiejsze certyfikat hello tooinstall do magazynu certyfikatów domyślnego języka Java hello niż hello przekazywanie "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" flag. Na przykład hello uwzględnione [aplikacji Java pokaz](https://localhost:8081/_explorer/index.html) zależy od hello domyślnym magazynie certyfikatów.

Postępuj zgodnie z instrukcjami hello hello [Dodawanie toohello certyfikatów, w magazynie certyfikatów urzędu certyfikacji Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certyfikatu do magazynu certyfikatów systemu hello domyślnego języka Java. Zwróć Pamiętaj można pracować w katalogu % JAVA_HOME % hello podczas uruchamiania keytool.

Raz Witaj "CosmosDBEmulatorCertificate" SSL jest instalowany certyfikat aplikacji powinny być możliwe tooconnect i użyj hello lokalnym emulatorze DB rozwiązania Cosmos Azure. Jeśli będziesz kontynuować toohave problem może być toofollow hello [debugowania połączeń SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) artykułu. Jest bardzo prawdopodobne hello certyfikat nie jest zainstalowany w magazynie %JAVA_HOME%/jre/lib/security/cacerts hello. Na przykład, jeśli masz wiele zainstalowanych wersji programu Java aplikacji może używać magazynu cacerts innego niż hello jedną zaktualizowane.

## <a name="how-toouse-hello-certificate-in-python"></a>Jak toouse hello certyfikatu w języku Python

Przez domyślny hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) hello interfejsu API usługi DocumentDB zostanie nie próbuj i używać certyfikatu SSL hello podczas łączenia z lokalnym emulatorze toohello. Jeśli jednak chcesz toouse SSL weryfikacji można wykonać przykłady hello w hello [Python gniazda otoki](https://docs.python.org/2/library/ssl.html) dokumentacji.

## <a name="how-toouse-hello-certificate-in-nodejs"></a>Jak toouse hello certyfikat w środowisku Node.js

Przez domyślny hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) hello interfejsu API usługi DocumentDB zostanie nie próbuj i używać certyfikatu SSL hello podczas łączenia z lokalnym emulatorze toohello. Jeśli jednak chcesz toouse SSL weryfikacji można wykonać przykłady hello w hello [dokumentacji Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Obrócony certyfikatów
> * Witaj wyeksportowany certyfikat SSL
> * Przedstawiono sposób toouse hello certyfikatu w języku Java, Python i Node.js

Można teraz kontynuować toohello pojęcia sekcji, aby uzyskać więcej informacji na temat rozwiązania Cosmos bazy danych.

> [!div class="nextstepaction"]
> [Dystrybucja globalna](distribute-data-globally.md) 
