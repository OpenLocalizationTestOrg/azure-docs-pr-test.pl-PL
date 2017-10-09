---
title: Serwer aplikacji Java aaaRun w klasycznym maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Ten samouczek używa zasobów utworzone za pomocą hello klasycznego modelu wdrażania i pokazuje, jak toocreate wirtualnej systemu Windows maszyny i skonfiguruj go toorun Apache Tomcat aplikacji serwera."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a>Jak toorun serwer aplikacji Java na maszynie wirtualnej utworzone z hello klasycznego modelu wdrażania
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Aby toodeploy szablon Menedżera zasobów aplikacji sieci Web Java 8 i Tomcat, zobacz [tutaj](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).

Przy użyciu platformy Azure można użyć funkcji serwera tooprovide maszyny wirtualnej. Na przykład maszynę wirtualną działającą na platformie Azure można toohost skonfigurowanego serwera aplikacji Java, takich jak Apache Tomcat.

Po zakończeniu pracy w tym przewodniku, trzeba będzie zrozumienia sposobu toocreate maszynę wirtualną działających na platformie Azure i skonfigurować go toorun serwera aplikacji Java. Zostanie Dowiedz się i wykonaj następujące zadania hello:

* Jak toocreate wirtualnej maszynie, która ma Java Development Kit (JDK) już zainstalowane.
* Jak zarejestrować tooremotely tooyour maszyny wirtualnej.
* Jak tooinstall serwer aplikacji Java — Apache Tomcat — na maszynie wirtualnej.
* Jak toocreate punktu końcowego dla maszyny wirtualnej.
* Jak tooopen portu w hello zapory dla serwera aplikacji.

Witaj zakończone wyniki instalacji w Tomcat uruchomione na maszynie wirtualnej.

![Maszyna wirtualna z systemem Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate maszyny wirtualnej
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).  
2. Kliknij przycisk **nowy**, kliknij przycisk **obliczeniowe**, następnie kliknij przycisk **zobaczyć wszystkie** w hello **wyróżnionych aplikacji**.
3. Kliknij przycisk **JDK**, kliknij przycisk **JDK 8** w hello **JDK** okienka.  
   Maszyny wirtualnej obrazy obsługujące **JDK 6** i **JDK 7** są dostępne, jeśli masz starsze aplikacje, które nie są gotowe toorun JDK 8.
4. Wybierz w okienku hello JDK 8 **klasycznego**, następnie kliknij przycisk **Utwórz**.
5. W hello **podstawy** bloku:
   1. Określ nazwę hello maszyny wirtualnej.
   2. Wprowadź nazwę administratora hello w hello **nazwy użytkownika** pola. Należy pamiętać, ta nazwa i hello skojarzone hasło w hello następnego pola. Należy je podczas zdalnego logowania toohello maszyny wirtualnej.
   3. Wprowadź hasło w hello **nowe hasło** pola, a następnie wprowadź je ponownie w hello **Potwierdź hasło** pola. Jest to hasło dla konta administratora hello.
   4. Wybierz odpowiednie hello **subskrypcji**.
   5. Dla hello **grupy zasobów**, kliknij przycisk **Utwórz nowy** , a następnie wprowadź nazwę hello nową grupę zasobów. Lub kliknij przycisk **Użyj istniejącego** i wybierz jedną z hello dostępnych grup zasobów.
   6. Wybierz lokalizację, w którym hello znajduje się maszyna wirtualna, takich jak **południowo-środkowe stany**.
6. Kliknij przycisk **Dalej**.
7. W hello **rozmiar obrazu maszyny wirtualnej** bloku, wybierz opcję **A1 standardowe** lub inny odpowiedni obraz.
8. Kliknij pozycję **Wybierz**.

