---
title: "Języki maszyny wirtualnej nauki danych na platformie Azure | Dokumentacja firmy Microsoft"
description: "Języki maszyny wirtualnej nauki danych na platformie Azure"
keywords: "narzędzia do analizy danych, maszyny wirtualnej analizy danych, narzędzia do analizy danych, nauki danych systemu linux"
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/11/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 2f2125e739b738847e03ce429d65801969611685
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="languages-supported-on-the-data-science-virtual-machine"></a>Języki obsługiwane na maszynie wirtualnej nauki danych 

Maszyna wirtualna nauki danych (DSVM) zawiera kilka wbudowanych języków i narzędzia deweloperskie do tworzenia aplikacji AI. Poniżej przedstawiono niektóre istotne z nich. 

## <a name="python"></a>Python

|    |           |
| ------------- | ------------- |
| Wersji językowych obsługiwane | 2.7 i 3.5 |
| DSVM obsługiwane wersje      | Linux, systemu Windows     |
| Jak jest on skonfigurowany / zainstalowanym DSVM?  | Dwa globalne `conda` środowisk są tworzone. <br /> * `root`w lokalizacji środowiska `/anaconda/` jest Python 2.7. <br/> * `py35`w lokalizacji środowiska `/anaconda/envs/py35`jest Python 3.5       |
| Łącza do próbek      | Uwzględniono notesów Jupyter próbki dla języka Python     |
| Pokrewne narzędzia na DSVM      | Julia PySpark, R,      |
### <a name="how-to-use--run-it"></a>Jak używać / uruchom go?    

**Windows**:

* W wierszu polecenia

Otwórz wiersz polecenia, a następnie wykonaj następujące kroki w zależności od wersji języka Python, który chcesz uruchomić. 

```
# To run Python 2.7
activate 
python --version

# To run Python 3.5
activate py35
python --version

```
* Przy użyciu w środowisku IDE

Użyj narzędzia Python Tools dla programu Visual Studio (PTVS) zainstalowany w wersji Visual Studio Community. Ustawienia środowiska tylko automatycznie w PTVS w Python 2.7. 
> [!NOTE]
> Aby wskazać PTVS Python 3.5, należy utworzyć niestandardowe środowiska w PTVS. Aby ustawić tej ścieżki środowiska Visual Studio Community Edition, przejdź do **narzędzia** -> **narzędzi Python Tools** -> **środowiska Python** a następnie kliknij przycisk **+ niestandardowe**. Następnie ustaw lokalizację `c:\anaconda\envs\py35` , a następnie kliknij przycisk _Autowykrywanie_. 

* Przy użyciu w oprogramowaniu Jupyter

Otwórz Jupyter i wybierz polecenie `New` przycisk, aby utworzyć nowy notes. W tym momencie można wybrać typ jądra jako _Python [Conda głównego]_ for Python 2.7 i _Python [Conda env:py35]_ dla środowiska Python 3.5. 

* Instalowanie pakietów języka Python

Domyślne środowiska Python w DSVM są globalne środowiska do odczytu przez wszystkich użytkowników. Ale tylko administratorzy mogą zapisu / zainstalować pakiety globalnego. Aby można było zainstalować pakiet środowiska globalnych, aktywować do katalogu głównego lub przy użyciu środowiska py35 `activate` polecenia jako Administrator. Następnie można użyć Menedżera pakietów, takie jak `conda` lub `pip` zainstalować lub pakietów aktualizacji. 


**Linux**:

* W terminalu

Otwórz terminal i wykonaj następujące kroki w zależności od wersji języka Python, który chcesz uruchomić. 

```
# To run Python 2.7
source activate 
python --version

# To run Python 3.5
source activate py35
python --version

```
* Przy użyciu w środowisku IDE

Użyj PyCharm zainstalowany w wersji Visual Studio Community. 

* Przy użyciu w oprogramowaniu Jupyter

Otwórz Jupyter i wybierz polecenie `New` przycisk, aby utworzyć nowy notes. W tym momencie można wybrać typ jądra jako _Python [Conda głównego]_ for Python 2.7 i _Python [Conda env:py35]_ dla środowiska Python 3.5. 

* Instalowanie pakietów języka Python

Środowiska Python domyślnej na DSVM są globalne środowisk do odczytu dla wszystkich użytkowników. Ale tylko administratorzy mogą zapisu / zainstalować pakiety globalnego. Aby można było zainstalować pakiet środowiska globalnych, aktywować do katalogu głównego lub przy użyciu środowiska py35 `source activate` polecenia jako Administrator lub użytkownik z uprawnieniami sudo. Następnie można użyć Menedżera pakietów, takie jak `conda` lub `pip` zainstalować lub pakietów aktualizacji. 

## <a name="r"></a>R

