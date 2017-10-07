---
title: "aaaSet się Apache Tomcat na maszynie wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset się Apache Tomcat7 przy użyciu maszyn wirtualnych Azure z systemem Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a>Konfigurowanie Tomcat7 na maszynie wirtualnej systemu Linux przy użyciu platformy Azure
Apache Tomcat (lub po prostu Tomcat, również nazywanych Jakarta Tomcat) to serwer sieci web typu open source i kontener serwlet opracowane przez hello Foundation oprogramowania Apache (ASF). Tomcat implementuje hello Serwlet Java i hello specyfikacje Sun Microsystems JavaServer Pages (JSP). Tomcat udostępnia czysty środowisko serwera sieci web Java HTTP w których toorun kodu języka Java. W hello najprostsza konfiguracja Tomcat działa w procesie jeden system operacyjny. Ten proces jest uruchomiony maszyny wirtualnej Java (JVM). Każde żądanie HTTP z tooTomcat przeglądarki jest przetwarzany jako oddzielnym wątku w procesie Tomcat hello.  

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule opisano, jak toouse hello klasycznego modelu wdrażania. Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager hello. Zobacz toouse toodeploy szablon Menedżera zasobów maszyny Wirtualnej systemu Ubuntu JDK otwarte i Tomcat, [w tym artykule](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).

W tym artykule zainstalujesz Tomcat7 w obrazie systemu Linux i wdrożyć go na platformie Azure.  

Dowiesz się:  

* Jak toocreate maszynę wirtualną na platformie Azure.
* Jak tooprepare hello maszyny wirtualnej dla Tomcat7.
* Jak tooinstall Tomcat7.

