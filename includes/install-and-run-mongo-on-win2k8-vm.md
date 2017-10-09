Wykonaj te kroki tooinstall i uruchomić bazy danych MongoDB na maszynie wirtualnej z systemem Windows Server.

> [!IMPORTANT]
> Funkcje zabezpieczeń bazy danych MongoDB, takich jak uwierzytelnianie i powiązanie adresu IP, nie są domyślnie włączone. Funkcje zabezpieczeń powinny być włączone przed wdrożeniem w środowisku produkcyjnym tooa bazy danych MongoDB.  Aby uzyskać więcej informacji, zobacz [zabezpieczeń i uwierzytelniania](http://www.mongodb.org/display/DOCS/Security+and+Authentication).
>
>

1. Po nawiązaniu połączenia toohello maszyny wirtualnej za pomocą pulpitu zdalnego, Otwórz program Internet Explorer z hello **Start** menu hello maszyny wirtualnej.
2. Wybierz hello **narzędzia** przycisk w prawym górnym rogu hello.  W **Opcje internetowe**, wybierz pozycję hello **zabezpieczeń** , a następnie wybierz hello **Zaufane witryny** ikonę, a na koniec kliknij hello **witryny** przycisk. Dodaj *https://\*. mongodb.org* toohello listy zaufanych witryn.
3. Przejdź za[pobiera — bazy danych MongoDB](https://www.mongodb.com/download-center#community).
4. Znajdź hello **bieżącej wersji stabilnej** z **Community Server**, wybierz pozycję hello najnowszych **64-bitowych** wersji w kolumnie Windows hello. Pobierz, a następnie uruchom Instalatora MSI hello.
5. Bazy danych MongoDB zazwyczaj jest zainstalowany w C:\Program Files\MongoDB. Wyszukiwanie zmiennych środowiskowych na pulpicie hello i dodać zmiennej PATH toohello ścieżki plików binarnych hello bazy danych MongoDB. Może na przykład znaleźć plików binarnych hello na C:\Program Files\MongoDB\Server\3.4\bin na tym komputerze.
6. Tworzenie katalogów danych i dziennika bazy danych MongoDB hello dysku danych (takich jak dysk **F:**) utworzone w poprzednich krokach hello. Z **Start**, wybierz pozycję **wiersza polecenia** tooopen okno wiersza polecenia.  Wpisz:

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. toorun hello bazy danych, uruchom:

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    Wszystkie komunikaty dziennika są ukierunkowanej toohello *F:\MongoLogs\mongolog.log* plików serwera mongod.exe rozpoczęciu i preallocates plików dziennika. Może potrwać kilka minut dla bazy danych MongoDB toopreallocate hello plików dziennika i rozpocząć nasłuchiwania dla połączenia. Wiersz polecenia Hello pozostaje koncentruje się na to zadanie uruchomionej wystąpienia bazy danych MongoDB.
8. toostart hello powłoki administracyjne bazy danych MongoDB, otwiera inne okno polecenia z **Start** i hello wpisz następujące polecenia:

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    Witaj baza danych została utworzona przez hello insert.
9. Alternatywnie możesz zainstalować mongod.exe jako usługa:

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    Zainstalowano usługę o nazwie bazy danych MongoDB z opisem "BD o Mongo". Witaj `--logpath` opcja musi być używane toospecify pliku dziennika, od hello usługi nie ma danych wyjściowych toodisplay okna poleceń.  Witaj `--logappend` opcja określa, czy ponowne uruchomienie usługi hello powoduje, że dane wyjściowe tooappend toohello istniejący plik dziennika.  Witaj `--dbpath` opcji określa lokalizację hello hello danych katalogu. Aby bardziej związane z usługą opcji wiersza polecenia, zobacz [opcje wiersza polecenia związane z usługą][MongoWindowsSvcOptions].

    toostart hello usługi, uruchom to polecenie:

        C:\> net start MongoDB
10. Bazy danych MongoDB jest zainstalowana i uruchomiona, należy tooopen port w Zaporze systemu Windows można zdalnie więc połączenie tooMongoDB.  Z hello **Start** menu, wybierz opcję **narzędzia administracyjne** , a następnie **Zapora systemu Windows z zabezpieczeniami zaawansowanymi**.
11. () w okienku po lewej stronie powitania, wybierz **reguły ruchu przychodzącego**.  W hello **akcje** okienku na powitania po prawej, wybierz opcję **nową regułę...** .

    ![Zapora systemu Windows][Image1]

    (b) w hello **Kreatora nowej reguły przychodzącej**, wybierz pozycję **portu** , a następnie kliknij przycisk **dalej**.

    ![Zapora systemu Windows][Image2]

    c) wybierz **TCP** , a następnie **określone porty lokalne**.  Określ port "27017" (port domyślny hello nasłuchuje bazy danych MongoDB), a następnie kliknij przycisk **dalej**.

    ![Zapora systemu Windows][Image3]

    d) wybierz **przyłączenia hello** i kliknij przycisk **dalej**.

    ![Zapora systemu Windows][Image4]

    e) kliknij **dalej** ponownie.

    ![Zapora systemu Windows][Image5]

    f) określ nazwę reguły hello, takie jak "MongoPort", a następnie kliknij przycisk **Zakończ**.

    ![Zapora systemu Windows][Image6]

12. Jeśli podczas tworzenia maszyny wirtualnej hello nie konfigurowania punktu końcowego dla bazy danych MongoDB, możesz to zrobić teraz. Wymagane zarówno hello regułę zapory i hello punktu końcowego toobe stanie tooconnect tooMongoDB zdalnie.

  W portalu Azure hello, kliknij przycisk **maszyn wirtualnych (klasyczne)**, kliknij nazwę hello nowej maszyny wirtualnej, a następnie kliknij przycisk **punkty końcowe**.

    ![Punkty końcowe][Image7]

13. Kliknij pozycję **Dodaj**.

14. Dodawanie punktu końcowego o nazwie "Mongo" protokołu **TCP**, a oba **publicznego** i **prywatnej** porty zestaw zbyt "27017". Otwierania tego portu umożliwia zdalny dostęp do toobe bazy danych MongoDB.

    ![Punkty końcowe][Image9]

> [!NOTE]
> Hello port 27017 hello domyślny port jest używany przez bazy danych MongoDB. Ten port domyślny można zmienić, określając hello `--port` parametru podczas uruchamiania serwera mongod.exe hello. Upewnij się, że toogive hello tego samego numeru portu w zaporze hello i hello punktu końcowego "Mongo" w hello poprzedzających instrukcji.
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
