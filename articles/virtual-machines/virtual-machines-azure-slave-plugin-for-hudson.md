---
title: "aaaHow toouse hello Azure podrzędna wtyczki o ciągłej integracji Hudson | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse hello Azure podrzędna wtyczki o Hudson ciągłej integracji."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>Jak toouse hello Azure podrzędna wtyczki o Hudson ciągłej integracji
Hello Azure podrzędna wtyczki dla Hudson umożliwia tooprovision węzłów podrzędnych na platformie Azure uruchamiania rozproszonych kompilacji.

## <a name="install-hello-azure-slave-plug-in"></a>Zainstaluj hello Azure podrzędna dodatku plug-in
1. W hello Hudson pulpitu nawigacyjnego, kliknij przycisk **Zarządzanie Hudson**.
2. W hello **Zarządzanie Hudson** kliknij pozycję **Zarządzanie wtyczkami**.
3. Kliknij przycisk hello **dostępne** kartę.
4. Kliknij przycisk **wyszukiwania** i typ **Azure** toolimit hello listy toorelevant dodatków plug-in.
   
    Jeśli wybierzesz tooscroll za pośrednictwem listy hello dostępne dodatki plug-in można znaleźć hello Azure podrzędna wtyczki w obszarze hello **klastra zarządzania i dystrybucji kompilacji** części hello **innym** kartę.
5. Zaznacz pole wyboru powitania dla **wtyczki podrzędna Azure**.
6. Kliknij pozycję **Zainstaluj**.
7. Uruchom ponownie Hudson.

Po zainstalowaniu tego dodatku plug-in hello hello następne kroki będą hello tooconfigure wtyczki z profilu subskrypcji platformy Azure i toocreate szablon, który będzie używany podczas tworzenia hello wirtualna hello podrzędny węzła.

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>Skonfiguruj hello Azure podrzędna wtyczki z profilem subskrypcji
Profil subskrypcji również tooas określonego ustawienia publikowania, jest plik XML, który zawiera bezpiecznych poświadczeń i dodatkowe informacje, należy toowork z platformy Azure w środowisku projektowania. tooconfigure hello Azure podrzędna wtyczki, potrzebne są:

* Identyfikator subskrypcji
* Certyfikat zarządzania dla subskrypcji

Są one dostępne w Twojej [profilu subskrypcji]. Poniżej znajduje się przykład profilu subskrypcji.

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

Po utworzeniu profilu subskrypcji, wykonaj te kroki tooconfigure hello Azure podrzędna dodatku plug-in.

1. W hello Hudson pulpitu nawigacyjnego, kliknij przycisk **Zarządzanie Hudson**.
2. Kliknij przycisk **skonfigurować System**.
3. Przewiń w dół hello strony toofind hello **chmury** sekcji.
4. Kliknij przycisk **Dodaj nowe chmury > Microsoft Azure**.
   
    ![Dodaj nowy chmury][add new cloud]
   
    Wyświetli hello pól, których należy tooenter Szczegóły subskrypcji.
   
    ![Konfigurowanie profilu][configure profile]
5. Skopiuj certyfikat zarządzania i identyfikator subskrypcji hello z Twojej subskrypcji i wklej je w odpowiednich polach hello.
   
    Podczas kopiowania hello subskrypcji identyfikator i certyfikat zarządzania, **nie** zawierają hello oferty, które należy ująć hello wartości.
6. Polecenie **konfiguracji Sprawdź**.
7. Gdy hello konfiguracji nie zostanie pomyślnie zweryfikowana, kliknij przycisk **zapisać**.

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>Konfigurowanie szablonu maszyny wirtualnej dla hello Azure podrzędna dodatku plug-in
Szablon maszyny wirtualnej definiuje parametry hello hello wtyczki użyje toocreate węzeł podrzędny na platformie Azure. W hello następujące kroki, możemy utworzyć szablon dla maszyny Wirtualnej systemu Ubuntu.

1. W hello Hudson pulpitu nawigacyjnego, kliknij przycisk **Zarządzanie Hudson**.
2. Polecenie **skonfigurować System**.
3. Przewiń w dół hello strony toofind hello **chmury** sekcji.
4. W ramach hello **chmury** sekcji, Znajdź **dodać szablon maszyny wirtualnej Azure** i kliknij przycisk hello **Dodaj** przycisku.
   
    ![Dodaj szablon maszyny wirtualnej][add vm template]
