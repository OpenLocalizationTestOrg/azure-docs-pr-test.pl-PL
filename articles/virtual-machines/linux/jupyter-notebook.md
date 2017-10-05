---
title: Tworzenie notesu Jupyter/IPython | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak wdrożyć notesu Jupyter/IPython na maszynie wirtualnej systemu Linux utworzone za pomocą modelu wdrażania Menedżera zasobów na platformie Azure."
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
ms.openlocfilehash: b5940190822cd5c5b78ea0e8f5c8695608d351d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Tworzenie maszyny Wirtualnej platformy Azure, instalowania Jupyter i uruchamiania notesu Jupyter na platformie Azure
[Projektu Jupyter](http://jupyter.org), wcześniej [projektu IPython](http://ipython.org), udostępnia kolekcję narzędzi dla obliczanie naukowe przy użyciu zaawansowanych powłok interaktywne, łączące wykonanie kodu z tworzeniem na żywo dokument obliczeniową. Te pliki notesu może zawierać dowolnego tekstu, matematycznymi, podaj kod, wyniki, grafiki, wideo i dowolnego typu nośnika Nowoczesna przeglądarka sieci web jest w stanie wyświetlania. Czy można całkowicie nowych użytkowników programu Python i Dowiedz się więcej w środowisku przyjemne, interakcyjnego lub czy niektóre poważne przetwarzanie równoległe/technical notesu Jupyter jest doskonałym wyborem.

![Zrzut ekranu](./media/jupyter-notebook/ipy-notebook-spectral.png) pakietów przy użyciu SciPy i Matplotlib do analizowania struktury nagrywanie dźwięku.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Jupyter dwa sposoby: Wdrażanie niestandardowych lub Azure notesów
Platforma Azure udostępnia usługi, która umożliwia [szybko uruchomić przy użyciu oprogramowania Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).  Za pomocą usługi Azure notesu, można łatwo uzyskać dostęp do interfejsu dostępnej w sieci web firmy Jupyter skalowalnych zasobów obliczeniowych dzięki możliwościom języka Python i wiele bibliotek.  Ponieważ instalacja jest obsługiwane przez usługę, użytkownicy można uzyskiwać dostęp do tych zasobów, bez konieczności zarządzania i konfiguracji przez użytkownika.

Jeśli usługa notesu nie działa w przypadku danego scenariusza nadal przeczytaj ten artykuł, który będzie opisano sposób wdrażania notesu Jupyter w systemie Microsoft Azure przy użyciu maszyn wirtualnych systemu Linux (VM).

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Tworzenie i konfigurowanie maszyny Wirtualnej na platformie Azure
Pierwszym krokiem jest utworzenie maszyny wirtualnej (VM) działających na platformie Azure.
Ta maszyna wirtualna jest całego systemu operacyjnego w chmurze i będzie służyć do uruchamiania notesu Jupyter. Jest w stanie uruchomionych maszyn wirtualnych zarówno systemu Linux i Windows Azure i omówimy Instalatora oprogramowania Jupyter na oba typy maszyn wirtualnych.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Utwórz Maszynę wirtualną systemu Linux i otwarcie portu dla Jupyter
Postępuj zgodnie z instrukcjami [tutaj] [ portal-vm-linux] do utworzenia maszyny wirtualnej z *Ubuntu* dystrybucji. W tym samouczku używana Ubuntu Server 14.04 LTS. Przyjmiemy nazwy użytkownika *azureuser*.

Po wdraża maszyny wirtualnej należy otworzyć reguły zabezpieczeń dla grupy zabezpieczeń sieci.  W portalu Azure, przejdź do **grup zabezpieczeń sieci** , a następnie otwórz kartę dla grupy zabezpieczeń odpowiadający maszyny Wirtualnej. Należy dodać reguły zabezpieczeń ruchu przychodzącego z następującymi ustawieniami: **TCP** protokołu,  **\***  dla portu źródłowego (publicznej) i **9999** dla port docelowy (prywatny).

![Zrzut ekranu](./media/jupyter-notebook/azure-add-endpoint.png)

Znajduje się w sieciowej grupy zabezpieczeń, kliknij polecenie **interfejsów sieciowych** i zanotuj **publicznego adresu IP** , ponieważ jest ono potrzebne do nawiązania połączenia z maszyną Wirtualną w następnym kroku.

## <a name="install-required-software-on-the-vm"></a>Zainstaluj w maszynie Wirtualnej wymaganego oprogramowania
Aby uruchomić notesu Jupyter w naszym maszyny Wirtualnej, możemy najpierw zainstalować Jupyter i jego zależności. Nawiązywanie połączenia z systemem linux maszynę wirtualną przy użyciu ssh i parą nazwy użytkownika i hasła, należy wybrać podczas tworzenia maszyny wirtualnej. W tym samouczku będziemy przy użyciu programu PuTTY i Połącz z systemu Windows.

### <a name="installing-jupyter-on-ubuntu"></a>Instalowanie oprogramowania Jupyter na Ubuntu
Zainstaluj platformę Anaconda — dystrybucję oprogramowania python nauki popularnych danych przy użyciu jednej z łącza z [Analytics kontynuacja](https://www.continuum.io/downloads).  Przeprowadzonych podczas opracowywania tego dokumentu poniższych łączy są najbardziej aktualne wersje daty.

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

    # Update Jupyter to the latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Zrzut ekranu](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>Konfigurowanie Jupyter i przy użyciu protokołu SSL
Po zainstalowaniu musimy Poświęć chwilę, aby skonfigurować pliki konfiguracji dla Jupyter. W przypadku napotkania troubles przy konfigurowaniu Jupyter mogą być pomocne dla przyjrzeć się [dokumentacji systemem Server notesu Jupyter](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).

Dalej będziemy `cd` do katalogu profilu można tworzyć naszych certyfikatu SSL i edytować plik konfiguracji profilów.

W systemie Linux należy użyć następującego polecenia.

    cd ~/.jupyter

Użyj następującego polecenia, aby utworzyć certyfikat SSL (Linux i Windows).

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Należy pamiętać, że ponieważ podpisany certyfikat SSL, jest tworzone podczas nawiązywania połączenia z notesu przeglądarki zostaną wyświetlone ostrzeżenie o zabezpieczeniach.  Długoterminowego użycia w środowisku produkcyjnym można użyć certyfikatu są poprawnie podpisane skojarzonego z Twoją organizacją.  Ponieważ zarządzanie certyfikatami jest poza zakres tego pokazu, firma Microsoft będzie osadzania certyfikatu z podpisem własnym teraz.

Oprócz używa certyfikatu, musisz także podać hasło, aby chronić notesu przed nieautoryzowanym użyciem.  Ze względów bezpieczeństwa Jupyter używa hasła szyfrowane w jego pliku konfiguracji, musisz najpierw szyfrowania hasła.  IPython udostępnia narzędzia do tego; w wierszu polecenia Uruchom następujące polecenie.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

Wyświetli monit o hasło i potwierdzenie, a następnie będzie drukować hasło. Uwaga to następny krok.

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

Następnie zostanie Edytuj plik konfiguracyjny ten profil, który jest `jupyter_notebook_config.py` pliku w znajdują się w katalogu.  Należy pamiętać, że ten plik nie istnieje — wystarczy utworzyć sytuacji.  Ten plik zawiera liczbę pól i domyślnie wszystkie są oznaczone jako komentarz.  Ten plik można otworzyć za pomocą dowolnego edytora tekstów, z Twoim preferencjom i należy upewnić się, że ma co najmniej następującą zawartość. **Pamiętaj zastąpić c.NotebookApp.password w pliku config sha1 z poprzedniego kroku**.

    c = get_config()

    # You must give the path to the certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-the-jupyter-notebook"></a>Uruchom notesu Jupyter
W tym momencie możemy rozpocząć notesu Jupyter. Aby to zrobić, przejdź do katalogu, który chcesz przechowywać notesów w i uruchomić serwera notesu Jupyter przy użyciu następującego polecenia.

    /anaconda3/bin/jupyter-notebook

Teraz powinien mieć możliwość dostępu notesu Jupyter pod adresem `https://[PUBLIC-IP-ADDRESS]:9999`.

Przy pierwszym uzyskaniu dostępu notesu strony logowania monituje o podanie hasła. I po zalogowaniu zostanie wyświetlona "Jupyter Notebook pulpitu nawigacyjnego", który jest Centrum kontrolne dla wszystkich operacji notesu.  Na tej stronie można tworzyć nowych notesów i otworzyć istniejące.

![Zrzut ekranu](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a>Za pomocą notesu Jupyter
Jeśli klikniesz przycisk **nowy** przycisku, zostanie wyświetlona następująca strona otwierania.

![Zrzut ekranu](./media/jupyter-notebook/jupyter-untitled-notebook.png)

Obszar oznaczonych `In []:` monit jest pole wejściowe, w tym miejscu można wpisać prawidłowy kod języka Python i wykona naciśnięcie `Shift-Enter` lub kliknij ikonę "Play" (wskazująca w prawo trójkąt na pasku narzędzi).

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>Zaawansowanego modelu: obliczeniowa dokumentów za pomocą multimedialną na żywo
Sam notesu powinien możesz bardzo fizycznych dla każdego, kto został użyty, Python i Edytor tekstów, ponieważ znajduje się w pewnym sensie kombinację obu: można wykonywać bloki kodu języka Python, ale można również zarejestrować zmieniając stylu komórki z "Code" do "Markdo uwagi i inny tekst dół"przy użyciu menu rozwijanego na pasku narzędzi.

Jupyter jest znacznie więcej niż edytora tekstów, który zezwala na łączenie obliczeń i rozbudowane nośnika (tekstu, grafiki, wideo i praktycznie coś, co umożliwia wyświetlanie Nowoczesna przeglądarka sieci web). Można łączyć, tekst, kod, klipów wideo i inne!

![Zrzut ekranu](./media/jupyter-notebook/jupyter-editing-experience.png)

I dzięki możliwościom języka Python wiele znakomity biblioteki naukowo komputerów na poniższym zrzucie ekranu prostego obliczenia można wykonywać za pomocą tego samego łatwość jako analizy złożoną siecią, wszystko w jednym środowisku.

Ten model mieszania zasilania nowoczesnych witryn sieci web z obliczeń na żywo oferuje wiele możliwości i doskonale nadaje się do chmury; można użyć notesu:

* Jako obliczeniową Notatnik, aby zarejestrować poznawcze działają w problem.
* Aby udostępnić wyniki swojemu współpracowników, w postaci obliczeniową "live" lub w pisemnie formatów (HTML, plików PDF).
* Do rozpowszechniania i prezentowanie na żywo nauczania materiały, które obejmują obliczeń, więc studentów można natychmiast eksperymentować rzeczywisty kod zmodyfikuj ją i ponownie wykonaj interaktywnie.
* Aby zapewnić "wykonywalny dokumenty", udostępniające wyników badań w taki sposób, który można natychmiast odtworzyć, zweryfikowane i rozszerzać przez innych użytkowników.
* Jako platforma do współpracy obliczeniowych: wiele użytkownicy mogą zalogować się do tego samego serwera notesu, aby udostępnić obliczeniową sesji na żywo.

Jeśli przejdziesz do kodu źródłowego IPython [repozytorium][repository], można znaleźć cały katalog wraz z przykładami notesu, które można pobrać i eksperymentować na maszynie Wirtualnej własne Azure Jupyter.  Wystarczy pobrać `.ipynb` plików z lokacji i przekazać je na pulpicie nawigacyjnym notesu maszyny Wirtualnej platformy Azure (lub pobrać je bezpośrednio do maszyny Wirtualnej).

## <a name="conclusion"></a>Podsumowanie
Notesu Jupyter zapewnia zaawansowany interfejs do uzyskiwania dostępu do interaktywnego zasilania ekosystemu języka Python na platformie Azure.  Obejmuje ona szeroką gamę przypadków użycia w tym proste eksploracji i Nauka języka Python, analizy danych i wizualizacji, symulacji oraz przetwarzania równoległego. Wynikowa dokumenty notesu zawierają pełny rekord obliczeń, które są wykonywane i może być współużytkowane z innymi użytkownikami Jupyter.  Notesu Jupyter mogą być używane jako lokalnych aplikacji, ale najlepiej nadaje się do wdrożenia w chmurze na platformie Azure

Są także dostępne w programie Visual Studio za pomocą podstawowych funkcji oprogramowania Jupyter [narzędzi Python Tools for Visual Studio] [ Python Tools for Visual Studio] (PTVS). PTVS to bezpłatny i wtyczki firmy Microsoft, które włącza Visual Studio do zaawansowanego środowiska programowania Python obejmuje Zaawansowany edytor z funkcji IntelliSense, debugowania, profilowania i równoległych open source obliczeniowych integracji.

## <a name="next-steps"></a>Następne kroki
Więcej informacji możesz znaleźć w [Centrum deweloperów języka Python](/develop/python/).

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