9. W hello **ustawienia** bloku, kliknij przycisk **OK**. Można użyć wartości domyślnych hello przez platformę Azure.  
10. W hello **Podsumowanie** bloku, kliknij przycisk **OK**.

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a>tooremotely logowania tooyour maszyny wirtualnej
1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **maszyn wirtualnych (klasyczne)**. W razie potrzeby kliknij **więcej usług** na powitania lewym dolnym rogu hello usługi kategoriach. Witaj **maszyn wirtualnych (klasyczne)** wpis ma na liście hello **obliczeniowe** grupy.
3. Kliknij nazwę hello hello maszyny wirtualnej, który chcesz toosign w.
4. Po uruchomieniu maszyny wirtualnej hello, menu u góry okienka hello hello zezwala na połączenia.
5. Kliknij przycisk **Połącz**.
6. Odpowiedz monity toohello jako maszyna wirtualna toohello tooconnect potrzebne. Zwykle Zapisz lub Otwórz plik RDP hello zawierający szczegóły połączenia hello. Może mieć hello toocopy adresu url: port jako ostatnia część hello pierwszy wiersz pliku RDP hello hello i wklej go w aplikacji zdalnej logowania.

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a>tooinstall serwer aplikacji Java na maszynie wirtualnej
Możesz skopiować maszynę wirtualną tooyour serwera aplikacji Java lub zainstalować serwer aplikacji Java za pomocą Instalatora.

Ten samouczek używa Tomcat jako tooinstall serwera aplikacji Java hello.

1. Gdy użytkownik jest zalogowany tooyour maszyny wirtualnej, otwórz sesję przeglądarki zbyt[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).
2. Kliknij dwukrotnie łącze hello **Instalator usługi Windows 32-bitowe/64-bitowych**. Korzystając z tej techniki, Tomcat jest instalowany jako usługa systemu Windows.
3. Po wyświetleniu monitu wybierz toorun hello Instalatora.
4. W ramach hello **Apache Tomcat Instalator** monituje Kreator, wykonaj hello tooinstall Tomcat. Witaj celów tego samouczka akceptując wartości domyślne hello funkcjonuje prawidłowo. Po przejściu hello **hello Kończenie pracy Kreatora instalacji programu Apache Tomcat** okno dialogowe, można opcjonalnie sprawdzić **Uruchom Apache Tomcat** toohave teraz start Tomcat. Kliknij przycisk **Zakończ** toocomplete hello Tomcat procesu instalacji.

## <a name="toostart-tomcat"></a>toostart Tomcat

Możesz ręcznie uruchomić Tomcat Otwieranie wiersza polecenia na maszynie wirtualnej i uruchomione polecenie hello **net&nbsp;start&nbsp;Tomcat8**.

Po uruchomieniu Tomcat, można uzyskać dostęp Tomcat, wprowadzając adres URL hello <adresem http://localhost: 8080> w przeglądarce maszyny wirtualnej hello.

toosee Tomcat uruchomiona z zewnętrznych komputerów, należy toocreate punktu końcowego i otworzyć port.

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a>toocreate punktu końcowego dla maszyny wirtualnej
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **maszyn wirtualnych (klasyczne)**.
3. Kliknij nazwę hello hello maszyny wirtualnej, która jest uruchomiony serwer aplikacji Java.
4. Kliknij przycisk **Punkty końcowe**.
5. Kliknij pozycję **Dodaj**.
6. W hello **dodać punkt końcowy** okno dialogowe:
   1. Określ nazwę dla punktu końcowego hello; na przykład **HttpIn**.
   2. Wybierz **TCP** protokołu hello.
   3. Określ **80** hello portu publicznego.
   4. Określ **8080** dla hello port prywatny.
   5. Wybierz **wyłączone** dla hello pływającego adresu IP.
   6. Pozostaw hello listy kontroli dostępu jest.
   7. Kliknij przycisk hello **OK** przycisk hello tooclose — okno dialogowe i utworzyć punktu końcowego hello.

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a>tooopen port w Zaporze Windows hello dla maszyny wirtualnej
1. Zaloguj się tooyour maszyny wirtualnej.
2. Kliknij przycisk **Start systemu Windows**.
3. Kliknij przycisk **Panel sterowania**.
4. Kliknij przycisk **System i zabezpieczenia**, kliknij przycisk **zapory systemu Windows**, a następnie kliknij przycisk **Zaawansowane ustawienia**.
5. Kliknij przycisk **reguły ruchu przychodzącego**, a następnie kliknij przycisk **nową regułę**.  
   ![Nowej reguły ruchu przychodzącego][NewIBRule]
