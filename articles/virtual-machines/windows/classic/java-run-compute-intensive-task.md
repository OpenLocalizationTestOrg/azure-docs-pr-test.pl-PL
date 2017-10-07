---
title: intensywnie aaaCompute aplikacji Java na maszynie Wirtualnej | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate maszyny wirtualnej platformy Azure, uruchomionym aplikacji Java obliczeniowych, które mogą być monitorowane przez inną aplikację Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a>Jak zadanie toorun obliczeniowych w języku Java na maszynie wirtualnej
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

Przy użyciu platformy Azure możesz użyć zadań obliczeniowych toohandle maszyny wirtualnej. Na przykład maszynę wirtualną można realizacji zadań i dostarczać wyniki tooclient maszyny lub aplikacji dla urządzeń przenośnych. Po przeczytaniu tego artykułu, trzeba będzie zrozumienia sposobu toocreate maszynę wirtualną działającą aplikację Java obliczeniowych mogą być monitorowane przez inną aplikację Java.

W tym samouczku założono, że wiesz, jak toocreate Java aplikacji konsoli, można zaimportować aplikacji Java tooyour bibliotek i może powodować generowanie archiwum Java (JAR). Przyjęto, że nie wie, Microsoft Azure.

Dowiesz się:

* Jak toocreate maszynę wirtualną z Java Development Kit (JDK) już zainstalowana.
* Jak tooremotely zalogować tooyour maszyny wirtualnej.
* Jak toocreate usługi magistrali przestrzeni nazw.
* Jak toocreate aplikacji Java, która wykonuje zadanie obliczeniowych.
* Jak toocreate aplikacji Java, która monitoruje hello postęp zadania obliczeniowych hello.
* Jak toorun hello aplikacji Java.
* Jak toostop hello aplikacji Java.

W tym samouczku będzie używać hello Problem sprzedawcy Traveling hello obliczeniowych zadań. Witaj poniżej znajduje się przykład hello Java aplikacji uruchomionej hello obliczeniowych zadania.

![Solver sprzedawcy Traveling Problem][solver_output]

Witaj poniżej znajduje się przykład hello zadanie obliczeniowych hello monitorowania aplikacji Java.

