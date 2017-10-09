---
title: aaaInstall MongoDB na maszynie Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tworzone tooinstall bazy danych MongoDB na maszynie Wirtualnej platformy Azure, system Windows Server 2012 R2 z modelu wdrażania usługi Resource Manager hello."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a>Instalowanie i Konfigurowanie bazy danych MongoDB na maszynie Wirtualnej systemu Windows na platformie Azure
[Bazy danych MongoDB](http://www.mongodb.org) jest popularnych open source, wysokiej wydajności bazę danych NoSQL. W tym artykule opisano sposób instalowania i konfigurowania bazy danych MongoDB na maszynie wirtualnej systemu Windows Server 2012 R2 (VM) na platformie Azure. Możesz również [zainstalować bazy danych MongoDB na Maszynę wirtualną systemu Linux na platformie Azure](../linux/install-mongodb.md).

## <a name="prerequisites"></a>Wymagania wstępne
Przed zainstalowaniem i skonfigurowaniem bazy danych MongoDB, którego należy toocreate Maszynę wirtualną, najlepiej jest dodać tooit dysku danych. Zobacz hello następujące artykuły toocreate maszyny Wirtualnej, a następnie Dodaj dysk z danymi:

* Tworzenie maszyny Wirtualnej systemu Windows Server przy użyciu [hello portalu Azure](quick-create-portal.md) lub [programu Azure PowerShell](quick-create-powershell.md).
* Dołączanie danych dysku tooa maszyny Wirtualnej systemu Windows Server przy użyciu [hello portalu Azure](attach-managed-disk-portal.md) lub [programu Azure PowerShell](attach-disk-ps.md).

toobegin Instalowanie i Konfigurowanie bazy danych MongoDB, [logowania tooyour maszyny Wirtualnej systemu Windows Server](connect-logon.md) przy użyciu pulpitu zdalnego.

## <a name="install-mongodb"></a>Instalowanie bazy danych MongoDB
> [!IMPORTANT]
> Funkcje zabezpieczeń bazy danych MongoDB, takich jak uwierzytelnianie i powiązanie adresu IP, nie są domyślnie włączone. Funkcje zabezpieczeń powinny być włączone przed wdrożeniem w środowisku produkcyjnym tooa bazy danych MongoDB. Aby uzyskać więcej informacji, zobacz [MongoDB zabezpieczeń i uwierzytelniania](http://www.mongodb.org/display/DOCS/Security+and+Authentication).


1. Po nawiązaniu połączenia tooyour maszyny Wirtualnej przy użyciu pulpitu zdalnego, Otwórz program Internet Explorer z hello **Start** menu na powitania maszyny Wirtualnej.
2. Wybierz **Użyj zalecanych ustawień zabezpieczeń, prywatności i zgodności** gdy program Internet Explorer najpierw otwiera i kliknij przycisk **OK**.
3. Konfiguracja zwiększonych zabezpieczeń programu Internet Explorer jest domyślnie włączona. Dodaj hello bazy danych MongoDB witryny sieci Web toohello listy dozwolonych witryn:
   
   * Wybierz hello **narzędzia** ikonę w prawym górnym rogu hello.
   * W **Opcje internetowe**, wybierz pozycję hello **zabezpieczeń** , a następnie wybierz hello **Zaufane witryny** ikony.
   * Kliknij przycisk hello **witryny** przycisku. Dodaj *https://\*. mongodb.org* toohello listy zaufanych witryn i hello następnie zamknij okno dialogowe.
     
     ![Konfigurowanie ustawień zabezpieczeń programu Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. Przeglądaj toohello [MongoDB — pliki do pobrania](http://www.mongodb.org/downloads) strony (http://www.mongodb.org/downloads).
5. W razie potrzeby wybierz hello **serwera społeczności** edition i hello a następnie wybierz pozycję najnowsze bieżącej stabilna wersji dla systemu Windows Server 2008 R2 w wersji 64-bitowej lub nowszym. toodownload hello Instalatora, kliknij przycisk **pobierania (msi)**.
   
    ![Pobierz Instalator bazy danych MongoDB](./media/install-mongodb/download-mongodb.png)
   
    Uruchom Instalatora hello, po zakończeniu pobierania hello.
6. Przeczytaj i zaakceptuj umowę licencyjną hello. Po wyświetleniu monitu wybierz **Complete** zainstalować.
7. Na ekranie końcowym powitania kliknij **zainstalować**.

## <a name="configure-hello-vm-and-mongodb"></a>Skonfiguruj hello maszyny Wirtualnej i bazy danych MongoDB
1. Witaj zmienne ścieżek nie są aktualizowane przez Instalatora bazy danych MongoDB hello. Bez hello bazy danych MongoDB `bin` lokalizacji w zmiennej path, należy toospecify hello pełną ścieżkę każdym użyciu wykonywalny bazy danych MongoDB. zmienna ścieżki tooadd hello lokalizacji tooyour:
   
   * Kliknij prawym przyciskiem myszy hello **Start** menu, a następnie wybierz **systemu**.
   * Kliknij przycisk **Zaawansowane ustawienia systemu**, a następnie kliknij przycisk **zmiennych środowiskowych**.
   * W obszarze **zmienne systemowe**, wybierz pozycję **ścieżki**, a następnie kliknij przycisk **Edytuj**.
     
     ![Skonfiguruj zmienne ŚCIEŻEK](./media/install-mongodb/configure-path-variables.png)
     
     Dodaj hello tooyour ścieżka bazy danych MongoDB `bin` folderu. Bazy danych MongoDB zazwyczaj jest zainstalowany w *C:\Program Files\MongoDB*. Sprawdź, czy ścieżka instalacji hello na maszynie Wirtualnej. Witaj poniższy przykład umożliwia dodanie hello domyślnej bazy danych MongoDB instalacji lokalizacji toohello `PATH` zmienną:
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > Należy się tooadd hello wiodącego średnika (`;`) tooindicate dodajesz tooyour lokalizacji `PATH` zmiennej.

2. Tworzenie bazy danych MongoDB katalogi danych i dziennika na dysku danych. Z hello **Start** menu, wybierz opcję **wiersza polecenia**. Następujące przykłady Hello tworzenia katalogów hello na dysku F:
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. Wystąpienie bazy danych MongoDB zaczynać się hello następujące polecenia, dostosowywania hello ścieżki tooyour danych i dziennika odpowiednio katalogi:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    Może potrwać kilka minut dla bazy danych MongoDB tooallocate hello plików dziennika i rozpocząć nasłuchiwania dla połączenia. Wszystkie komunikaty dziennika są ukierunkowanej toohello *F:\MongoLogs\mongolog.log* pliku jako `mongod.exe` server uruchamia i przydziela plików dziennika.
   
   > [!NOTE]
   > Wiersz polecenia Hello pozostaje koncentruje się na to zadanie uruchomionej wystąpienia bazy danych MongoDB. Pozostaw hello wiersza polecenia okna otwarte toocontinue uruchamiania bazy danych MongoDB. Ewentualnie można zainstalować bazy danych MongoDB jako usługa, zgodnie z opisem w następnym kroku hello.

4. W przypadku bardziej niezawodne środowisko bazy danych MongoDB, zainstaluj hello `mongod.exe` jako usługa. Tworzenie usługi oznacza, że nie ma potrzeby tooleave wiersz polecenia z każdym toouse bazy danych MongoDB. Tworzenie usługi hello następujące odpowiednio dostosowywania hello ścieżki tooyour danych i dziennika katalogów:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    Witaj poprzednie polecenie tworzy usługę o nazwie bazy danych MongoDB, opis "BD o Mongo". określono też Hello następujące parametry:
   
   * Witaj `--dbpath` opcji określa lokalizację hello hello danych katalogu.
   * Witaj `--logpath` opcja musi być używane toospecify pliku dziennika, ponieważ hello uruchomionej usługi nie ma danych wyjściowych toodisplay okna poleceń.
   * Witaj `--logappend` opcja określa, czy ponowne uruchomienie usługi hello powoduje, że dane wyjściowe tooappend toohello istniejący plik dziennika.
   
   toostart hello usługi bazy danych MongoDB, uruchom następujące polecenie hello:
   
    ```
    net start MongoDB
    ```
   
    Aby uzyskać więcej informacji o tworzeniu hello usługi bazy danych MongoDB, zobacz [skonfigurować usługę systemu Windows dla bazy danych MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).

## <a name="test-hello-mongodb-instance"></a>Wystąpienie bazy danych MongoDB hello testu
Z bazy danych MongoDB, uruchomione jako jedno wystąpienie lub zainstalowany jako usługa można teraz rozpocząć tworzenie i korzystanie z baz danych. toostart hello powłoki administracyjne bazy danych MongoDB, otworzyć inne okno wiersza polecenia z hello **Start** menu, a następnie wprowadź następujące polecenie hello:

```
mongo  
```

Możesz wyświetlić listę hello baz danych, hello `db` polecenia. Wstaw dowolne dane w następujący sposób:

```
db.foo.insert( { a : 1 } )
```

Wyszukiwanie danych w następujący sposób:

```
db.foo.find()
```

Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

Zakończ hello `mongo` konsoli w następujący sposób:

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a>Konfigurowanie zapory i reguł sieciowej grupy zabezpieczeń
Teraz, bazy danych MongoDB jest zainstalowana i uruchomiona, należy otworzyć port w Zaporze systemu Windows, aby mogli zdalnie łączyć z tooMongoDB. toocreate nowy port TCP tooallow reguły dla ruchu przychodzącego 27017, otwórz administracyjny wiersz środowiska PowerShell i wpisz następujące polecenie hello:

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

Można również utworzyć reguły hello przy użyciu hello **Zapora systemu Windows z zabezpieczeniami zaawansowanymi** graficzne narzędzie do zarządzania. Utwórz nowy port TCP tooallow reguły dla ruchu przychodzącego 27017.

W razie potrzeby utwórz grupę zabezpieczeń sieci reguły tooallow dostępu tooMongoDB z poza hello istniejącą podsieć sieci wirtualnej platformy Azure. Można utworzyć hello reguł sieciowej grupy zabezpieczeń przy użyciu hello [portalu Azure](nsg-quickstart-portal.md) lub [programu Azure PowerShell](nsg-quickstart-powershell.md). Podobnie jak w przypadku reguł zapory systemu Windows hello, Zezwalaj na interfejs sieci wirtualnej toohello port 27017 TCP maszyny wirtualnej bazy danych MongoDB.

> [!NOTE]
> TCP port 27017 hello domyślny port jest używany przez bazy danych MongoDB. Tego portu można zmienić za pomocą hello `--port` parametru podczas uruchamiania `mongod.exe` ręcznie lub z poziomu usługi. W przypadku zmiany portu hello, upewnij się, że tooupdate hello zapory systemu Windows i grupy zabezpieczeń sieci reguły w poprzednich krokach hello.


## <a name="next-steps"></a>Następne kroki
W tym samouczku można przedstawiono sposób tooinstall i skonfigurować bazy danych MongoDB na maszynie Wirtualnej systemu Windows. Można uzyskać dostęp bazy danych MongoDB na maszynie Wirtualnej systemu Windows, w następujących hello zaawansowanych tematów w hello [dokumentacją usługi MongoDB](https://docs.mongodb.com/manual/).

