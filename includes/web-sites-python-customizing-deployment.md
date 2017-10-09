Platforma Azure określi, że aplikacja używa języka Python, **jeśli są spełnione oba te warunki**:

* Plik Requirements.txt znajduje się w folderze głównym hello
* Każdy plik .py w folderze głównym hello lub pliku runtime.txt, który określa języka python

W takim przypadku hello użyje skryptu wdrażania języka Python, który wykonuje standardową synchronizację plików, a także dodatkowe operacje języka Python, takie jak hello:

* Automatyczne zarządzanie środowiskiem wirtualnym
* Instalacja pakietów wymienionych w pliku requirements.txt przy użyciu adresu pip
* Tworzenie odpowiedniego pliku web.config hello oparte na powitania wybranej wersji języka Python.
* Zbieranie plików statycznych dla aplikacji Django

Można kontrolować niektóre aspekty domyślnych kroków wdrażania hello bez konieczności toocustomize hello skryptu.

Jeśli chcesz tooskip wszystkie kroki wdrażania właściwe dla języka Python, możesz utworzyć ten pusty plik:

    \.skipPythonDeployment

Aby uzyskać większą kontrolę nad wdrażaniem można zastąpić hello domyślny skrypt wdrożenia, tworząc hello następujące pliki:

    \.deployment
    \deploy.cmd

Można użyć hello [interfejsu wiersza polecenia platformy Azure] [ Azure command-line interface] toocreate hello plików.  Użyj tego polecenia w folderze projektu:

    azure site deploymentscript --python

Jeśli te pliki nie istnieją, platforma Azure tworzy tymczasowy skrypt wdrażania i uruchamia go.  Jest identyczne toohello został utworzony za pomocą polecenia hello powyżej.

[Azure command-line interface]: http://azure.microsoft.com/downloads/
