---
title: aaaCreate notesu Jupyter/IPython | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toodeploy hello notesu Jupyter/IPython na maszynie wirtualnej systemu Linux utworzone z modelu wdrażania Menedżera zasobów hello na platformie Azure."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Tworzenie maszyny Wirtualnej platformy Azure, instalowania Jupyter i uruchamiania notesu Jupyter na platformie Azure
Witaj [projektu Jupyter](http://jupyter.org), wcześniej hello [IPython projektu](http://ipython.org), udostępnia kolekcję narzędzi dla przy użyciu zaawansowanych powłok interaktywne, łączące wykonanie kodu z tworzenia hello obliczanie naukowe dokument obliczeniową na żywo. Te pliki notesu może zawierać dowolnego tekstu, matematycznymi, podaj kod, wyniki, grafiki, wideo i dowolnego typu nośnika Nowoczesna przeglądarka sieci web jest w stanie wyświetlania. Określa, czy jest całkowicie nowe tooPython i chcesz toolearn w fun, interaktywnego środowiska lub czy niektóre poważne równoległe/technicznych obliczeniowych, hello notesu Jupyter jest doskonałym wyborem.

![Zrzut ekranu](./media/jupyter-notebook/ipy-notebook-spectral.png) przy użyciu SciPy Matplotlib pakiety tooanalyze hello struktury i nagrywanie dźwięku.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Jupyter dwa sposoby: Wdrażanie niestandardowych lub Azure notesów
Platforma Azure udostępnia usługi, która służy za[szybko uruchomić przy użyciu oprogramowania Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).  Przy użyciu hello Azure notesu usługi, można łatwo uzyskać tooJupyter dostępu interfejsu dostępnej w sieci web do skalowalnych zasobów obliczeniowych przy użyciu hello zasilania środowiska Python i jego wiele bibliotek.  Ponieważ instalacja hello jest obsługiwana przez usługę hello, użytkownicy mogą otwierać tych zasobów, bez potrzeby hello administracji i konfiguracji przez użytkownika hello.

Jeśli usługa notesu hello nie działa w przypadku danego scenariusza nadal tooread tego artykułu, który będzie opisano sposób toodeploy hello notesu Jupyter w systemie Microsoft Azure przy użyciu maszyn wirtualnych systemu Linux (VM).

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Tworzenie i konfigurowanie maszyny Wirtualnej na platformie Azure
pierwszym krokiem Hello jest toocreate maszynę wirtualną (VM) działającą na platformie Azure.
Ta maszyna wirtualna jest całego systemu operacyjnego w chmurze hello i będzie służyć do uruchamiania hello notesu Jupyter. Jest w stanie uruchomionych maszyn wirtualnych zarówno systemu Linux i Windows Azure i omówimy hello ustawienia Jupyter na oba typy maszyn wirtualnych.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Utwórz Maszynę wirtualną systemu Linux i otwarcie portu dla Jupyter
Postępuj zgodnie z instrukcjami hello [tutaj] [ portal-vm-linux] toocreate maszynę wirtualną w hello *Ubuntu* dystrybucji. W tym samouczku używana Ubuntu Server 14.04 LTS. Przyjmiemy nazwy użytkownika hello *azureuser*.

Po wdraża maszyny wirtualnej hello potrzebujemy tooopen reguły zabezpieczeń na powitania sieciowej grupy zabezpieczeń.  Z hello portalu Azure, przejdź zbyt**grup zabezpieczeń sieci** i hello Otwórz kartę tooyour odpowiedniego hello grupy zabezpieczeń maszyny Wirtualnej. Należy tooadd reguły zabezpieczeń ruchu przychodzącego z hello następujące ustawienia: **TCP** dla protokołu hello  **\***  hello portu źródłowego (publicznej) i **9999** dla Witaj port docelowy (prywatny).

![Zrzut ekranu](./media/jupyter-notebook/azure-add-endpoint.png)

Znajduje się w sieciowej grupy zabezpieczeń, kliknij polecenie **interfejsów sieciowych** i hello Uwaga **publicznego adresu IP** jak będą potrzebne tooconnect tooyour maszyny Wirtualnej w hello następnego kroku.

## <a name="install-required-software-on-hello-vm"></a>Zainstaluj oprogramowanie wymagane na powitania maszyny Wirtualnej
toorun hello notesu Jupyter w naszym maszyny Wirtualnej, musi najpierw zainstalować Jupyter i jego zależności. Połącz przy użyciu ssh maszyny wirtualnej systemu linux tooyour i parę nazwy użytkownika i hasła hello wybrane, podczas tworzenia hello maszyny wirtualnej. W tym samouczku będziemy przy użyciu programu PuTTY i Połącz z systemu Windows.

### <a name="installing-jupyter-on-ubuntu"></a>Instalowanie oprogramowania Jupyter na Ubuntu
Zainstaluj platformę Anaconda — dystrybucję oprogramowania python nauki popularnych danych przy użyciu jednej z łącza hello [Analytics kontynuacja](https://www.continuum.io/downloads).  Począwszy od hello opracowywania tego dokumentu, hello poniższych łączy są hello najbardziej się toodate wersji.

#### <a name="anaconda-installs-for-linux"></a>Instaluje anaconda dla systemu Linux
<table>
  <th>Języka Python 3.4</th>
  <th>Python 2.7</th>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64-bitowy</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64-bitowy</href>
    </td>
  </tr>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32-bitowy</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32-bitowy</href>
    </td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a>Instalowanie Anaconda3 2.3.0 64-bit na Ubuntu
Na przykład jest to, jak można zainstalować na Ubuntu Anaconda

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Zrzut ekranu](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>Konfigurowanie Jupyter i przy użyciu protokołu SSL
Po zainstalowaniu potrzebujemy tootake plików konfiguracji hello toosetup obecnie dla Jupyter. Jeśli wystąpią troubles przy konfigurowaniu Jupyter mogą być przydatne toolook na powitania [dokumentacji systemem Server notesu Jupyter](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).

Dalej będziemy `cd` toohello profilu toocreate katalogu naszych certyfikatu SSL i edycję pliku konfiguracyjnego hello profilów.

W systemie Linux należy użyć hello następujące polecenia.

    cd ~/.jupyter

Użyj hello następujące polecenia toocreate hello certyfikat SSL (Linux i Windows).

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Należy pamiętać, że ponieważ podpisany certyfikat SSL, jest tworzone podczas łączenia notesu toohello przeglądarkę zapewni ostrzeżenie o zabezpieczeniach.  Długoterminowe użycia w środowisku produkcyjnym mają toouse są poprawnie podpisane certyfikatu skojarzonego z Twoją organizacją.  Ponieważ zarządzanie certyfikatami wykracza poza zakres tego pokazu hello, firma Microsoft będzie trzymaj certyfikatu z podpisem własnym tooa teraz.

Ponadto toousing certyfikatu, musisz także podać tooprotect hasło notesu przed nieautoryzowanym użyciem.  Ze względów bezpieczeństwa Jupyter używa hasła szyfrowane w pliku konfiguracji, dlatego potrzebujesz tooencrypt hasło najpierw.  Udostępnia IPython toodo narzędzie w wierszu polecenia Uruchom następujące polecenie hello.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

Wyświetli monit o hasło i potwierdzenie, a następnie będzie drukować hello hasła. Uwaga to powitania po kroku.

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

Następnie zostanie Edytuj plik konfiguracyjny hello profil, który jest `jupyter_notebook_config.py` pliku w katalogu hello w.  Należy pamiętać, że ten plik nie istnieje — wystarczy utworzyć hello sytuacji.  Ten plik zawiera liczbę pól i domyślnie wszystkie są oznaczone jako komentarz.  Ten plik można otworzyć za pomocą dowolnego edytora tekstów, z Twoim preferencjom i upewnij się, że ma co najmniej hello po zawartości. **Należy się c.NotebookApp.password hello tooreplace w pliku konfiguracyjnym hello z sha1 hello z poprzedniego kroku hello**.

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a>Uruchom hello notesu Jupyter
W tym momencie mamy hello gotowe toostart notesu Jupyter. toodo, przejdź do katalogu toohello notesów toostore i zacząć powitania serwera notesu Jupyter z hello następujące polecenia.

    /anaconda3/bin/jupyter-notebook

Możesz teraz powinno być możliwe tooaccess notesu Jupyter pod adresem hello `https://[PUBLIC-IP-ADDRESS]:9999`.

Przy pierwszym uzyskaniu dostępu notesu strony logowania hello monituje o podanie hasła. I po zalogowaniu zostanie wyświetlona "Pulpitu nawigacyjnego notesu Jupyter," hello czyli Centrum kontrolne dla wszystkich operacji notesu.  Na tej stronie można tworzyć nowych notesów i otworzyć istniejące.

![Zrzut ekranu](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a>Przy użyciu hello notesu Jupyter
Jeśli klikniesz przycisk hello **nowy** przycisku, zobaczysz powitania po strona początkowa.

![Zrzut ekranu](./media/jupyter-notebook/jupyter-untitled-notebook.png)

obszar Hello oznaczonych `In []:` monit jest hello obszaru wprowadzania, w tym miejscu można wpisać prawidłowy kod języka Python i wykona naciśnięcie `Shift-Enter` lub kliknij ikonę "Play" hello (hello wskazująca w prawo trójkąt hello w pasku narzędzi).

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>Zaawansowanego modelu: obliczeniowa dokumentów za pomocą multimedialną na żywo
notesu Hello, sama powinien uznać tooanyone bardzo fizycznych, który został użyty, Python i Edytor tekstów, ponieważ znajduje się w pewnym sensie kombinację obu: można wykonywać bloki kodu języka Python, ale można również zarejestrować uwagi i innych tekstu, zmieniając hello stylu komórki 'Code' zbyt "Ma rkdown"przy użyciu menu rozwijanego hello na pasku narzędzi.

Jupyter jest znacznie więcej niż edytora tekstów, który zezwala na łączenie obliczeń i rozbudowane nośnika (tekstu, grafiki, wideo i praktycznie coś, co umożliwia wyświetlanie Nowoczesna przeglądarka sieci web). Można łączyć, tekst, kod, klipów wideo i inne!

![Zrzut ekranu](./media/jupyter-notebook/jupyter-editing-experience.png)

I o sile hello wiele bibliotek znakomity języka Python dla naukowo obliczeniowych w hello następującego zrzutu ekranu, prostego obliczenia można wykonywać za pomocą hello sam do jej obsługi ułatwiają jako analizę złożoną siecią wszystko w jednym środowisku.

Ten model mieszania hello możliwości hello nowoczesnych witryn sieci web z obliczeń na żywo oferuje wiele możliwości i doskonale nadaje się do chmury hello; Witaj notesu może być używany:

* Jako toorecord obliczeniową Notatnik poznawcze działają w problem.
* powoduje tooshare współpracownikom "na żywo" formularza obliczeniową lub pisemnie formatów (HTML, plików PDF).
* toodistribute obecny materiałów nauczania na żywo obejmujących obliczeń, więc studentów można natychmiast eksperymentować hello rzeczywisty kod, zmodyfikuj go i ponownie wykonaj interaktywnie.
* tooprovide "wykonywalny dokumenty", udostępniające hello wyników badań w taki sposób, który można od razu można odtworzyć, zweryfikowane i rozszerzać przez innych użytkowników.
* Jako platforma do współpracy obliczeniowych: wiele użytkownicy mogą zalogować toothe sam notesu serwera tooshare obliczeniową sesję na żywo.

Jeśli przejdziesz kodu źródłowego IPython toohello [repozytorium][repository], można znaleźć cały katalog wraz z przykładami notesu, które można pobrać i eksperymentować na maszynie Wirtualnej własne Azure Jupyter.  Wystarczy pobrać hello `.ipynb` pliki z hello lokacji i przekazać je na pulpit nawigacyjny hello notesu maszyny Wirtualnej platformy Azure (lub pobrać je bezpośrednio do hello maszyny Wirtualnej).

## <a name="conclusion"></a>Podsumowanie
Hello notesu Jupyter zapewnia zaawansowany interfejs do uzyskiwania dostępu do interaktywnego zasilania hello ekosystemu języka Python hello na platformie Azure.  Obejmuje ona szeroką gamę przypadków użycia w tym proste eksploracji i Nauka języka Python, analizy danych i wizualizacji, symulacji oraz przetwarzania równoległego. Hello wynikowy notesu dokumenty zawierają pełny rekord hello obliczenia, które są wykonywane i może być współużytkowane z innymi użytkownikami Jupyter.  Witaj notesu Jupyter mogą być używane jako lokalnych aplikacji, ale najlepiej nadaje się do wdrożenia w chmurze na platformie Azure

Witaj podstawowych funkcji oprogramowania Jupyter są również dostępne w programie Visual Studio za pomocą [narzędzi Python Tools for Visual Studio] [ Python Tools for Visual Studio] (PTVS). PTVS to bezpłatny i wtyczki firmy Microsoft, które włącza Visual Studio do zaawansowanego środowiska programowania Python obejmuje Zaawansowany edytor z funkcji IntelliSense, debugowania, profilowania i równoległych open source obliczeniowych integracji.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Python](/develop/python/).

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