![Problem sprzedawcy Traveling klienta][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate maszyny wirtualnej
1. Zaloguj się za toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Kliknij przycisk **nowy**, kliknij przycisk **obliczeniowe**, kliknij przycisk **maszyny wirtualnej**, a następnie kliknij przycisk **z galerii**.
3. W hello **wybierz obraz maszyny wirtualnej** okno dialogowe, wybierz opcję **JDK 7 systemu Windows Server 2012**.
   Należy pamiętać, że **JDK 6 systemu Windows Server 2012** jest dostępna w przypadku, gdy masz starsze aplikacje, które nie są jeszcze gotowy toorun w JDK 7.
4. Kliknij przycisk **Dalej**.
5. W hello **konfiguracji maszyny wirtualnej** okno dialogowe:
   1. Określ nazwę hello maszyny wirtualnej.
   2. Określ toouse rozmiar hello hello maszyny wirtualnej.
   3. Wprowadź nazwę administratora hello w hello **nazwy użytkownika** pola. Zapamiętaj to hasło nazwy i hello wprowadzanymi przez użytkownika będzie dalej, użyjesz ich podczas zdalnego logowania toohello maszyny wirtualnej.
   4. Wprowadź hasło w hello **nowe hasło** pól i wprowadź go ponownie w hello **Potwierdź** pola. Jest to hasło konta administratora hello.
   5. Kliknij przycisk **Dalej**.
6. W hello dalej **konfiguracji maszyny wirtualnej** okno dialogowe:
   1. Dla **usługi w chmurze**, użyj domyślnej hello **Utwórz nową usługę w chmurze**.
   2. Witaj wartość **nazwa DNS usługi w chmurze** musi być unikatowa w cloudapp.net. W razie potrzeby zmodyfikuj tę wartość, tym Azure oznacza jest unikatowa.
   3. Określ region, grupę koligacji lub sieci wirtualnej. Do celów tego samouczka, określ region, takich jak **zachodnie stany USA**.
   4. Dla **konta magazynu**, wybierz pozycję **użyć konta magazynu automatycznie generowanych**.
   5. Aby uzyskać **zestawu dostępności**, wybierz pozycję **(Brak)**.
   6. Kliknij przycisk **Dalej**.
7. W ostatnim hello **konfiguracji maszyny wirtualnej** okno dialogowe:
   1. Zaakceptuj hello domyślnych wpisów punktu końcowego.
   2. Kliknij przycisk **Complete** (Zakończ).

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a>Dziennik tooremotely w tooyour maszyny wirtualnej
1. Zaloguj się na toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Kliknij przycisk **maszyn wirtualnych**.
3. Kliknij nazwę hello hello maszyny wirtualnej, który chcesz toolog w.
4. Kliknij przycisk **Połącz**.
5. Odpowiedz monity toohello jako maszyna wirtualna toohello tooconnect potrzebne. Po wyświetleniu monitu dla hello nazwę i hasło administratora, należy użyć wartości hello, podanych podczas tworzenia maszyny wirtualnej hello.

Uwaga tej funkcji usługi Azure Service Bus hello wymaga toobe certyfikat główny firmy CyberTrust Baltimore hello zainstalowane w ramach Twojego środowiska JRE **cacerts** przechowywania. Ten certyfikat jest automatycznie uwzględnione w hello Java Runtime Environment (JRE) używane w tym samouczku. Jeśli nie masz ten certyfikat w Twojej środowiska JRE **cacerts** przechowywania, zobacz [Dodawanie toohello certyfikatu z magazynu certyfikatów urzędu certyfikacji Java] [ add_ca_cert] informacji na temat dodawania go (a także informacje o wyświetlaniu hello certyfikaty w magazynie cacerts).

## <a name="how-toocreate-a-service-bus-namespace"></a>Jak toocreate usługi magistrali przestrzeni nazw
kolejkuje toobegin przy użyciu usługi Service Bus na platformie Azure, musisz najpierw utworzyć przestrzeń nazw usługi. Przestrzeń nazw usługi zapewnia kontener zakresu na potrzeby adresowania zasobów usługi Service Bus w aplikacji.

toocreate przestrzeni nazw usługi:

1. Zaloguj się na toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. W okienku nawigacji w lewym dolnym hello hello klasycznego portalu Azure, kliknij przycisk **usługi Service Bus, kontroli dostępu i buforowanie**.
3. W okienku lewej górnej hello hello klasycznego portalu Azure, kliknij przycisk hello **usługi Service Bus** węzeł, a następnie kliknij przycisk hello **nowy** przycisku.  
   ![Zrzut ekranu węzeł magistrali usług][svc_bus_node]
4. W hello **tworzenie nowych Namespace usługi** okna dialogowego wprowadź **Namespace**, a następnie kliknij przycisk toomake się, że jest unikatowa, **Sprawdź dostępność** przycisku.  
   ![Utwórz nowy Namespace zrzut ekranu][create_namespace]
5. Po upewnieniu się, hello przestrzeni nazw jest dostępna, wybierz kraj lub region, w którym ma być hostowana przestrzeni nazw, a następnie kliknij hello **utworzyć Namespace** przycisku.  
   
   utworzona przestrzeń nazw Hello pojawi się w hello klasycznego portalu Azure i przejście tooactivate chwilę. Poczekaj, aż stan hello jest **Active** przed kontynuowaniem hello następnego kroku.

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a>Uzyskiwanie hello domyślnych poświadczeń zarządzania dla przestrzeni nazw hello
W operacji zarządzania tooperform kolejności, takich jak tworzenie kolejki w nowej przestrzeni nazw hello należy tooobtain hello zarządzania poświadczenia dla przestrzeni nazw.

1. W okienku nawigacji po lewej stronie powitania kliknij hello **usługi Service Bus** węzeł, aby wyświetlić hello listę dostępnych przestrzeni nazw.
   ![Dostępne obszary nazw zrzut ekranu][avail_namespaces]
2. Wybierz obszar nazw hello, nowo utworzoną z wyświetlonej listy hello.
   ![Zrzut ekranu listy Namespace][namespace_list]
3. po prawej stronie powitania **właściwości** okienko zawiera listę właściwości hello nowej przestrzeni nazw.
   ![Zrzut ekranu okienka właściwości][properties_pane]
4. Witaj **domyślny klucz** jest ukryty. Kliknij przycisk hello **widoku** przycisk poświadczenia zabezpieczeń hello toodisplay.
   ![Zrzut ekranu klucz domyślny][default_key]
5. Zanotuj hello **domyślne wystawcy** i hello **domyślny klucz** jako użyje tych informacji poniżej tooperform operacje z przestrzenią nazw.

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a>Jak toocreate aplikacji Java, która wykonuje zadanie obliczeniowych
1. Na komputerze deweloperskim (który nie ma maszyny wirtualnej na powitania toobe utworzony), Pobierz hello [zestawu Azure SDK dla języka Java](https://azure.microsoft.com/develop/java/).
2. Utwórz aplikację konsoli języka Java przy użyciu hello przykładowy kod na końcu hello w tej sekcji. W tym samouczku użyjemy **TSPSolver.java** jako nazwa pliku hello Java. Modyfikowanie hello **Twojego\_usługi\_magistrali\_przestrzeni nazw**, **Twojego\_usługi\_magistrali\_właściciela**i **Twojego\_usługi\_magistrali\_klucza** toouse symbole zastępcze z usługi service bus **przestrzeni nazw**, **domyślne wystawcy** i  **Domyślny klucz** wartości odpowiednio.
3. Po kodowania, eksportu hello aplikacji tooa do uruchomienia Java archiwum (JAR) i hello pakietu wymaganych bibliotek na powitania wygenerowany JAR. W tym samouczku użyjemy **TSPSolver.jar** jako nazwa JAR hello wygenerowany.

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a>Jak toocreate aplikacji Java, która monitoruje hello postęp zadania obliczeniowych hello
1. Na komputerze deweloperskim Utwórz aplikację konsoli języka Java przy użyciu hello przykładowy kod na końcu hello w tej sekcji. W tym samouczku użyjemy **TSPClient.java** jako nazwa pliku hello Java. Jak pokazano wcześniej, zmodyfikuj hello **Twojego\_usługi\_magistrali\_przestrzeni nazw**, **Twojego\_usługi\_magistrali\_właściciela**, i **Twojego\_usługi\_magistrali\_klucza** toouse symbole zastępcze z usługi service bus **przestrzeni nazw**, **domyślne wystawcy**i **domyślny klucz** wartości odpowiednio.
2. Eksportuj tooa aplikacji hello JAR do uruchomienia i pakietów hello wymaganych bibliotek na powitania wygenerowany JAR. W tym samouczku użyjemy **TSPClient.jar** jako nazwa JAR hello wygenerowany.

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a>Jak toorun hello aplikacji Java
Uruchamianie aplikacji obliczeniowych hello, pierwszy toocreate hello kolejki, a następnie toosolve hello podróży Saleseman Problem, który doda hello bieżącego najlepszą trasę toohello kolejką usługi service bus. Podczas hello obliczeniowych aplikacja jest uruchomiona (lub później), wykonywania powitania klienta toodisplay wyników z kolejką usługi service bus hello.

### <a name="toorun-hello-compute-intensive-application"></a>toorun hello obliczeniowych aplikacji
1. Zaloguj się na tooyour maszyny wirtualnej.
2. Utwórz folder, w którym będzie działała aplikacja sieci. Na przykład **c:\TSP**.
3. Kopiuj **TSPSolver.jar** za**c:\TSP**,
4. Utwórz plik o nazwie **c:\TSP\cities.txt** z powitania po zawartości.
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. W wierszu polecenia Zmień tooc:\TSP katalogów.
6. Upewnij się, że folder bin hello JRE znajduje się w zmiennej środowiskowej PATH hello.
7. Musisz kolejką usługi service bus toocreate hello przed rozpoczęciem powitalne TSP solver permutacji. Witaj uruchom następujące polecenie kolejką usługi service bus toocreate hello.
   
        java -jar TSPSolver.jar createqueue
8. Teraz, gdy hello Trwa tworzenie kolejki, możesz uruchomić hello TSP solver permutacji. Na przykład uruchom hello następujące polecenia toorun hello solver dla 8 miast.
   
        java -jar TSPSolver.jar 8
   
   Jeśli nie określisz numeru, zostanie on uruchomiony dla 10 miast. Jak hello znalezieniem bieżącego najkrótszy tras, spowoduje to dodanie ich toohello kolejki.

> [!NOTE]
> Liczba, że określono, zostanie uruchomiony dłużej solver hello hello hello Hello większy. Na przykład uruchomiony 14 miasta może potrwać kilka minut i uruchamiane przez 15 miasta może zająć kilka godzin. Zwiększenie too16 lub więcej miast może spowodować dni środowiska uruchomieniowego (ostatecznie tygodnie, miesiące i lata). Jest to powodu toohello szybki wzrost hello liczbę permutacji obliczone przez moduł rozwiązywania hello jako hello liczba wzrasta miast.
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a>Jak toorun hello monitorowania aplikacji klienta
1. Zaloguj się na komputerze tooyour, w którym będzie uruchamiany powitania klienta aplikacji. To nie jest konieczne toobe hello tym samym komputerze, na którym działa hello **TSPSolver** aplikacji, mimo że można go.
2. Utwórz folder, w którym będzie działała aplikacja sieci. Na przykład **c:\TSP**.
3. Kopiuj **TSPClient.jar** za**c:\TSP**,
4. Upewnij się, że folder bin hello JRE znajduje się w zmiennej środowiskowej PATH hello.
5. W wierszu polecenia Zmień tooc:\TSP katalogów.
6. Uruchom następujące polecenie hello.
   
        java -jar TSPClient.jar
   
    Opcjonalnie określ hello liczbę minut toosleep Between sprawdzanie hello kolejki, przekazując argument wiersza polecenia. Witaj domyślny okres uśpienia sprawdzania kolejki hello jest 3 minuty, który jest używany, jeśli żaden argument wiersza polecenia jest przekazywany za**TSPClient**. Toouse inną wartość dla interwału powitania uśpienia, na przykład jedną minutę, uruchomić hello następujące polecenia.
   
        java -jar TSPClient.jar 1
   
    powitania klienta zostanie uruchomiony, dopóki nie widzi ona komunikatu w kolejce "Zakończ". Należy pamiętać, że po uruchomieniu wielu wystąpień hello solver bez uruchamiania powitania klienta może być konieczne toorun powitania klienta kolejki pusty hello toocompletely wiele razy. Alternatywnie można usunąć kolejki hello i utworzyć ją ponownie. kolejki hello toodelete, uruchom następujące hello **TSPSolver** (nie **TSPClient**) polecenia.
   
        java -jar TSPSolver.jar deletequeue
   
    Hello solver zostanie uruchomiony do momentu zakończenia badanie wszystkie trasy.

## <a name="how-toostop-hello-java-applications"></a>Jak toostop hello aplikacji Java
Hello solver i aplikacje klienckie, można nacisnąć klawisz **klawisze Ctrl + C** tooexit, jeśli chcesz, aby tooend toonormal wcześniejszego wykonania.

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