|    |           |
| ------------- | ------------- |
| Wersji językowych obsługiwane | Otwórz R Microsoft 3.x (100% zgodny z sieci CRAN-R<br /> Serwer R Microsoft 9.x Developer edition (A Scalable Enterprise gotowe platformy R)|
| DSVM obsługiwane wersje      | Linux, systemu Windows     |
| Jak jest on skonfigurowany / zainstalowanym DSVM?  | System Windows:`C:\Program Files\Microsoft\R Server\R_SERVER` <br />Linux:` /usr/lib64/microsoft-r/3.3/lib64/R`    |
| Łącza do próbek      | Przykładowe notesów Jupyter dla języka R są dołączone     |
| Pokrewne narzędzia na DSVM      | Julia SparkR, Python,      |
### <a name="how-to-use--run-it"></a>Jak używać / uruchom go?    

**Windows**:

* W wierszu polecenia

Otwórz wiersz polecenia i wpisz `R`.

* Przy użyciu w środowisku IDE

Użyj RTools dla programu Visual Studio (RTVS) zainstalowanej w Visual Studio Community edition i programu RStudio. Są one dostępne w start menu lub jako ikony pulpitu. 

* Przy użyciu w oprogramowaniu Jupyter

Otwórz Jupyter i wybierz polecenie `New` przycisk, aby utworzyć nowy notes. W tym momencie można wybrać typ jądra jako _R_ do użycia Jupyter R jądra (IRKernel). 

* Instalowanie pakietów języka R

R jest zainstalowany na DSVM w środowisku globalne do odczytu dla wszystkich użytkowników. Ale tylko administratorzy mogą zapisu / zainstalować pakiety globalnego. Aby można było zainstalować pakiet środowiska globalnych, uruchom R przy użyciu jednej z metod powyżej. Następnie możesz uruchomić Menedżera pakietów R `install.packages()` zainstalować lub pakietów aktualizacji. 

**Linux**:

* W terminalu

Otwórz terminal i Uruchom tylko `R`.  

* Przy użyciu w środowisku IDE

Użyj programu RStudio zainstalowanym DSVM systemu Linux.  

* Przy użyciu w oprogramowaniu Jupyter

Otwórz Jupyter i wybierz polecenie `New` przycisk, aby utworzyć nowy notes. W tym momencie można wybrać typ jądra jako _R_ do użycia Jupyter R jądra (IRKernel). 

* Instalowanie pakietów języka R

R jest zainstalowany na DSVM w środowisku globalne do odczytu dla wszystkich użytkowników. Ale tylko administratorzy mogą zapisu / zainstalować pakiety globalnego. Aby można było zainstalować pakiet środowiska globalnych, uruchom R przy użyciu jednej z metod powyżej. Następnie możesz uruchomić Menedżera pakietów R `install.packages()` zainstalować lub pakietów aktualizacji. 


## <a name="julia"></a>Julia

|    |           |
| ------------- | ------------- |
| Wersji językowych obsługiwane | 0.5 |
| DSVM obsługiwane wersje      | Linux, systemu Windows     |
| Jak jest on skonfigurowany / zainstalowanym DSVM?  | System Windows: Zainstalowany w`C:\JuliaPro-VERSION`<br /> Linux: Zainstalowane w`/opt/JuliaPro-VERSION`    |
| Łącza do próbek      | Uwzględniono notesów Jupyter próbki dla Julia     |
| Pokrewne narzędzia na DSVM      | Python-R      |
### <a name="how-to-use--run-it"></a>Jak używać / uruchom go?    

**Windows**:

* W wierszu polecenia

Otwórz wiersz polecenia i uruchom `julia`. 
* Przy użyciu w środowisku IDE

Użyj `Juno` IDE Julia zainstalowanych na DSVM i dostępna jako skrót na pulpicie.

* Przy użyciu w oprogramowaniu Jupyter

Otwórz Jupyter i wybierz polecenie `New` przycisk, aby utworzyć nowy notes. W tym momencie można wybrać typ jądra jako`Julia VERSION` 

* Instalowanie pakietów Julia

Domyślna lokalizacja Julia to środowisko globalne do odczytu przez wszystkich użytkowników. Ale tylko administratorzy mogą zapisu / zainstalować pakiety globalnego. Aby można było zainstalować pakiet środowiska globalnych, uruchom Julia przy użyciu jednej z metod powyżej. Następnie możesz uruchomić pakiet Julia Menedżer poleceń, takich jak `Pkg.add()` zainstalować lub pakietów aktualizacji. 


**Linux**:
* Uruchomione w terminalu.

Otwórz terminal i Uruchom tylko `julia`. 
* Przy użyciu w środowisku IDE

Użyj `Juno` IDE Julia zainstalowanych na DSVM i dostępne jako skrót menu aplikacji.

* Przy użyciu w oprogramowaniu Jupyter

Otwórz Jupyter i wybierz polecenie `New` przycisk, aby utworzyć nowy notes. W tym momencie można wybrać typ jądra jako`Julia VERSION` 

* Instalowanie pakietów Julia

Domyślna lokalizacja Julia to środowisko globalne do odczytu przez wszystkich użytkowników. Ale tylko administratorzy mogą zapisu / zainstalować pakiety globalnego. Aby można było zainstalować pakiet środowiska globalnych, uruchom Julia przy użyciu jednej z metod powyżej. Następnie możesz uruchomić pakiet Julia Menedżer poleceń, takich jak `Pkg.add()` zainstalować lub pakietów aktualizacji. 

## <a name="other-languages"></a>Inne języki

**C#**: dostępne w systemie Windows i jest dostępny, za pomocą programu Visual Studio Community edition lub na `Developer Command Prompt for Visual Studio` można po prostu realizującym `csc` polecenia. 

**Java**: OpenJDK jest dostępna w wersji zarówno systemu Linux i Windows DSVM i zestawu w ścieżce. Możesz wpisać `javac` lub `java` polecenie w wierszu polecenia systemu Windows lub powłoki bash w systemie Linux do używania języka Java. 

**node.js**: node.js jest dostępna w wersji zarówno systemu Linux i Windows DSVM i zestawu w ścieżce. Możesz wpisać `node` lub `npm` polecenie w wierszu polecenia systemu Windows lub powłoki bash w systemie Linux można uzyskać dostępu do środowiska node.js. W systemie Windows narzędzia Node.js dla rozszerzenia Visual Studio jest zainstalowany zapewnienie graficznego IDE umożliwiające tworzenie aplikacji node.js. 

**F #**: dostępne w systemie Windows i jest dostępny, za pomocą programu Visual Studio Community edition lub na `Developer Command Prompt for Visual Studio` można po prostu realizującym `fsc` polecenia. 