5. Określ nazwę usługi w chmurze w hello **nazwa** pola. Jeśli nazwa hello odwołuje się tooan istniejące usługi w chmurze, hello maszyny Wirtualnej zostaną zainicjowane w tej usłudze. W przeciwnym razie Azure utworzy nowy.
6. W hello **opis** wprowadź tekst, który opisuje tworzysz szablon hello. Te informacje są tylko do celów dokumentacji i nie jest używany w inicjowania obsługi maszyny Wirtualnej.
7. W hello **etykiety** wprowadź **linux**. Etykieta jest używane tooidentify hello szablon, który tworzysz i szablon hello tooreference następnie używane podczas tworzenia zadania Hudson.
8. Wybierz region, w którym zostanie utworzona hello maszyny Wirtualnej.
9. Wybierz odpowiedni rozmiar maszyny Wirtualnej hello.
10. Określ konto magazynu, w którym zostanie utworzona hello maszyny Wirtualnej. Upewnij się, że jest on hello usługi w chmurze hello należy używać tego samego regionu. Jeśli chcesz, aby nowe toobe magazynu utworzony, to pole może pozostać puste.
11. Czas przechowywania określa hello liczbę minut, zanim Hudson usuwa bezczynności podrzędna. Pozostaw to wartość domyślna hello 60.
12. W **użycia**, wybierz hello odpowiedniego warunku, gdy będzie można użyć ten węzeł podrzędny. Teraz, wybierz **korzystać z tego węzła możliwie**.
    
     W tym momencie formularza będzie wyglądać nieco podobne toothis:
    
     ![Konfiguracja szablonu][template config]
13. W **rodziny obrazu lub identyfikator** ma toospecify obrazów systemu zostanie zainstalowana na maszynie Wirtualnej. Możesz wybrać z listy obrazów rodzin lub określ niestandardowy obraz.
    
     Tooselect z listy rodzin obrazu, wprowadź hello pierwszego znaku (z uwzględnieniem wielkości liter) Nazwa rodziny hello obrazu. Na przykład wpisanie **U** pojawi się lista rodzin Ubuntu Server. Po wybraniu z listy hello Wpięć użyje najnowszej wersji tego obrazu systemu z tej rodziny hello podczas inicjowania obsługi administracyjnej maszyny Wirtualnej.
    
     ![Listy rodziny systemów operacyjnych][OS family list]
    
     Jeśli chcesz toouse niestandardowego obrazu, wprowadź nazwę hello niestandardowego obrazu. Nazwy niestandardowego obrazu nie są wyświetlane na liście, który pozwala uzyskać tooensure, który hello nazwa został wprowadzony prawidłowo.    
    
     W tym samouczku, wpisz **U** toobring listy obrazów Ubuntu i wybierz **Ubuntu Server 14.04 LTS**.
14. Dla **uruchamiania metody**, wybierz pozycję **SSH**.
15. Poniższy skrypt hello kopiowania i wklejania w hello **skryptu Init** pola.
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     Witaj **skryptu Init** zostanie wykonany po hello zostanie utworzona maszyna wirtualna. W tym przykładzie skrypt hello instaluje Java, usługi git i ant.
16. W hello **Username** i **hasło** pól, wprowadź wartości preferowanych hello konta administratora, który zostanie utworzony na maszynie Wirtualnej.
17. Polecenie **Sprawdź szablon** toocheck, jeśli można określić parametry hello są prawidłowe.
18. Kliknij przycisk **Zapisz**.

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>Utwórz zadanie Hudson uruchamianego na węzeł podrzędny na platformie Azure
W tej sekcji trzeba utworzyć zadania Hudson, które zostanie uruchomione w węźle podrzędna na platformie Azure.

1. W hello Hudson pulpitu nawigacyjnego, kliknij przycisk **nowe zadanie**.
2. Wprowadź nazwę hello zadania, które tworzysz.
3. Typ zadania hello wybierz **kompilacji zadanie oprogramowania wolne stylu**.
4. Kliknij przycisk **OK**.
5. Na stronie konfiguracji zadania hello wybierz **Ogranicz, w którym można uruchomić tego projektu**.
6. Wybierz **węzła i etykiety menu** i wybierz **linux** (możemy określona etykieta w podczas tworzenia szablonu maszyny wirtualnej hello w poprzedniej sekcji hello).
7. W hello **kompilacji** kliknij **kroku kompilacji Dodaj** i wybierz **wykonywania powłoki**.
8. Edytuj hello następującego skryptu, zastępując **{nazwa konta usługi github}**, **{nazwę projektu}**, i **{katalogu projektu}** z odpowiednie wartości, a następnie wklej hello Edytowanie skryptu w hello obszaru tekstu, który pojawia się.
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. Kliknij przycisk **Zapisz**.
10. W hello Hudson pulpitu nawigacyjnego, Znajdź zadanie hello właśnie utworzony i kliknij pozycję hello **zaplanować kompilacji** ikony.

Hudson będą utworzyć przy użyciu szablonu hello utworzonego w poprzedniej sekcji hello węzeł podrzędny i uruchom skrypt hello określone w hello kroku kompilacji dla tego zadania.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[profilu subskrypcji]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

