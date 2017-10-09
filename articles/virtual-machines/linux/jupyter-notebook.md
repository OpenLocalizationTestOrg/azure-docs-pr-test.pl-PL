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
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="1b0f9-103">Tworzenie maszyny Wirtualnej platformy Azure, instalowania Jupyter i uruchamiania notesu Jupyter na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1b0f9-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="1b0f9-104">Witaj [projektu Jupyter](http://jupyter.org), wcześniej hello [IPython projektu](http://ipython.org), udostępnia kolekcję narzędzi dla przy użyciu zaawansowanych powłok interaktywne, łączące wykonanie kodu z tworzenia hello obliczanie naukowe dokument obliczeniową na żywo.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-104">hello [Jupyter project](http://jupyter.org), formerly hello [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with hello creation of a live computational document.</span></span> <span data-ttu-id="1b0f9-105">Te pliki notesu może zawierać dowolnego tekstu, matematycznymi, podaj kod, wyniki, grafiki, wideo i dowolnego typu nośnika Nowoczesna przeglądarka sieci web jest w stanie wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="1b0f9-106">Określa, czy jest całkowicie nowe tooPython i chcesz toolearn w fun, interaktywnego środowiska lub czy niektóre poważne równoległe/technicznych obliczeniowych, hello notesu Jupyter jest doskonałym wyborem.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-106">Whether you're absolutely new tooPython and want toolearn it in a fun, interactive environment or do some serious parallel/technical computing, hello Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="1b0f9-107">![Zrzut ekranu](./media/jupyter-notebook/ipy-notebook-spectral.png) przy użyciu SciPy Matplotlib pakiety tooanalyze hello struktury i nagrywanie dźwięku.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages tooanalyze hello structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="1b0f9-108">Jupyter dwa sposoby: Wdrażanie niestandardowych lub Azure notesów</span><span class="sxs-lookup"><span data-stu-id="1b0f9-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="1b0f9-109">Platforma Azure udostępnia usługi, która służy za[szybko uruchomić przy użyciu oprogramowania Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-109">Azure provides a service that you can use too[quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="1b0f9-110">Przy użyciu hello Azure notesu usługi, można łatwo uzyskać tooJupyter dostępu interfejsu dostępnej w sieci web do skalowalnych zasobów obliczeniowych przy użyciu hello zasilania środowiska Python i jego wiele bibliotek.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-110">By using hello Azure Notebook Service, you can easily gain access tooJupyter's web-accessible interface to scalable computational resources with all hello power of Python and its many libraries.</span></span>  <span data-ttu-id="1b0f9-111">Ponieważ instalacja hello jest obsługiwana przez usługę hello, użytkownicy mogą otwierać tych zasobów, bez potrzeby hello administracji i konfiguracji przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-111">Since hello installation is handled by hello service, users can access these resources without hello need for administration and configuration by hello user.</span></span>

<span data-ttu-id="1b0f9-112">Jeśli usługa notesu hello nie działa w przypadku danego scenariusza nadal tooread tego artykułu, który będzie opisano sposób toodeploy hello notesu Jupyter w systemie Microsoft Azure przy użyciu maszyn wirtualnych systemu Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-112">If hello notebook service does not work for your scenario please continue tooread this article which will will show you how toodeploy hello Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="1b0f9-113">Tworzenie i konfigurowanie maszyny Wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1b0f9-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="1b0f9-114">pierwszym krokiem Hello jest toocreate maszynę wirtualną (VM) działającą na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-114">hello first step is toocreate a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="1b0f9-115">Ta maszyna wirtualna jest całego systemu operacyjnego w chmurze hello i będzie służyć do uruchamiania hello notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-115">This VM is a complete operating system in hello cloud and will be used to run hello Jupyter Notebook.</span></span> <span data-ttu-id="1b0f9-116">Jest w stanie uruchomionych maszyn wirtualnych zarówno systemu Linux i Windows Azure i omówimy hello ustawienia Jupyter na oba typy maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover hello setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="1b0f9-117">Utwórz Maszynę wirtualną systemu Linux i otwarcie portu dla Jupyter</span><span class="sxs-lookup"><span data-stu-id="1b0f9-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="1b0f9-118">Postępuj zgodnie z instrukcjami hello [tutaj] [ portal-vm-linux] toocreate maszynę wirtualną w hello *Ubuntu* dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-118">Follow hello instructions given [here][portal-vm-linux] toocreate a virtual machine of hello *Ubuntu* distribution.</span></span> <span data-ttu-id="1b0f9-119">W tym samouczku używana Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="1b0f9-120">Przyjmiemy nazwy użytkownika hello *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-120">We'll assume hello user name *azureuser*.</span></span>

<span data-ttu-id="1b0f9-121">Po wdraża maszyny wirtualnej hello potrzebujemy tooopen reguły zabezpieczeń na powitania sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-121">After hello virtual machine deploys we need tooopen up a security rule on hello network security group.</span></span>  <span data-ttu-id="1b0f9-122">Z hello portalu Azure, przejdź zbyt**grup zabezpieczeń sieci** i hello Otwórz kartę tooyour odpowiedniego hello grupy zabezpieczeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-122">From hello Azure portal, go too**Network Security Groups** and open hello tab for hello Security Group corresponding tooyour VM.</span></span> <span data-ttu-id="1b0f9-123">Należy tooadd reguły zabezpieczeń ruchu przychodzącego z hello następujące ustawienia: **TCP** dla protokołu hello  **\***  hello portu źródłowego (publicznej) i **9999** dla Witaj port docelowy (prywatny).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-123">You need tooadd an Inbound Security rule with hello following settings: **TCP** for hello protocol, **\*** for hello source (public) port and **9999** for hello destination (private) port.</span></span>

![Zrzut ekranu](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="1b0f9-125">Znajduje się w sieciowej grupy zabezpieczeń, kliknij polecenie **interfejsów sieciowych** i hello Uwaga **publicznego adresu IP** jak będą potrzebne tooconnect tooyour maszyny Wirtualnej w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-125">While in your Network Security Group, click on **Network Interfaces** and note hello **Public IP Address** as it will be needed tooconnect tooyour VM in hello next step.</span></span>

## <a name="install-required-software-on-hello-vm"></a><span data-ttu-id="1b0f9-126">Zainstaluj oprogramowanie wymagane na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1b0f9-126">Install required software on hello VM</span></span>
<span data-ttu-id="1b0f9-127">toorun hello notesu Jupyter w naszym maszyny Wirtualnej, musi najpierw zainstalować Jupyter i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-127">toorun hello Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="1b0f9-128">Połącz przy użyciu ssh maszyny wirtualnej systemu linux tooyour i parę nazwy użytkownika i hasła hello wybrane, podczas tworzenia hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-128">Connect tooyour linux vm using ssh and hello username/password pair you chose when you created hello vm.</span></span> <span data-ttu-id="1b0f9-129">W tym samouczku będziemy przy użyciu programu PuTTY i Połącz z systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="1b0f9-130">Instalowanie oprogramowania Jupyter na Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1b0f9-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="1b0f9-131">Zainstaluj platformę Anaconda — dystrybucję oprogramowania python nauki popularnych danych przy użyciu jednej z łącza hello [Analytics kontynuacja](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-131">Install Anaconda, a popular data science python distribution, using one of hello links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="1b0f9-132">Począwszy od hello opracowywania tego dokumentu, hello poniższych łączy są hello najbardziej się toodate wersji.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-132">As of hello writing of this document, hello below links are hello most up toodate versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="1b0f9-133">Instaluje anaconda dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="1b0f9-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="1b0f9-134">Języka Python 3.4</span><span class="sxs-lookup"><span data-stu-id="1b0f9-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="1b0f9-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="1b0f9-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="1b0f9-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64-bitowy</href>
    </span><span class="sxs-lookup"><span data-stu-id="1b0f9-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="1b0f9-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64-bitowy</href>
    </span><span class="sxs-lookup"><span data-stu-id="1b0f9-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1b0f9-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32-bitowy</href>
    </span><span class="sxs-lookup"><span data-stu-id="1b0f9-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="1b0f9-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32-bitowy</href>
    </span><span class="sxs-lookup"><span data-stu-id="1b0f9-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="1b0f9-140">Instalowanie Anaconda3 2.3.0 64-bit na Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1b0f9-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="1b0f9-141">Na przykład jest to, jak można zainstalować na Ubuntu Anaconda</span><span class="sxs-lookup"><span data-stu-id="1b0f9-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

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

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="1b0f9-143">Konfigurowanie Jupyter i przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="1b0f9-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="1b0f9-144">Po zainstalowaniu potrzebujemy tootake plików konfiguracji hello toosetup obecnie dla Jupyter.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-144">After installing we need tootake a moment toosetup hello configuration files for Jupyter.</span></span> <span data-ttu-id="1b0f9-145">Jeśli wystąpią troubles przy konfigurowaniu Jupyter mogą być przydatne toolook na powitania [dokumentacji systemem Server notesu Jupyter](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-145">If you experience troubles with configuring Jupyter it may be helpful toolook at hello [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="1b0f9-146">Dalej będziemy `cd` toohello profilu toocreate katalogu naszych certyfikatu SSL i edycję pliku konfiguracyjnego hello profilów.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-146">Next we `cd` toohello profile directory toocreate our SSL certificate and edit hello profiles configuration file.</span></span>

<span data-ttu-id="1b0f9-147">W systemie Linux należy użyć hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-147">On Linux use hello following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="1b0f9-148">Użyj hello następujące polecenia toocreate hello certyfikat SSL (Linux i Windows).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-148">Use hello following command toocreate hello SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="1b0f9-149">Należy pamiętać, że ponieważ podpisany certyfikat SSL, jest tworzone podczas łączenia notesu toohello przeglądarkę zapewni ostrzeżenie o zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-149">Note that since we are creating a self-signed SSL certificate, when connecting toohello notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="1b0f9-150">Długoterminowe użycia w środowisku produkcyjnym mają toouse są poprawnie podpisane certyfikatu skojarzonego z Twoją organizacją.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-150">For long-term production use, you will want toouse a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="1b0f9-151">Ponieważ zarządzanie certyfikatami wykracza poza zakres tego pokazu hello, firma Microsoft będzie trzymaj certyfikatu z podpisem własnym tooa teraz.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-151">Since certificate management is beyond hello scope of this demo, we will stick tooa self-signed certificate for now.</span></span>

<span data-ttu-id="1b0f9-152">Ponadto toousing certyfikatu, musisz także podać tooprotect hasło notesu przed nieautoryzowanym użyciem.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-152">In addition toousing a certificate, you must also provide a password tooprotect your notebook from unauthorized use.</span></span>  <span data-ttu-id="1b0f9-153">Ze względów bezpieczeństwa Jupyter używa hasła szyfrowane w pliku konfiguracji, dlatego potrzebujesz tooencrypt hasło najpierw.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need tooencrypt your password first.</span></span>  <span data-ttu-id="1b0f9-154">Udostępnia IPython toodo narzędzie w wierszu polecenia Uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-154">IPython provides a utility toodo so; at a command prompt run hello following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="1b0f9-155">Wyświetli monit o hasło i potwierdzenie, a następnie będzie drukować hello hasła.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-155">This will prompt you for a password and confirmation, and will then print hello password.</span></span> <span data-ttu-id="1b0f9-156">Uwaga to powitania po kroku.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-156">Note this for hello following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

<span data-ttu-id="1b0f9-157">Następnie zostanie Edytuj plik konfiguracyjny hello profil, który jest `jupyter_notebook_config.py` pliku w katalogu hello w.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-157">Next, we will edit hello profile's configuration file, which is the `jupyter_notebook_config.py` file in hello directory you are in.</span></span>  <span data-ttu-id="1b0f9-158">Należy pamiętać, że ten plik nie istnieje — wystarczy utworzyć hello sytuacji.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-158">Note that this file may not exist -- just create it if that is hello case.</span></span>  <span data-ttu-id="1b0f9-159">Ten plik zawiera liczbę pól i domyślnie wszystkie są oznaczone jako komentarz.  Ten plik można otworzyć za pomocą dowolnego edytora tekstów, z Twoim preferencjom i upewnij się, że ma co najmniej hello po zawartości.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least hello following content.</span></span> <span data-ttu-id="1b0f9-160">**Należy się c.NotebookApp.password hello tooreplace w pliku konfiguracyjnym hello z sha1 hello z poprzedniego kroku hello**.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-160">**Be sure tooreplace hello c.NotebookApp.password in hello config with hello sha1 from hello previous step**.</span></span>

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

### <a name="run-hello-jupyter-notebook"></a><span data-ttu-id="1b0f9-161">Uruchom hello notesu Jupyter</span><span class="sxs-lookup"><span data-stu-id="1b0f9-161">Run hello Jupyter Notebook</span></span>
<span data-ttu-id="1b0f9-162">W tym momencie mamy hello gotowe toostart notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-162">At this point we are ready toostart hello Jupyter Notebook.</span></span> <span data-ttu-id="1b0f9-163">toodo, przejdź do katalogu toohello notesów toostore i zacząć powitania serwera notesu Jupyter z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-163">toodo this, navigate toohello directory you want toostore notebooks in and start hello Jupyter Notebook server with hello following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="1b0f9-164">Możesz teraz powinno być możliwe tooaccess notesu Jupyter pod adresem hello `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-164">You should now be able tooaccess your Jupyter Notebook at hello address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="1b0f9-165">Przy pierwszym uzyskaniu dostępu notesu strony logowania hello monituje o podanie hasła.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-165">When you first access your notebook, hello login page asks for your password.</span></span> <span data-ttu-id="1b0f9-166">I po zalogowaniu zostanie wyświetlona "Pulpitu nawigacyjnego notesu Jupyter," hello czyli Centrum kontrolne dla wszystkich operacji notesu.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-166">And once you log in, you will see hello "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="1b0f9-167">Na tej stronie można tworzyć nowych notesów i otworzyć istniejące.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-167">From this page you can create new notebooks and open existing ones.</span></span>

![Zrzut ekranu](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a><span data-ttu-id="1b0f9-169">Przy użyciu hello notesu Jupyter</span><span class="sxs-lookup"><span data-stu-id="1b0f9-169">Using hello Jupyter Notebook</span></span>
<span data-ttu-id="1b0f9-170">Jeśli klikniesz przycisk hello **nowy** przycisku, zobaczysz powitania po strona początkowa.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-170">If you click hello **New** button, you will see hello following opening page.</span></span>

![Zrzut ekranu](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="1b0f9-172">obszar Hello oznaczonych `In []:` monit jest hello obszaru wprowadzania, w tym miejscu można wpisać prawidłowy kod języka Python i wykona naciśnięcie `Shift-Enter` lub kliknij ikonę "Play" hello (hello wskazująca w prawo trójkąt hello w pasku narzędzi).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-172">hello area marked with an `In []:` prompt is hello input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on hello "Play" icon (hello right-pointing triangle in hello toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="1b0f9-173">Zaawansowanego modelu: obliczeniowa dokumentów za pomocą multimedialną na żywo</span><span class="sxs-lookup"><span data-stu-id="1b0f9-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="1b0f9-174">notesu Hello, sama powinien uznać tooanyone bardzo fizycznych, który został użyty, Python i Edytor tekstów, ponieważ znajduje się w pewnym sensie kombinację obu: można wykonywać bloki kodu języka Python, ale można również zarejestrować uwagi i innych tekstu, zmieniając hello stylu komórki 'Code' zbyt "Ma rkdown"przy użyciu menu rozwijanego hello na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-174">hello notebook itself should feel very natural tooanyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing hello style of a cell from "Code" too"Markdown" using hello drop-down menu in the toolbar.</span></span>

<span data-ttu-id="1b0f9-175">Jupyter jest znacznie więcej niż edytora tekstów, który zezwala na łączenie obliczeń i rozbudowane nośnika (tekstu, grafiki, wideo i praktycznie coś, co umożliwia wyświetlanie Nowoczesna przeglądarka sieci web).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="1b0f9-176">Można łączyć, tekst, kod, klipów wideo i inne!</span><span class="sxs-lookup"><span data-stu-id="1b0f9-176">You can mix, text, code, videos and more!</span></span>

![Zrzut ekranu](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="1b0f9-178">I o sile hello wiele bibliotek znakomity języka Python dla naukowo obliczeniowych w hello następującego zrzutu ekranu, prostego obliczenia można wykonywać za pomocą hello sam do jej obsługi ułatwiają jako analizę złożoną siecią wszystko w jednym środowisku.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-178">And with hello power of Python's many excellent libraries for scientific and technical computing, in hello following screenshot, a simple calculation can be performed with hello same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="1b0f9-179">Ten model mieszania hello możliwości hello nowoczesnych witryn sieci web z obliczeń na żywo oferuje wiele możliwości i doskonale nadaje się do chmury hello; Witaj notesu może być używany:</span><span class="sxs-lookup"><span data-stu-id="1b0f9-179">This paradigm of mixing hello power of hello modern web with live computation offers many possibilities, and is ideally suited for hello cloud; hello Notebook can be used:</span></span>

* <span data-ttu-id="1b0f9-180">Jako toorecord obliczeniową Notatnik poznawcze działają w problem.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-180">As a computational scratchpad toorecord exploratory work on a problem.</span></span>
* <span data-ttu-id="1b0f9-181">powoduje tooshare współpracownikom "na żywo" formularza obliczeniową lub pisemnie formatów (HTML, plików PDF).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-181">tooshare results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="1b0f9-182">toodistribute obecny materiałów nauczania na żywo obejmujących obliczeń, więc studentów można natychmiast eksperymentować hello rzeczywisty kod, zmodyfikuj go i ponownie wykonaj interaktywnie.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-182">toodistribute and present live teaching materials that involve computation, so students can immediately experiment with hello real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="1b0f9-183">tooprovide "wykonywalny dokumenty", udostępniające hello wyników badań w taki sposób, który można od razu można odtworzyć, zweryfikowane i rozszerzać przez innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-183">tooprovide "executable papers" that present hello results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="1b0f9-184">Jako platforma do współpracy obliczeniowych: wiele użytkownicy mogą zalogować toothe sam notesu serwera tooshare obliczeniową sesję na żywo.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-184">As a platform for collaborative computing: multiple users can log in toothe same notebook server tooshare a live computational session.</span></span>

<span data-ttu-id="1b0f9-185">Jeśli przejdziesz kodu źródłowego IPython toohello [repozytorium][repository], można znaleźć cały katalog wraz z przykładami notesu, które można pobrać i eksperymentować na maszynie Wirtualnej własne Azure Jupyter.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-185">If you go toohello IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="1b0f9-186">Wystarczy pobrać hello `.ipynb` pliki z hello lokacji i przekazać je na pulpit nawigacyjny hello notesu maszyny Wirtualnej platformy Azure (lub pobrać je bezpośrednio do hello maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-186">Simply download hello `.ipynb` files from hello site and upload them onto hello dashboard of your notebook Azure VM (or download them directly into hello VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="1b0f9-187">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="1b0f9-187">Conclusion</span></span>
<span data-ttu-id="1b0f9-188">Hello notesu Jupyter zapewnia zaawansowany interfejs do uzyskiwania dostępu do interaktywnego zasilania hello ekosystemu języka Python hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-188">hello Jupyter Notebook provides a powerful interface for accessing interactively hello power of hello Python ecosystem on Azure.</span></span>  <span data-ttu-id="1b0f9-189">Obejmuje ona szeroką gamę przypadków użycia w tym proste eksploracji i Nauka języka Python, analizy danych i wizualizacji, symulacji oraz przetwarzania równoległego.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="1b0f9-190">Hello wynikowy notesu dokumenty zawierają pełny rekord hello obliczenia, które są wykonywane i może być współużytkowane z innymi użytkownikami Jupyter.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-190">hello resulting Notebook documents contain a complete record of hello computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="1b0f9-191">Witaj notesu Jupyter mogą być używane jako lokalnych aplikacji, ale najlepiej nadaje się do wdrożenia w chmurze na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1b0f9-191">hello Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="1b0f9-192">Witaj podstawowych funkcji oprogramowania Jupyter są również dostępne w programie Visual Studio za pomocą [narzędzi Python Tools for Visual Studio] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-192">hello core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="1b0f9-193">PTVS to bezpłatny i wtyczki firmy Microsoft, które włącza Visual Studio do zaawansowanego środowiska programowania Python obejmuje Zaawansowany edytor z funkcji IntelliSense, debugowania, profilowania i równoległych open source obliczeniowych integracji.</span><span class="sxs-lookup"><span data-stu-id="1b0f9-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b0f9-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b0f9-194">Next steps</span></span>
<span data-ttu-id="1b0f9-195">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="1b0f9-195">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