Zakłada się, że masz już subskrypcję platformy Azure.  Jeśli nie, można założyć bezpłatnej wersji próbnej na [hello Azure witryny sieci Web](https://azure.microsoft.com/). Jeśli masz subskrypcję MSDN, zobacz [specjalne cennik Microsoft Azure: MSDN, MPN i korzyści BizSpark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39). toolearn więcej informacji na temat usługi Azure, zobacz [co to jest Azure?](https://azure.microsoft.com/overview/what-is-azure/).

W tym artykule przyjęto założenie, że masz podstawową wiedzę na temat pracy z Tomcat i Linux.  

## <a name="phase-1-create-an-image"></a>Faza 1: Tworzenie obrazu
W tej fazie spowoduje utworzenie maszyny wirtualnej za pomocą obrazu systemu Linux na platformie Azure.  

### <a name="step-1-generate-an-ssh-authentication-key"></a>Krok 1: Generowanie klucza uwierzytelniania SSH
SSH jest narzędziem ważne dla administratorów systemu. Konfigurowanie zabezpieczeń dostępu na podstawie hasła ustalić ludzkich nie jest jednak zalecane. Złośliwi użytkownicy można podzielić na podstawie nazwy użytkownika i hasło słabe systemu.

Dobra wiadomość Hello jest, czy istnieje sposób tooleave dostępu zdalnego Otwórz i nie martw się o hasłach. Ta metoda składa się z uwierzytelniania za pomocą kryptografii asymetrycznej. Witaj klucza prywatnego użytkownika jest hello, który przyznaje hello uwierzytelniania. Można nawet blokować hello konta toonot Zezwalaj na uwierzytelnianie hasła.

Zaletą tej metody jest niepotrzebne toosign różnych haseł w toodifferent serwerów. Można uwierzytelniać za pomocą klucza prywatnego osobistego hello na wszystkich serwerach, co zapobiega konieczności tooremember kilka haseł.



Wykonaj te kroki toogenerate hello SSH uwierzytelniania klucza.

1. Pobierz i zainstaluj PuTTYgen z następującej lokalizacji hello: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Uruchom Puttygen.exe.
3. Kliknij przycisk **Generuj** toogenerate hello kluczy. W procesie hello może zwiększyć losowości przez przenoszenie hello myszy nad hello pusty obszar w oknie hello.  
   ![PuTTY zrzut ekranu generatora klucza, pokazujący hello nowego klucza przycisk Generuj][1]
4. Po hello Generuj proces, Puttygen.exe wyświetli nowy klucz publiczny.  
   ![PuTTY zrzut ekranu generatora klucza, pokazujący hello nowego klucza publicznego i hello prywatnego klucza przyciskiem Zapisz][2]
5. Zaznacz i skopiuj klucz publiczny hello i zapisz go w pliku o nazwie publicKey.pem. Nie klikaj pozycji **Zapisz klucz publiczny**, ponieważ jest inny niż klucz publiczny hello chcemy hello zapisanego formatu pliku klucza publicznego.
6. Kliknij przycisk **Zapisz klucz prywatny**i zapisz go w pliku o nazwie privateKey.ppk.

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a>Krok 2: Tworzenie obraz powitania w hello portalu Azure
1. W hello [portal](https://portal.azure.com/), kliknij przycisk **nowy** w hello zadań paska toocreate obrazu. Następnie wybierz obraz systemu Linux hello jest na podstawie Twoich potrzeb. Witaj poniższym przykładzie użyto hello Ubuntu 14.04 obrazu.
![Zrzut ekranu przedstawiający portal hello, który zawiera przycisk Nowy hello][3]

2. Aby uzyskać **nazwy hosta**, określ nazwę hello hello adres URL, czy użytkownik i klientów internetowych użyje tooaccess tej maszyny wirtualnej. Zdefiniuj hello ostatnia część hello nazwy DNS, na przykład tomcatdemo. Azure będzie generować hello adresu URL jako tomcatdemo.cloudapp.net.  

3. Dla **klucz uwierzytelniania SSH**, skopiuj wartość klucza hello z hello publicKey.pem pliku, który zawiera klucz publiczny hello generowane przez PuTTYgen.  
![Wprowadź klucz uwierzytelniania SSH w portalu hello][4]

4. Skonfiguruj inne ustawienia, a następnie kliknij przycisk **Utwórz**.  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a>Faza 2: Przygotowanie maszyny wirtualnej do Tomcat7
W tym kroku zostanie konfigurowania punktu końcowego dla ruchu Tomcat, a następnie połącz tooyour nowej maszyny wirtualnej.

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a>Krok 1: Otwórz dostęp w sieci web tooallow portu hello HTTP
Punkty końcowe platformy Azure składają się z protokołem TCP lub UDP, oraz port publiczny i prywatny. port prywatny Hello jest port hello, że maszyna wirtualna hello tooon nasłuchuje usługa hello. port publiczny Hello jest port hello hello usługi w chmurze Azure nasłuchuje tooexternally dla ruchu przychodzącego, internetowego.  

TCP port 8080 jest hello domyślny numer portu używany toolisten Tomcat. Ten port jest otwarty z punktu końcowego platformy Azure, możesz i innych Klienci internetowi mogą uzyskiwać dostęp stron Tomcat.  

1. W portalu powitania kliknij **Przeglądaj** > **maszyn wirtualnych**, a następnie kliknij przycisk hello maszyny wirtualnej, który został utworzony.  
   ![Zrzut ekranu przedstawiający hello katalogu maszyny wirtualne][5]
2. tooadd punktu końcowego maszyny wirtualnej tooyour, kliknij przycisk hello **punkty końcowe** pole.
   ![Zrzut ekranu pokazujący pole punkty końcowe hello][6]
3. Kliknij pozycję **Dodaj**.  

   1. Dla punktu końcowego hello, wprowadź nazwę dla punktu końcowego hello w **punktu końcowego**, a następnie wprowadź 80 w **Port publiczny**.  

      Jeśli zostanie ustawiona too80, nie potrzebujesz numeru portu hello tooinclude hello adres URL, który jest używany tooaccess Tomcat. Na przykład http://tomcatdemo.cloudapp.net.    

      Jeśli zostanie ustawiona wartość tooanother, na przykład 81, należy tooadd hello portu numer toohello adres URL tooaccess Tomcat. Na przykład http://tomcatdemo.cloudapp.net:81 /.
   2. Wprowadź 8080 w **Port prywatny**. Domyślnie Tomcat nasłuchuje na porcie TCP 8080. Zmieniono hello domyślne nasłuchiwania portu Tomcat, należy zaktualizować **Port prywatny** toobe hello tak samo jak hello port nasłuchiwania Tomcat.  
      ![Zrzut ekranu z interfejsu użytkownika, który zawiera polecenie Dodaj, Port publiczny i Port prywatny][7]
4. Kliknij przycisk **OK** maszyny wirtualnej tooyour tooadd hello punktu końcowego.

### <a name="step-2-connect-toohello-image-you-created"></a>Krok 2: Łączenie toohello obrazu, który został utworzony
Można wybrać żadnej maszyny wirtualnej tooyour tooconnect SSH narzędzia. W tym przykładzie używamy programu PuTTY.  

1. Pobierz nazwę DNS hello maszyny wirtualnej z hello portalu.
    1. Kliknij przycisk **Przeglądaj** > **maszyn wirtualnych**.
    2. Wybierz nazwę hello maszyny wirtualnej, a następnie kliknij przycisk **właściwości**.
    3. W hello **właściwości** kafelka, Szukaj w hello **nazwy domeny** nazwy DNS hello tooget pole.  

2. Pobierz hello numer portu dla połączenia SSH z hello **SSH** pole.  
![Zrzut ekranu pokazujący numer portu połączenia SSH hello][8]

3. Pobierz [PuTTY](http://www.putty.org/).  

4. Po pobraniu, kliknij plik wykonywalny hello Putty.exe. W konfiguracji programu PuTTY Konfiguruj opcje Podstawowe hello hello nazwy hosta i portu numer uzyskany z hello właściwości maszyny wirtualnej.   
![Zrzut ekranu pokazujący hello PuTTY konfiguracji hosta, portu i opcje][9]

5. W okienku po lewej stronie powitania kliknij **połączenia** > **SSH** > **uwierzytelniania**, a następnie kliknij przycisk **Przeglądaj** toospecify Lokalizacja Hello hello privateKey.ppk pliku. Plik privateKey.ppk Hello zawiera hello klucza prywatnego, który jest generowany przez PuTTYgen we wcześniejszej części hello "faza 1: Tworzenie obrazu" w dalszej części tego artykułu.  
![Zrzut ekranu pokazujący hierarchii katalogów połączenia hello i przycisk przeglądania][10]

6. Kliknij przycisk **Otwórz**. Użytkownik może otrzymywać alerty przez okno komunikatu. Jeśli skonfigurowano hello nazwę DNS i numer portu poprawnie, kliknij przycisk **tak**.
![Zrzut ekranu pokazujący hello powiadomień][11]

7. Możesz się zostanie wyświetlony monit o tooenter nazwy użytkownika.  
![Zrzut ekranu pokazujący, gdzie tooenter nazwy użytkownika][12]

8. Wprowadź nazwę użytkownika hello używane maszyny wirtualnej hello toocreate w hello "faza 1: Tworzenie obrazu" wcześniej w tym artykule. Zostanie wyświetlony ekran podobny do następujących hello:  
![Zrzut ekranu pokazujący hello uwierzytelniania potwierdzenia][13]

## <a name="phase-3-install-software"></a>Faza 3: Instalacja oprogramowania
Na tym etapie należy zainstalować środowisko uruchomieniowe języka Java hello, Tomcat7 i inne składniki Tomcat7.  

### <a name="java-runtime-environment"></a>Środowisko uruchomieniowe języka Java
Tomcat jest napisany w języku Java. Istnieją dwa rodzaje Java Development Kit (JDKs), OpenJDK i Oracle JDK. Można wybrać hello żądanego.  

> [!NOTE]
> Zarówno JDKs mają prawie hello sam kod klasy hello w hello interfejsu API języka Java, ale jest różny kod hello hello maszyny wirtualnej. OpenJDK zwykle toouse otwarte biblioteki, podczas gdy zwykle Oracle JDK toouse zamknięte te. Oracle JDK ma więcej klasy, a niektóre stałe usterek i Oracle JDK jest stabilna więcej niż OpenJDK.

#### <a name="install-openjdk"></a>Zainstaluj OpenJDK  

Użyj następującego polecenia toodownload OpenJDK hello.   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* toocreate toocontain katalogu hello JDK plików:  

        sudo mkdir /usr/lib/jvm  
* tooextract hello JDK pliki w katalogu/usr/lib/jvm/hello:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a>Zainstaluj Oracle JDK


Użyj hello następujące polecenia toodownload Oracle JDK z witryny sieci Web hello Oracle.  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* toocreate toocontain katalogu hello JDK plików:  

        sudo mkdir /usr/lib/jvm  
* tooextract hello JDK pliki w katalogu/usr/lib/jvm/hello:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* tooset Oracle JDK jako hello maszyny wirtualnej Java domyślne:  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a>Upewnij się, że Java Instalacja powiodła się
Można użyć polecenia, takich jak powitania po tootest środowiska uruchomieniowego hello jest poprawnie zainstalowany:  

    java -version  

Jeśli zainstalowano OpenJDK, powinien zostać wyświetlony komunikat podobnie następującej hello: ![OpenJDK pomyślnej instalacji wiadomości][14]

Jeśli zainstalowano Oracle JDK, powinien zostać wyświetlony komunikat podobnie następującej hello: ![komunikat instalacji pomyślne JDK Oracle][15]

### <a name="install-tomcat7"></a>Zainstaluj Tomcat7
Użyj następującego polecenia tooinstall Tomcat7 hello.  

    sudo apt-get install tomcat7  

Jeśli nie używasz Tomcat7, użyj hello odpowiednią odmianę tego polecenia.  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a>Upewnij się, że Tomcat7 Instalacja powiodła się
Po pomyślnym zainstalowaniu Tomcat7 toocheck Przeglądaj nazwa DNS serwera Tomcat tooyour. W tym artykule hello przykładowy adres URL jest http://tomcatexample.cloudapp.net/. Jeśli zostanie wyświetlony komunikat z takich jak następujące hello Tomcat7 jest poprawnie zainstalowany.
![Komunikat instalacji Tomcat7 powiodło się][16]

### <a name="install-other-tomcat7-components"></a>Instalowanie innych składników Tomcat7
Istnieją inne składniki opcjonalne Tomcat, które można zainstalować.  

Użyj hello **tomcat7 stanie pamięci podręcznej wyszukiwania sudo** toosee polecenia wszystkie dostępne składniki hello. Użyj następującego polecenia tooinstall hello niektórych składników przydatne.  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a>Faza 4: Konfigurowanie Tomcat7
Na tym etapie można administrować Tomcat.

### <a name="start-and-stop-tomcat7"></a>Uruchamianie i zatrzymywanie Tomcat7
Serwer Tomcat7 Hello jest uruchamiana automatycznie po zainstalowaniu go. Można również uruchomić z hello następujące polecenie:   

    sudo /etc/init.d/tomcat7 start

toostop Tomcat7:

    sudo /etc/init.d/tomcat7 stop

Stan hello tooview Tomcat7:

    sudo /etc/init.d/tomcat7 status

toorestart Tomcat usługi: 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a>Administracja Tomcat7
Można edytować hello Tomcat użytkownika konfiguracji pliku tooset się swoje poświadczenia administratora. Witaj Użyj następującego polecenia:  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

Oto przykład:  
![Zrzut ekranu pokazujący hello sudo vi polecenia w danych wyjściowych][17]  

> [!NOTE]
> Utwórz silne hasło dla nazwy użytkownika administratora hello.  

Po zmodyfikowaniu tego pliku, należy ponownie uruchomić usługi Tomcat7 z hello tooensure polecenia czy hello zmiany zostały wprowadzone następujące:  

    sudo /etc/init.d/tomcat7 restart  

Otwórz przeglądarkę i wprowadź **http://<your tomcat server DNS name>/Menedżera/html** jako hello adresu URL. Na przykład hello w tym artykule adres URL hello jest http://tomcatexample.cloudapp.net/manager/html.  

Po połączeniu, powinny być widoczne następujące toohello coś podobnego:  
![Zrzut ekranu przedstawiający hello Menedżer aplikacji sieci Web Tomcat][18]

## <a name="common-issues"></a>Typowe problemy
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a>Nie można uzyskać dostęp do maszyny wirtualnej hello Tomcat i Moodle z hello Internet
#### <a name="symptom"></a>Objaw  
  Tomcat jest uruchomiony, ale nie widać hello Tomcat domyślną stronę w przeglądarce.
#### <a name="possible-root-cause"></a>Możliwe przyczyny   

  * port nasłuchu Tomcat Hello nie jest hello taki sam jak port prywatny hello punktu końcowego maszyny wirtualnej dla ruchu Tomcat.  

     Sprawdź portu publicznego i prywatnego portu ustawienia punktu końcowego i upewnij się, że port prywatny hello jest taki sam, jak hello Tomcat hello nasłuchiwać portu. Zobacz "faza 1: Tworzenie obrazu" tego artykułu, aby uzyskać instrukcje dotyczące konfigurowania punktów końcowych dla maszyny wirtualnej.  

     Witaj toodetermine Tomcat nasłuchiwać portu, otwórz /etc/httpd/conf/httpd.conf (Red Hat release) lub /etc/tomcat7/server.xml (wersja Debian). Domyślnie program hello port nasłuchiwania Tomcat jest 8080. Oto przykład:  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     Jeśli używasz maszynę wirtualną, takie jak Debian i Ubuntu i mają toochange hello domyślnego portu z Tomcat nasłuchiwania (na przykład 8081), należy również otworzyć port hello hello systemu operacyjnego. Najpierw otwórz profilu hello:  

        sudo vi /etc/default/tomcat7  

     Następnie usuń komentarz hello ostatniego wiersza i zmień "nie" za "yes".  

        AUTHBIND=yes
  2. Zapora Hello wyłączył hello nasłuchiwania portu Tomcat.

     Może zobaczyć tylko hello Tomcat domyślną stronę z hello hosta lokalnego. Hello problem jest najbardziej prawdopodobne, że hello portu, który jest nasłuch tooby Tomcat, jest blokowany przez zaporę hello. Możesz użyć hello w3m narzędzie toobrowse hello strony sieci Web. Witaj następujące polecenia Zainstaluj w3m i Przeglądaj toohello Tomcat domyślnej strony:  


        sudo yum instalacji w3m w3m-img


        w3m adresem http://localhost: 8080  
#### <a name="solution"></a>Rozwiązanie

  * Jeśli hello port nasłuchiwania Tomcat nie jest hello sam jako port prywatny hello punktu końcowego hello maszyny wirtualnej toohello ruchu, należy zmienić port prywatny hello toobe hello tak samo jak hello port nasłuchiwania Tomcat.   
  2. Jeśli problem hello jest spowodowany przez zaporę/iptables, Dodaj następujące wiersze zbyt/etc/sysconfig/iptables hello. drugi wiersz Hello jest potrzebna tylko dla ruchu https:  

      -A -p tcp -m tcp--dport 80 -j AKCEPTUJ wejściowych

      -A -p tcp -m tcp--dport 443 -j AKCEPTUJ wejściowych  

     > [!IMPORTANT]
     > Upewnij się, że wierszy poprzedniej hello są pozycjonowane powyżej, które globalnie ograniczałyby dostępu, takich jak hello następujące: - wejściowych -j Odrzuć — Odrzuć with zabronione hostów protokołu icmp



tooreload hello iptables, uruchom następujące polecenie hello:

    service iptables restart

To została przetestowana CentOS 6.3.

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a>Pozwolono podczas ładowania projektu pliki zbyt/var/lib/tomcat7/webapps /
#### <a name="symptom"></a>Objaw
  Gdy maszynę wirtualną tooyour tooconnect SFTP klienta (na przykład FileZilla) i przejdź zbyt/var/lib/tomcat7/webapps/toopublish witryny, zostanie wyświetlony błąd komunikat podobny toohello następujące:  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a>Możliwe przyczyny
  Nie masz żadnych uprawnień tooaccess hello /var/lib/tomcat7/webapps folderu.  
#### <a name="solution"></a>Rozwiązanie  
  Wymagane jest uprawnienie tooget z hello konta głównego. Nazwa głównego toohello użytkownika używane podczas przydzielania maszyny hello, można zmienić hello prawo własności do tego folderu. Oto przykład nazwą konta azureuser hello:  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  Użyj zbyt hello -R — opcja tooapply hello uprawnienia dla wszystkich plików w katalogu.  

  To polecenie działa również w przypadku katalogów. zmiany opcji -R Hello hello uprawnienia dla wszystkich plików i katalogów w katalogu hello. Oto przykład:  

     sudo chown -R username:group directory  

  To polecenie powoduje zmianę własności (użytkowników i grup) dla wszystkich plików i katalogów, które znajdują się w katalogu hello.  

  Witaj następujące polecenie tylko zmienia uprawnienia hello hello folder katalogu. Witaj pliki i foldery w katalogu hello nie są zmieniane.  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
