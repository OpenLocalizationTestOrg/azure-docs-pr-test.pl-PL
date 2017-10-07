---
title: "aaaAzure wdrożenia maszyny wirtualnej z Chef | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Chef toodo zautomatyzowane wdrażanie maszyn wirtualnych i konfiguracji w systemie Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a>Automatyzowanie wdrażania maszyny wirtualnej platformy Azure przy użyciu narzędzia Chef
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Chef to doskonałe narzędzie do dostarczania automatyzacji i żądanego stanu konfiguracji.

Z naszych najnowszej wersji interfejsu api chmury Chef zapewnia bezproblemową integrację z platformy Azure, umożliwiając hello tooprovision możliwości i wdrożyć stanami konfiguracji, za pomocą jednego polecenia.

W tym artykule, I opisano sposób tooset się tooprovision środowiska użytkownika Chef wirtualnej Azure maszyny i przeprowadzi użytkownika przez proces tworzenia zasad lub "CookBook", a następnie wdrażania tego tooan cookbook maszyny wirtualnej platformy Azure.

Zacznijmy!

## <a name="chef-basics"></a>Podstawy chef
Przed rozpoczęciem sugeruje recenzowania hello podstawowych pojęciach dotyczących Chef. Istnieje bardzo materiałów <a href="http://www.chef.io/chef" target="_blank">tutaj</a> i najlepiej masz szybkiego odczytu przed podjęciem próby tego przewodnika. Będzie można jednak recap podstawy hello początek.

powitania po diagram przedstawia architekturę Chef wysokiego poziomu hello.

![][2]

Chef ma trzy główne składniki architektury: Chef, Chef klienta (węzeł), Chef stacji roboczej i serwerze.

powitania serwera Chef jest naszych punkt zarządzania i dostępne są dwie opcje dla powitania serwera Chef: hostowanej rozwiązania lub rozwiązaniem w firmie. Użyjemy hostowanego rozwiązania.

Witaj Chef klienta (węzeł) jest hello agenta, która znajduje się na serwerach hello, którym zarządzasz.

Witaj Chef stacji roboczej jest naszych administracyjnej stacji roboczej, którym możemy tworzyć nasze zasady i wykonywać polecenia nasze management. Przeprowadzana hello **nóż** poleceń z hello toomanage stacji roboczej Chef naszej infrastruktury.

Istnieje również hello pojęcie "Cookbooks" i "Przepisami". Efektywne są zasady hello możemy Zdefiniuj i Zastosuj tooour serwerów.

## <a name="preparing-hello-workstation"></a>Przygotowanie stacji roboczej hello
Po pierwsze umożliwia hello przygotowywania stacji roboczej. Używam standardowe stacji roboczej systemu Windows. Potrzebujemy toocreate toostore katalogu plików konfiguracji i cookbooks firmy Microsoft.

Najpierw utwórz katalog o nazwie C:\chef.

Następnie utwórz drugi katalog o nazwie c:\chef\cookbooks.

Teraz potrzebujemy toodownload naszych pliku ustawień platformy Azure, Chef może komunikować się z naszym subskrypcji platformy Azure.

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
Pobierz Twoje ustawienia za pomocą hello PowerShell Azure publikowania [Get AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) polecenia. 

Zapisz hello pliku ustawień publikowania w C:\chef.