6. Dla hello **typ reguły**, wybierz pozycję **portu**, a następnie kliknij przycisk **dalej**.  
   ![Nowy port reguły dla ruchu przychodzącego][NewRulePort]
7. Na powitania **protokoły i porty** ekranu wybierz **TCP**, określ **8080** jako hello **określonych portów lokalnych**, a następnie kliknij przycisk **Dalej**.  
  ![Nowej reguły ruchu przychodzącego][NewRuleProtocol]
8. Na powitania **akcji** ekranu wybierz **przyłączenia hello**, a następnie kliknij przycisk **dalej**.
   ![Nowa akcja reguły dla ruchu przychodzącego][NewRuleAction]
9. Na powitania **profilu** ekranu, upewnij się, że **domeny**, **prywatnej**, i **publicznego** są zaznaczone, a następnie kliknij przycisk **dalej** .
   ![Nowy profil reguły dla ruchu przychodzącego][NewRuleProfile]
10. Na powitania **nazwa** ekranu, określ nazwę reguły hello, takich jak **HttpIn** (hello Nazwa reguły nie jest wymagane toomatch hello Nazwa punktu końcowego, jednak), a następnie kliknij przycisk **Zakończ**.  
    ![Nazwa nowej reguły ruchu przychodzącego][NewRuleName]

W tym momencie witryny sieci Web Tomcat powinien być widoczny z zewnętrznej przeglądarki. W oknie przeglądarki hello adresu wpisz adres URL formularza hello  **http://*Twojego\_DNS\_nazwa*. cloudapp.net**, gdzie ***Twojego\_DNS\_nazwa*** jest określony, podczas tworzenia maszyny wirtualnej hello nazwa DNS hello.

## <a name="application-lifecycle-considerations"></a>Zagadnienia dotyczące cyklu życia aplikacji
* Można tworzyć własne archiwum aplikacji sieci web (plik WAR) i dodaj go toohello **webapps** folderu. Na przykład Tworzenie podstawowego projektu sieci web dynamiczne strony usługi Java (JSP) i wyeksportować go jako plik WAR. Następnie skopiuj hello WAR toohello Apache Tomcat **webapps** folderu na maszynie wirtualnej hello, następnie uruchom go w przeglądarce.
* Domyślnie po zainstalowaniu usługi Tomcat hello jest ustawiona toostart ręcznie. Możesz przełączyć go toostart automatycznie za pomocą przystawki usługi hello. Uruchom przystawkę usługi hello klikając **Start systemu Windows**, **narzędzia administracyjne**, a następnie **usług**. Kliknij dwukrotnie hello **Apache Tomcat** usługi i ustaw **uruchamiana** za**automatyczne**.

    ![Ustawienie toostart usługi automatycznie][service_automatic_startup]

    Witaj o konieczności Tomcat automatycznego uruchamiania jest czy rozpoczyna działanie po ponownym uruchomieniu maszyny wirtualnej hello (na przykład po zainstalowaniu aktualizacji oprogramowania, które wymagają ponownego uruchomienia).

## <a name="next-steps"></a>Następne kroki
Informacje na temat innych usług (takich jak magazynu Azure, magistrali usług i bazy danych SQL), które mogą zostać tooinclude z aplikacji Java. Wyświetl hello informacje są dostępne na powitania [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/).

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
