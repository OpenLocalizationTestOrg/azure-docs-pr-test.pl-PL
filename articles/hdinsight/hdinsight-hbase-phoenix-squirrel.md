---
title: aaaUse Apache Phoenix i SQuirreL z systemem Windows Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Apache Phoenix w usłudze HDInsight i w jaki sposób tooinstall i skonfigurować SQuirreL na stacji roboczej klastra HBase tooan tooconnect w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a>Użyj Apache Phoenix i SQuirreL z klastrami HBase opartych na systemie Windows w usłudze HDInsight
Dowiedz się, jak toouse [Apache Phoenix](http://phoenix.apache.org/) w usłudze HDInsight i w jaki sposób tooinstall i skonfigurować SQuirreL na stacji roboczej klastra HBase tooan tooconnect w usłudze HDInsight. Aby uzyskać więcej informacji na temat Phoenix, zobacz [Phoenix w ciągu 15 minut lub mniej](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Aby hello Phoenix gramatyki, zobacz [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Aby hello Phoenix informacje o wersji w usłudze HDInsight, zobacz [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight?](hdinsight-component-versioning.md).
>

> [!IMPORTANT]
> Witaj czynnościach w ramach tego dokumentu działa tylko w przypadku klastrów usługi HDInsight opartej na systemie Windows. HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows). Uzyskać informacji na temat używania Phoenix na opartych na systemie Linux usługi HDInsight, zobacz [Użyj Apache Phoenix z bazy danych HBase opartych na systemie Linux klastrów w usłudze HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).
>