## <a name="creating-a-managed-chef-account"></a>Tworzenie zarządzanego konta Chef
Załóż konto hostowanej Chef [tutaj](https://manage.chef.io/signup).

W trakcie zapisywania hello będzie zadawane toocreate nowej organizacji.

![][3]

Po utworzeniu organizacji, Pobierz hello starter kit.

![][4]

> [!NOTE]
> Jeśli zostanie wyświetlony monit, ostrzeżenie, że spowoduje zresetowanie kluczy, jest ok tooproceed jak mamy bez istniejącej infrastruktury jeszcze skonfigurowany.
> 
> 

Ten plik starter kit zip zawiera organizacji plików konfiguracji i kluczy.

## <a name="configuring-hello-chef-workstation"></a>Konfigurowanie stacji roboczej Chef hello
Wyodrębnij zawartość hello hello tooC:\chef chef starter.zip.

Kopiowanie wszystkich plików w katalogu chef-starter\chef repozytorium\.chef tooyour c:\chef katalogu.

Katalogu powinien teraz wyglądać hello poniższy przykład.

![][5]

Teraz powinien mieć cztery pliki, w tym hello Azure publikowania plików w katalogu głównym hello c:\chef.

pliki PEM Hello zawierają organizacji i administratora klucze prywatne do komunikacji podczas hello knife.rb plik zawiera konfigurację Nóż. Potrzebujemy tooedit hello knife.rb pliku.

Otwórz plik hello w wybranym edytorze i zmodyfikować hello "cookbook_path", usuwając hello /... / ze ścieżki hello tak wygląda na to, jak pokazano w następnym.

    cookbook_path  ["#{current_dir}/cookbooks"]

Również dodać hello następująca linia odbicia nazwę hello Azure pliku ustawień publikowania.

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

Plik knife.rb powinna wyglądać podobnie toohello poniższy przykład.

![][6]

Te wiersze zapewnia, że nóż odwołuje się do katalogu cookbooks hello c:\chef\cookbooks i używa również naszych pliku ustawień publikowania platformy Azure podczas operacji platformy Azure.

## <a name="installing-hello-chef-development-kit"></a>Instalowanie hello Chef Development Kit
Następny [Pobierz i zainstaluj](http://downloads.getchef.com/chef-dk/windows) hello tooset ChefDK (Chef Development Kit) zapasowej stacji roboczej Chef.

![][7]

Zainstaluj w lokalizacji domyślnej hello c:\opscode. Ta instalacja potrwa około 10 minut.

Upewnij się, że zmiennej PATH zawiera wpisy dla C:\opscode\chefdk\bin; C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin

Jeśli nie są dostępne, upewnij się, że możesz dodać tych ścieżek!

*Uwaga hello kolejności z hello ścieżki jest ważne!* Jeśli Twoje opscode ścieżek nie są w odpowiedniej kolejności hello masz problemy.

Przed kontynuowaniem uruchom ponownie stację roboczą.

Następnie zostanie zainstalowany hello Azure nóż rozszerzenia. To zapewnia nóż hello "Wtyczkę Azure".

Uruchom następujące polecenie hello.

    chef gem install knife-azure ––pre

> [!NOTE]
> argument — sprzed Hello gwarantuje, że otrzymujesz hello najnowszej wersji RC hello nóż Azure wtyczkę, która zapewnia dostęp toohello najnowszy zestaw interfejsów API.
> 
> 

Istnieje prawdopodobieństwo, że liczba zależności także zostaną zainstalowane na powitania tym samym czasie.

![][8]

tooensure, wszystko jest poprawnie skonfigurowana; hello uruchom następujące polecenie.

    knife azure image list

Jeśli wszystko jest poprawnie skonfigurowane, zobaczysz listę dostępnych obrazów Azure przewiń.

Gratulacje. Konfigurowanie stacji roboczej Witaj!

## <a name="creating-a-cookbook"></a>Tworzenie Cookbook
Cookbook jest używany przez Chef toodefine zestaw poleceń, które chcesz tooexecute na zarządzanym kliencie. Tworzenie Cookbook jest proste i używamy hello **chef Generowanie cookbook** polecenia toogenerate naszych Cookbook szablonu. I będzie wywoływany serwer sieci web Cookbook jako chcę zasadę, która powoduje automatyczne wdrożenie usług IIS.

W obszarze katalogu C:\Chef Uruchom hello następujące polecenia.

    chef generate cookbook webserver

Spowoduje to wygenerowanie zestawu plików w katalogu hello C:\Chef\cookbooks\webserver. Teraz potrzebujemy toodefine hello zestaw poleceń, chcielibyśmy naszych tooexecute klienta Chef w naszym zarządzanej maszynie wirtualnej.

polecenia Hello są przechowywane w hello default.rb pliku. W tym pliku I będzie można definiujący zestaw poleceń, który instaluje usługi IIS, uruchamiania usług IIS i kopiuje folder wwwroot toohello pliku szablonu.

Zmodyfikuj C:\chef\cookbooks\webserver\recipes\default.rb hello i dodaj następujące wiersze hello.

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

Zapisz plik hello, gdy wszystko będzie gotowe.

## <a name="creating-a-template"></a>Tworzenie szablonu
Jak wspomniano wcześniej, potrzebujemy toogenerate pliku szablonu, który będzie używany jako naszą stronę default.html.

Witaj uruchom następujące polecenie toogenerate hello szablonu.

    chef generate template webserver Default.htm

Teraz przejdź toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb pliku. Edytuj plik hello przez dodanie prostego kodu "Hello World" HTML, a następnie zapisz plik hello.

## <a name="upload-hello-cookbook-toohello-chef-server"></a>Przekaż hello Cookbook toohello Chef serwera
W tym kroku wiemy zabierać hello Cookbook, który został utworzony w naszym komputera lokalnego i przekazać go toohello Chef hostowana serwera. Po przekazaniu plików hello Cookbook zostanie wyświetlony w obszarze hello **zasad** kartę.

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a>Wdrażanie maszyny wirtualnej z platformy Azure, nóż
Firma Microsoft będzie teraz wdrożyć maszyny wirtualnej platformy Azure i stosować hello Cookbook "Serwer sieci Web", co spowoduje zainstalowanie naszych usług IIS sieci web usługi i domyślnej strony sieci web.

W kolejności toodo, to należy użyć hello **utworzenie przez serwer nóż azure** polecenia.

Czy na przykład hello polecenia pojawi się dalej.

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

Parametry Hello nie wymaga wyjaśnień. Zastąp określonego zmiennych, a następnie uruchom.

> [!NOTE]
> Za pomocą wiersza polecenia hello hello I używam również Automatyzacja reguł filtra punktu końcowego sieci przy użyciu parametru punkty końcowe tcp — Witaj. I zostały otwarte porty 80 i 3389 strony sieci web toomy dostępu tooprovide i sesji protokołu RDP.
> 
> 

Po uruchomieniu polecenia hello Przejdź toohello Azure portal i zostanie wyświetlony rozpocząć tooprovision komputer.

![][13]

następnie zostanie wyświetlona Hello wiersza polecenia.

![][10]

Po zakończeniu wdrażania hello będziemy usługi sieci web toohello tooconnect stanie za pośrednictwem portu 80 jak firma Microsoft ma otwarty hello port podczas przydzielania firma Microsoft hello maszynę wirtualną z hello Azure nóż polecenia. Ta maszyna wirtualna jest hello tylko maszyny wirtualnej w usłudze w chmurze, połączę go z adresem url usługi chmury hello.

![][11]

Jak widać, otrzymano creative z mojego kodu HTML.

Pamiętaj, że firma Microsoft mogą łączyć za pomocą sesji protokołu RDP z portalu Azure za pośrednictwem portu 3389 hello.

Mam nadzieję, że było to pomocne! Przejdź i uruchom infrastruktury jako przebieg kodu z platformą Azure już dziś!

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
