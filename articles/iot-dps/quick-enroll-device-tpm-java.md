---
title: "Rejestrowanie urządzenia TPM w usłudze Azure Device Provisioning przy użyciu usługi Java | Microsoft Docs"
description: "Przewodnik Szybki start platformy Azure — rejestrowanie urządzenia TPM w usłudze Azure IoT Hub Device Provisioning przy użyciu zestawu SDK usługi Java"
services: iot-dps
keywords: 
author: dsk-2015
ms.author: dkshir
ms.date: 12/20/2017
ms.topic: hero-article
ms.service: iot-dps
documentationcenter: 
manager: timlt
ms.devlang: na
ms.custom: mvc
ms.openlocfilehash: f57b5304b8dc575d157f970312e71463496bf10d
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/22/2017
---
# <a name="enroll-tpm-device-to-iot-hub-device-provisioning-service-using-java-service-sdk"></a>Rejestrowanie urządzenia TPM w usłudze IoT Hub Device Provisioning przy użyciu zestawu SDK usługi Java
> [!div class="op_single_selector"]
> * [Java](quick-enroll-device-tpm-java.md)
> * [Node.js](quick-enroll-device-tpm-node.md)

Znajdują się tu instrukcje programowego rejestrowania symulowanego urządzenia TPM w usługach Azure IoT Hub Device Provisioning przy użyciu [zestawu SDK usługi Java](https://azure.github.io/azure-iot-sdk-java/service/) za pomocą przykładowej aplikacji Java. Mimo że zestaw SDK usługi Java działa zarówno na komputerach z systemami Windows, jak i Linux, w tym artykule w celu zaprezentowania procesu rejestracji użyto komputera deweloperskiego z systemem Windows.

Pamiętaj, aby przed kontynuowaniem [skonfigurować usługę IoT Hub Device Provisioning za pomocą witryny Azure Portal](./quick-setup-auto-provision.md) oraz przeprowadzić [symulowanie urządzenia TPM](quick-create-simulated-device.md#simulatetpm).

<a id="setupdevbox"></a>

## <a name="prepare-the-development-environment"></a>Przygotowywanie środowiska deweloperskiego 

1. Upewnij się, że na maszynie zainstalowano środowisko [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). 

2. Skonfiguruj zmienne środowiskowe instalacji języka Java. Zmienna `PATH` powinna zawierać pełną ścieżkę do katalogu *jdk1.8.x\bin*. Jeśli jest to pierwsza instalacja języka Java na komputerze, utwórz nową zmienną środowiskową o nazwie `JAVA_HOME` i ustaw ją na pełną ścieżkę do katalogu *jdk1.8.x*. Na komputerze z systemem Windows ten katalog znajduje się zwykle w folderze *C:\\Program Files\\Java\\*, a zmienne środowiskowe można tworzyć lub edytować po wyszukaniu frazy **Edytuj zmienne środowiskowe systemu** w **Panelu sterowania** komputera z systemem Windows. 

  Aby sprawdzić poprawność skonfigurowania języka Java na komputerze, możesz uruchomić następujące polecenie w oknie polecenia:

    ```cmd\sh
    java -version
    ```

3. Pobierz pakiet [Maven 3](https://maven.apache.org/download.cgi) i wyodrębnij go na swoim komputerze. 

4. Zmodyfikuj zmienną środowiskową `PATH`, aby wskazywała na folder *apache-maven-3.x.x\\bin* znajdujący się w folderze, do którego wyodrębniono pakiet Maven. Poprawność zainstalowania pakietu Maven można potwierdzić, uruchamiając to polecenie w oknie polecenia:

    ```cmd\sh
    mvn --version
    ```

5. Upewnij się, że na swojej maszynie masz zainstalowane oprogramowanie [git](https://git-scm.com/download/) i że jest ono dodane do zmiennej środowiskowej `PATH`. 


<a id="javasample"></a>

## <a name="download-and-modify-the-java-sample-code"></a>Pobieranie i modyfikowanie przykładowego kodu Java

W tej sekcji przedstawiono sposób dodawania szczegółów aprowizacji urządzenia TPM do przykładowego kodu. 

1. Otwórz wiersz polecenia. Sklonuj repozytorium GitHub na potrzeby przykładowego kodu rejestracji urządzenia przy użyciu zestawu SDK usługi Java:
    
    ```cmd\sh
    git clone https://github.com/Azure/azure-iot-sdk-java.git --recursive
    ```

2. W pobranym kodzie źródłowym przejdź do folderu przykładu **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-sample_**. Otwórz plik **_/src/main/java/samples/com/microsoft/azure/sdk/iot/ServiceEnrollmentSample.java_** w dowolnym edytorze i dodaj następujące szczegółowe informacje:

    1. Dodaj ciąg `[Provisioning Connection String]` dla usługi aprowizacji z portalu, jako pokazano poniżej:
        1. Przejdź do usługi aprowizacji w witrynie [Azure Portal](https://portal.azure.com). 
        2. Otwórz **Zasady dostępu współużytkowanego** i wybierz zasadę, która ma uprawnienie *EnrollmentWrite*.
        3. Skopiuj **Parametry połączenia klucza podstawowego**. 

            ![Pobieranie parametrów połączenia aprowizacji z portalu](./media/quick-enroll-device-tpm-java/provisioning-string.png)  

        4. W przykładowym pliku kodu **_ServiceEnrollmentSample.java_** zastąp ciąg `[Provisioning Connection String]` **parametrami połączenia klucza podstawowego**.
    
            ```Java
            private static final String PROVISIONING_CONNECTION_STRING = "[Provisioning Connection String]";
            ```

    2. Dodaj szczegóły urządzenia TPM:
        1. Pobierz *identyfikator rejestracji* i *klucz poręczenia modułu TPM* na potrzeby symulacji urządzenia TPM, wykonując kroki prowadzące do sekcji [Symulowanie urządzenia TPM](quick-create-simulated-device.md#simulatetpm).
        2. Użyj **_identyfikatora rejestracji_** i **_klucza poręczenia_** z danych wyjściowych poprzedniego kroku, aby zastąpić ciągi `[RegistrationId]` i `[TPM Endorsement Key]` w przykładowym pliku kodu **_ServiceEnrollmentSample.java_**:
        
            ```Java
            private static final String REGISTRATION_ID = "[RegistrationId]";
            private static final String TPM_ENDORSEMENT_KEY = "[TPM Endorsement Key]";
            ```

    3. Opcjonalnie możesz skonfigurować usługę aprowizacji za pośrednictwem przykładowego kodu:
        - Aby dodać tę konfigurację do przykładu, wykonaj następujące kroki:
            1. Przejdź do centrum IoT połączonego z usługą aprowizacji w witrynie [Azure Portal](https://portal.azure.com). Otwórz kartę **Przegląd** centrum i skopiuj wartość pola **Nazwa hosta**. Przypisz tę **nazwę hosta** do parametru *IOTHUB_HOST_NAME*.
                ```Java
                private static final String IOTHUB_HOST_NAME = "[Host name].azure-devices.net";
                ```
            2. Przypisz przyjazną nazwę do parametru *DEVICE_ID* i zachowaj dla parametru *PROVISIONING_STATUS* wartość domyślną *ENABLED*. 
    
        - LUB, jeśli nie chcesz konfigurować usługi aprowizacji, oznacz jako komentarze bądź usuń następujące instrukcje w pliku _ServiceEnrollmentSample.java_:
            ```Java
            // The following parameters are optional. Remove it if you don't need.
            individualEnrollment.setDeviceId(DEVICE_ID);
            individualEnrollment.setIotHubHostName(IOTHUB_HOST_NAME);
            individualEnrollment.setProvisioningStatus(PROVISIONING_STATUS);
            ```

    4. Przejrzyj przykładowy kod. Tworzy on, aktualizuje i usuwa rejestrację indywidualną urządzenia TPM oraz tworzy do niej zapytanie. Aby sprawdzić poprawność rejestracji w portalu, tymczasowo oznacz jako komentarz następujące wiersze kodu na końcu pliku _ServiceEnrollmentSample.java_:
    
        ```Java
        // *********************************** Delete info of individualEnrollment ************************************
        System.out.println("\nDelete the individualEnrollment...");
        provisioningServiceClient.deleteIndividualEnrollment(REGISTRATION_ID);
        ```

    5. Zapisz plik _ServiceEnrollmentSample.java_.

<a id="runjavasample"></a>

## <a name="build-and-run-the-java-sample-code"></a>Kompilowanie i uruchamianie przykładowego kodu Java

1. Otwórz okno polecenia i przejdź do folderu **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-sample_**.

2. Skompiluj przykładowy kod za pomocą tego polecenia:

    ```cmd\sh
    mvn install -DskipTests
    ```

   To polecenie pobiera pakiet Maven [`com.microsoft.azure.sdk.iot.provisioning.service`](https://www.mvnrepository.com/artifact/com.microsoft.azure.sdk.iot.provisioning/provisioning-service-client) na komputer. Ten pakiet zawiera pliki binarne zestawu SDK usługi Java wymagane przez przykładowy kod na potrzeby kompilacji. 

3. Uruchom przykładowy kod przy użyciu tych poleceń w oknie polecenia:

    ```cmd\sh
    cd target
    java -jar ./service-enrollment-sample-{version}-with-deps.jar
    ```

4. Sprawdź poprawność rejestracji w oknie danych wyjściowych. 

5. Przejdź do usługi aprowizacji w witrynie Azure Portal. Kliknij pozycję **Zarządzanie rejestracjami** i wybierz kartę **Rejestracje indywidualne**. Zwróć uwagę, że na liście znajduje się teraz *Identyfikator rejestracji* symulowanego urządzenia TPM. 

    ![Potwierdzanie poprawności rejestracji urządzenia TPM w portalu](./media/quick-enroll-device-tpm-java/verify-tpm-enrollment.png)  

## <a name="clean-up-resources"></a>Oczyszczanie zasobów
Jeśli planujesz eksplorować przykładową usługę Java, nie usuwaj zasobów utworzonych w tym przewodniku Szybki start. Jeśli nie planujesz kontynuować pracy, wykonaj poniższe kroki, aby usunąć wszystkie zasoby utworzone w ramach tego przewodnika Szybki start.

1. Zamknij okno danych wyjściowych przykładowej usługi Java na swojej maszynie.
1. Zamknij okno symulatora modułu TPM, które mogło zostać utworzone do symulacji urządzenia TPM.
1. Przejdź do usługi Device Provisioning w witrynie Azure Portal, kliknij pozycję **Zarządzanie rejestracjami**, a następnie wybierz kartę **Rejestracje indywidualne**. Wybierz *Identyfikator rejestracji* urządzenia zarejestrowanego w ramach tego przewodnika Szybki start i kliknij przycisk **Usuń** u góry bloku. 

## <a name="next-steps"></a>Następne kroki
W tym przewodniku Szybki start zarejestrowano urządzenie TPM w usłudze Device Provisioning. Aby uzyskać dokładne informacje na temat aprowizowania urządzeń, przejdź do samouczka poświęconego konfiguracji usługi Device Provisioning Service w witrynie Azure portal. 

> [!div class="nextstepaction"]
> [Samouczki dla usługi Azure IoT Hub Device Provisioning Service](./tutorial-set-up-cloud.md)