## <a name="use-sqlline"></a>Użyj SQLLine
[SQLLine](http://sqlline.sourceforge.net/) jest tooexecute narzędzie wiersza polecenia SQL.

### <a name="prerequisites"></a>Wymagania wstępne
Przed użyciem SQLLine, musi mieć następujące hello:

* **Klaster HBase w usłudze HDInsight**. Aby uzyskać informacje dotyczące udostępniania bazy danych HBase klastra, zobacz [Rozpoczynanie pracy z bazy danych Apache HBase w usłudze HDInsight][hdinsight-hbase-get-started].
* **Połącz klaster HBase toohello za pośrednictwem protokołu RDP hello**. Aby uzyskać instrukcje, zobacz [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu klasycznego portalu Azure hello][hdinsight-manage-portal].

**toofind limit hello nazwy hosta**

1. Otwórz **wiersza polecenia platformy Hadoop** z hello pulpitu.
2. Uruchom hello następującego sufiksu DNS hello tooget polecenia:

        ipconfig

    Zapisz **sufiks DNS konkretnego połączenia**. Na przykład *myhbasecluster.f5.internal.cloudapp.net*. Po ustanowieniu połączenia klastra HBase tooan należy tooone tooconnect z hello dozorcy przy użyciu nazwy FQDN. Każdy klaster usługi HDInsight ma dozorcy 3. Są one *zookeeper0*, *zookeeper1*, i *zookeeper2*. Witaj nazwa FQDN będzie wyglądać mniej więcej tak *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.

**toouse SQLLine**

1. Otwórz **wiersza polecenia platformy Hadoop** z hello pulpitu.
2. Uruchom następujące polecenia tooopen SQLLine hello:

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    Witaj polecenia używane w przykładowym hello:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

Aby uzyskać więcej informacji, zobacz [ręcznego SQLLine](http://sqlline.sourceforge.net/#manual) i [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="use-squirrel"></a>Użyj SQuirreL
[Klient SQL sQuirreL](http://squirrel-sql.sourceforge.net/) graficznego program Java, który pozwala tooview hello struktury bazy danych zgodne JDBC, Przeglądaj hello dane w tabelach, wydania poleceń SQL itp. Może być używane tooconnect tooApache Phoenix w usłudze HDInsight.

W tej sekcji opisano sposób tooinstall i skonfigurować SQuirreL na stacji roboczej tooconnect tooan HBase klastra w usłudze HDInsight za pośrednictwem sieci VPN.

### <a name="prerequisites"></a>Wymagania wstępne
Przed wykonaniem procedury hello, musi mieć następujące hello:

* Klaster HBase wdrożyć tooan sieci wirtualnej platformy Azure z maszyną wirtualną DNS.  Aby uzyskać instrukcje, zobacz [HBase Tworzenie klastrów w sieci wirtualnej Azure][hdinsight-hbase-provision-vnet].

* Pobierz sufiks DNS konkretnego połączenia programu hello HBase klastra klastra. tooget go RDP do klastra hello, a następnie uruchom polecenie IPConfig.  sufiks DNS Hello jest podobny do:

        myhbase.b7.internal.cloudapp.net
* Pobierz i zainstaluj [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) na stacji roboczej. Konieczne będzie makecert z toocreate pakietu hello certyfikatu.  
* Pobierz i zainstaluj [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) na stacji roboczej.  SQuirreL SQL klienta w wersji 3.0 lub nowszego wymaga środowiska JRE wersji 1.6 lub nowszej.  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a>Skonfiguruj toohello połączenia sieci VPN typu punkt-lokacja sieci wirtualnej platformy Azure
Obejmuje 3 kroki konfigurowania połączenia VPN punkt lokacja:

1. [Konfigurowanie sieci wirtualnej i brama routingu dynamicznego](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [Tworzenie certyfikatów](#Create-your-certificates)
3. [Konfigurowanie klienta sieci VPN](#Configure-your-VPN-client)

Zobacz [skonfigurować tooan połączenia sieci VPN typu punkt-lokacja sieci wirtualnej Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) Aby uzyskać więcej informacji.

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a>Konfigurowanie sieci wirtualnej i brama routingu dynamicznego
Upewnić się, że po uprzednim udostępnieniu klaster HBase w sieci wirtualnej platformy Azure (patrz wymagania wstępne powitania dla tej sekcji). Witaj następnym krokiem jest tooconfigure połączenie punkt lokacja.

**połączenie punkt lokacja hello tooconfigure**

1. Zaloguj się toohello [klasycznego portalu Azure][azure-portal].
2. Powitania po lewej stronie, kliknij przycisk **sieci**.
3. Kliknij przycisk hello sieci wirtualnej zostały utworzone (zobacz [klastrów HBase udostępniania w sieci wirtualnej Azure][hdinsight-hbase-provision-vnet]).
4. Kliknij przycisk **Konfiguruj** od góry hello.
5. W hello **połączenie punkt lokacja** zaznacz **Konfiguracja połączenia punkt lokacja**.
6. Skonfiguruj **uruchamianie IP** i **CIDR** adresów toospecify hello zakres adresów IP z których klienci VPN będą otrzymywać adresu IP po połączeniu. Witaj zakresu nie może nakładać się ze wszystkimi hello zakresy znajduje się w lokalnej sieci i hello sieci wirtualnej platformy Azure, które będą łączyć się. Na przykład. w przypadku wybrania 10.0.0.0/20 hello sieci wirtualnej, można wybrać 10.1.0.0/24 dla przestrzeni adresowej powitania klienta. Zobacz hello [punkt-lokacja, łączność] [ vnet-point-to-site-connectivity] strony, aby uzyskać więcej informacji.
7. W sekcji spacje adresów sieci wirtualnej powitania kliknij **Dodaj podsieć bramy**.
8. Kliknij przycisk **ZAPISAĆ** na powitania u dołu strony hello.
9. Kliknij przycisk **tak** tooconfirm hello zmiany. Poczekaj, aż hello system zakończył wprowadzania hello zmiany przed kontynuowaniem toohello następnej procedury.

**toocreate dynamiczne bramy routingu**

1. Hello klasycznego portalu Azure, kliknij **pulpitu NAWIGACYJNEGO** od góry hello hello strony.
2. Kliknij przycisk **Tworzenie bramy** od dołu hello hello strony.
3. Kliknij przycisk **tak** tooconfirm. Poczekaj, aż utworzeniu hello bramy.
4. Kliknij przycisk **pulpitu NAWIGACYJNEGO** od góry hello.  Zostanie wyświetlony visual diagram hello sieci wirtualnej:

    ![Diagram wirtualnego punkt lokacja sieci wirtualnej platformy Azure][img-vnet-diagram]

    Witaj diagram przedstawia 0 połączeń klientów. Po wprowadzeniu toohello połączenia wirtualnej sieci numer hello będzie tooone zaktualizowane.

#### <a name="create-your-certificates"></a>Tworzenie certyfikatów
Jednym ze sposobów toocreate jest certyfikatu X.509 przy użyciu hello narzędzie tworzenia certyfikatów (makecert.exe), który jest dostarczany z [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).

**toocreate certyfikat główny z podpisem własnym**

1. Na stacji roboczej otwórz okno wiersza polecenia.
2. Przejdź folder Narzędzia Visual Studio toohello.
3. następujące polecenie w poniższym przykładzie hello Hello utworzy i zainstalować certyfikat główny w magazynie certyfikatów osobistych hello na stacji roboczej i również utworzyć odpowiedni plik .cer będzie jego przesłania toohello klasycznego portalu Azure.

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    Zmień toohello katalogu, który ma być hello toobe pliku .cer znajdują się w, gdzie HBaseVnetVPNRootCertificate jest nazwa hello mają toouse hello certyfikatu.

    Nie zamykaj hello wiersza polecenia.  Będzie on potrzebny w następnej procedurze hello.

   > [!NOTE]
   > Ponieważ utworzono certyfikat główny, z którego zostanie wygenerowana certyfikaty klienta, może mają tooexport ten certyfikat wraz z kluczem prywatnym i zapisz go w bezpiecznym miejscu tooa, których mogą zostać odzyskane.
   >
   >

**toocreate certyfikatu klienta**

* Z hello sam wiersz polecenia (ma toobe na powitania tym samym komputerze, na którym utworzono hello certyfikatu głównego. certyfikat klienta na powitania musi zostać wygenerowany z hello certyfikatu głównego), uruchom hello następujące polecenie:

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    HBaseVnetVPNRootCertificate jest nazwa certyfikatu głównego hello.  Ma ona nazwę certyfikatu głównego hello toomatch.  

    Zarówno hello certyfikatu głównego, jak i certyfikat klienta na powitania są przechowywane w magazynie certyfikatów osobistych na komputerze. Użyj certmgr.msc tooverify.

    ![Certyfikat sieci VPN punkt lokacja sieci wirtualnej platformy Azure][img-certificate]

    Certyfikat klienta należy zainstalować na każdym komputerze, które mają sieci wirtualnej toohello tooconnect. Zaleca się tworzenia unikatowych klientów certyfikatów dla każdego komputera, które mają sieci wirtualnej toohello tooconnect. certyfikaty klienta hello tooexport, użyj certmgr.msc.

**tooupload hello głównego certyfikatu toohello klasycznego portalu Azure**

1. Hello klasycznego portalu Azure, kliknij **sieci** powitania po lewej stronie.
2. Kliknij przycisk hello sieci wirtualnej wdrożonym klastra HBase do.
3. Kliknij przycisk **certyfikaty** od góry hello.
4. Kliknij przycisk **przekazać** z hello dołu, a następnie określ plik certyfikatu głównego hello utworzonego w procedurze hello przed ostatnią. Poczekaj, aż hello certyfikat został zaimportowany.
5. Kliknij przycisk **pulpitu NAWIGACYJNEGO** u góry hello.  Witaj wirtualnych diagram przedstawia stan hello.

#### <a name="configure-your-vpn-client"></a>Konfigurowanie klienta sieci VPN
**pakiet sieci VPN klienta hello toodownload i instalacji**

1. Ze strony pulpitu NAWIGACYJNEGO hello hello sieci wirtualnej, w sekcji szybkiego dostępu powitania kliknij **pobierania hello 64-bitowego klienta VPN pakietu** lub **pobierania hello pakietu sieci VPN klienta 32-bitowego** na podstawie użytkownika wersja systemu operacyjnego stacji roboczej.
2. Kliknij przycisk **Uruchom** tooinstall hello pakietu.
3. W wierszu hello zabezpieczeń, kliknij przycisk **więcej informacji o**, a następnie kliknij przycisk **Uruchom mimo to**.
4. Kliknij przycisk **tak** dwa razy.

**tooconnect tooVPN**

1. Na pulpicie hello stacji roboczej kliknij ikonę sieci hello na pasku zadań hello. Zostanie wyświetlona połączenia sieci VPN z nazwą sieci wirtualnej.
2. Kliknij nazwę połączenia VPN hello.
3. Kliknij przycisk **Połącz**.

**Witaj tootest rozpoznawania nazw połączenia i domen sieci VPN**

* Witaj stacji roboczej, otwórz wiersz polecenia i ping powitania od nazwy podanej klastra HBase hello sufiks DNS jest myhbase.b7.internal.cloudapp.net:

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a>Instalowanie i konfigurowanie SQuirreL na stacji roboczej
**tooinstall SQuirreL**

1. Pobierz plik jar klienta hello SQuirreL SQL z [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).
2. Witaj Otwórz i uruchom plik jar. Wymaga to hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
3. Kliknij przycisk **dalej** dwa razy.
4. Określ ścieżkę, w którym masz hello uprawnienie do zapisu, a następnie kliknij przycisk **dalej**.

  > [!NOTE]
  > domyślny folder instalacji Hello znajduje się w folderze C:\Program Files\squirrel-sql 3,6 hello.  W ścieżce toothis toowrite kolejności Instalator hello musi mieć przyznane uprawnienia administratora hello. Można otworzyć wiersz polecenia jako administrator, przejdź na tooJava folder bin, a następnie uruchom:
  >
  >     Java.exe-jar [ścieżka hello plik jar SQuirreL hello]
5. Kliknij przycisk **OK** tooconfirm tworzenie hello katalog docelowy.
6. Witaj domyślne ustawienie to tooinstall hello Base i standardowe pakietów.  Kliknij przycisk **Dalej**.
7. Kliknij przycisk **dalej** dwa razy, a następnie kliknij przycisk **gotowe**.

**tooinstall hello Phoenix sterownika**

Plik jar sterownika phoenix Hello znajduje się na powitania klastra HBase. Ścieżka Hello jest podobne następujące toohello oparte na wersji hello:

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
Należy toocopy go tooyour stacji roboczej, w obszarze hello [folder instalacji SQuirreL] / lib ścieżki.  Witaj Najprostszym sposobem jest tooRDP na powitania klastra, a następnie użyj pliku kopiowanie i wklejanie (CTRL + C i CTRL + V) toocopy on tooyour stacji roboczej.

**tooadd tooSQuirreL sterownika Phoenix**

1. Otwórz klienta SQL SQuirreL ze stacji roboczej.
2. Kliknij przycisk hello **sterownika** kartę powitania po lewej stronie.
3. Z hello **sterowniki** menu, kliknij przycisk **nowego sterownika**.
4. Wprowadź hello następujących informacji:

   * **Nazwa**: Phoenix
   * **Przykładowy adres URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net
   * **Nazwa klasy**: org.apache.phoenix.jdbc.PhoenixDriver

     > [!WARNING]
     > Użytkownik małe litery w hello przykładowego adresu URL. Można użyć ich pełną dozorcy kworum w przypadku, gdy jeden z nich jest wyłączony.  nazwy hostów Hello są zookeeper0, zookeeper1 i zookeeper2.
     >
     >

     ![HDInsight HBase Phoenix SQuirreL sterownika][img-squirrel-driver]
5. Kliknij przycisk **OK**.

**toocreate klaster HBase toohello aliasu**

1. SQuirreL, kliknij hello **aliasy** kartę powitania po lewej stronie.
2. Z hello **aliasy** menu, kliknij przycisk **nowy Alias**.
3. Wprowadź hello następujących informacji:

   * **Nazwa**: hello nazwę klastra HBase hello lub dowolną nazwę preferowane.
   * **Sterownik**: Phoenix.  To musi odpowiadać nazwie sterownik hello, utworzony w poprzedniej procedurze hello.
   * **Adres URL**: hello adres URL jest kopiowana z konfiguracji sterownika. Upewnij się, że toouser małe litery.
   * **Nazwa użytkownika**: może być dowolny tekst.  Ponieważ używane połączenie z siecią VPN w tym miejscu hello nazwa użytkownika nie jest używany w ogóle.
   * **Hasło**: może być dowolny tekst.

     ![HDInsight HBase Phoenix SQuirreL sterownika][img-squirrel-alias]
4. Kliknij przycisk **testu**.
5. Kliknij przycisk **Połącz**. Po jego nawiązaniu połączenia hello, SQuirreL wygląda następująco:

    ![HBase Phoenix SQuirreL][img-squirrel]

**toorun testu**

1. Kliknij przycisk hello **SQL** karcie prawo dalej toohello **obiektów** kartę.
2. Skopiuj i Wklej hello następującego kodu:

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. Kliknij przycisk Uruchom hello.

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. Przełącz wstecz toohello **obiektów** kartę.
5. Rozwiń nazwę aliasu hello, a następnie rozwiń **tabeli**.  Zostanie wyświetlona nowa tabela hello kategorii.

## <a name="next-steps"></a>Następne kroki
W tym artykule wiesz już, jak toouse Apache Phoenix w usłudze HDInsight.  toolearn więcej, zobacz

* [Przegląd bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview]: HBase jest bazą danych Apache NoSQL typu open source opartą na platformie Hadoop, która zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą i bez struktury.
* [Udostępnianie klastrów HBase w sieci wirtualnej Azure][hdinsight-hbase-provision-vnet]: Z integracji sieci wirtualnej klastrów HBase może być wdrożone toohello sam wirtualnych sieci jako aplikacje tak aplikacje mogą komunikować się z HBase bezpośrednio.
* [Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight](hdinsight-hbase-replication.md): Dowiedz się, jak replikacji bazy danych HBase tooconfigure między dwoma centrami danych Azure.
* [Analizowanie Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight][hbase-twitter-sentiment]: Dowiedz się, jak toodo w czasie rzeczywistym [analizy wskaźniki nastrojów klientów](http://en.wikipedia.org/wiki/Sentiment_analysis) dużych danych przy użyciu bazy danych HBase w klastra usługi Hadoop w usłudze HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
