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
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="0da2a-103">Tworzenie maszyny Wirtualnej platformy Azure, instalowania Jupyter i uruchamiania notesu Jupyter na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0da2a-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="0da2a-104">[Projektu Jupyter](http://jupyter.org), wcześniej [projektu IPython](http://ipython.org), udostępnia kolekcję narzędzi dla obliczanie naukowe przy użyciu zaawansowanych powłok interaktywne, łączące wykonanie kodu z tworzeniem na żywo dokument obliczeniową.</span><span class="sxs-lookup"><span data-stu-id="0da2a-104">The [Jupyter project](http://jupyter.org), formerly the [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with the creation of a live computational document.</span></span> <span data-ttu-id="0da2a-105">Te pliki notesu może zawierać dowolnego tekstu, matematycznymi, podaj kod, wyniki, grafiki, wideo i dowolnego typu nośnika Nowoczesna przeglądarka sieci web jest w stanie wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="0da2a-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="0da2a-106">Czy można całkowicie nowych użytkowników programu Python i Dowiedz się więcej w środowisku przyjemne, interakcyjnego lub czy niektóre poważne przetwarzanie równoległe/technical notesu Jupyter jest doskonałym wyborem.</span><span class="sxs-lookup"><span data-stu-id="0da2a-106">Whether you're absolutely new to Python and want to learn it in a fun, interactive environment or do some serious parallel/technical computing, the Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="0da2a-107">![Zrzut ekranu](./media/jupyter-notebook/ipy-notebook-spectral.png) pakietów przy użyciu SciPy i Matplotlib do analizowania struktury nagrywanie dźwięku.</span><span class="sxs-lookup"><span data-stu-id="0da2a-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages to analyze the structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="0da2a-108">Jupyter dwa sposoby: Wdrażanie niestandardowych lub Azure notesów</span><span class="sxs-lookup"><span data-stu-id="0da2a-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="0da2a-109">Platforma Azure udostępnia usługi, która umożliwia [szybko uruchomić przy użyciu oprogramowania Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="0da2a-109">Azure provides a service that you can use to [quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="0da2a-110">Za pomocą usługi Azure notesu, można łatwo uzyskać dostęp do interfejsu dostępnej w sieci web firmy Jupyter skalowalnych zasobów obliczeniowych dzięki możliwościom języka Python i wiele bibliotek.</span><span class="sxs-lookup"><span data-stu-id="0da2a-110">By using the Azure Notebook Service, you can easily gain access to Jupyter's web-accessible interface to scalable computational resources with all the power of Python and its many libraries.</span></span>  <span data-ttu-id="0da2a-111">Ponieważ instalacja jest obsługiwane przez usługę, użytkownicy można uzyskiwać dostęp do tych zasobów, bez konieczności zarządzania i konfiguracji przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0da2a-111">Since the installation is handled by the service, users can access these resources without the need for administration and configuration by the user.</span></span>

<span data-ttu-id="0da2a-112">Jeśli usługa notesu nie działa w przypadku danego scenariusza nadal przeczytaj ten artykuł, który będzie opisano sposób wdrażania notesu Jupyter w systemie Microsoft Azure przy użyciu maszyn wirtualnych systemu Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="0da2a-112">If the notebook service does not work for your scenario please continue to read this article which will will show you how to deploy the Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="0da2a-113">Tworzenie i konfigurowanie maszyny Wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0da2a-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="0da2a-114">Pierwszym krokiem jest utworzenie maszyny wirtualnej (VM) działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0da2a-114">The first step is to create a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="0da2a-115">Ta maszyna wirtualna jest całego systemu operacyjnego w chmurze i będzie służyć do uruchamiania notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="0da2a-115">This VM is a complete operating system in the cloud and will be used to run the Jupyter Notebook.</span></span> <span data-ttu-id="0da2a-116">Jest w stanie uruchomionych maszyn wirtualnych zarówno systemu Linux i Windows Azure i omówimy Instalatora oprogramowania Jupyter na oba typy maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0da2a-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover the setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="0da2a-117">Utwórz Maszynę wirtualną systemu Linux i otwarcie portu dla Jupyter</span><span class="sxs-lookup"><span data-stu-id="0da2a-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="0da2a-118">Postępuj zgodnie z instrukcjami [tutaj] [ portal-vm-linux] do utworzenia maszyny wirtualnej z *Ubuntu* dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="0da2a-118">Follow the instructions given [here][portal-vm-linux] to create a virtual machine of the *Ubuntu* distribution.</span></span> <span data-ttu-id="0da2a-119">W tym samouczku używana Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="0da2a-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="0da2a-120">Przyjmiemy nazwy użytkownika *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="0da2a-120">We'll assume the user name *azureuser*.</span></span>

<span data-ttu-id="0da2a-121">Po wdraża maszyny wirtualnej należy otworzyć reguły zabezpieczeń dla grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="0da2a-121">After the virtual machine deploys we need to open up a security rule on the network security group.</span></span>  <span data-ttu-id="0da2a-122">W portalu Azure, przejdź do **grup zabezpieczeń sieci** , a następnie otwórz kartę dla grupy zabezpieczeń odpowiadający maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0da2a-122">From the Azure portal, go to **Network Security Groups** and open the tab for the Security Group corresponding to your VM.</span></span> <span data-ttu-id="0da2a-123">Należy dodać reguły zabezpieczeń ruchu przychodzącego z następującymi ustawieniami: **TCP** protokołu,  **\***  dla portu źródłowego (publicznej) i **9999** dla port docelowy (prywatny).</span><span class="sxs-lookup"><span data-stu-id="0da2a-123">You need to add an Inbound Security rule with the following settings: **TCP** for the protocol, **\*** for the source (public) port and **9999** for the destination (private) port.</span></span>

![Zrzut ekranu](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="0da2a-125">Znajduje się w sieciowej grupy zabezpieczeń, kliknij polecenie **interfejsów sieciowych** i zanotuj **publicznego adresu IP** , ponieważ jest ono potrzebne do nawiązania połączenia z maszyną Wirtualną w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="0da2a-125">While in your Network Security Group, click on **Network Interfaces** and note the **Public IP Address** as it will be needed to connect to your VM in the next step.</span></span>

## <a name="install-required-software-on-the-vm"></a><span data-ttu-id="0da2a-126">Zainstaluj w maszynie Wirtualnej wymaganego oprogramowania</span><span class="sxs-lookup"><span data-stu-id="0da2a-126">Install required software on the VM</span></span>
<span data-ttu-id="0da2a-127">Aby uruchomić notesu Jupyter w naszym maszyny Wirtualnej, możemy najpierw zainstalować Jupyter i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="0da2a-127">To run the Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="0da2a-128">Nawiązywanie połączenia z systemem linux maszynę wirtualną przy użyciu ssh i parą nazwy użytkownika i hasła, należy wybrać podczas tworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0da2a-128">Connect to your linux vm using ssh and the username/password pair you chose when you created the vm.</span></span> <span data-ttu-id="0da2a-129">W tym samouczku będziemy przy użyciu programu PuTTY i Połącz z systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0da2a-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="0da2a-130">Instalowanie oprogramowania Jupyter na Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0da2a-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="0da2a-131">Zainstaluj platformę Anaconda — dystrybucję oprogramowania python nauki popularnych danych przy użyciu jednej z łącza z [Analytics kontynuacja](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="0da2a-131">Install Anaconda, a popular data science python distribution, using one of the links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="0da2a-132">Przeprowadzonych podczas opracowywania tego dokumentu poniższych łączy są najbardziej aktualne wersje daty.</span><span class="sxs-lookup"><span data-stu-id="0da2a-132">As of the writing of this document, the below links are the most up to date versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="0da2a-133">Instaluje anaconda dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0da2a-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="0da2a-134">Języka Python 3.4</span><span class="sxs-lookup"><span data-stu-id="0da2a-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="0da2a-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="0da2a-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="0da2a-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64-bitowy</href>
    </span><span class="sxs-lookup"><span data-stu-id="0da2a-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="0da2a-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64-bitowy</href>
    </span><span class="sxs-lookup"><span data-stu-id="0da2a-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="0da2a-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32-bitowy</href>
    </span><span class="sxs-lookup"><span data-stu-id="0da2a-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="0da2a-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32-bitowy</href>
    </span><span class="sxs-lookup"><span data-stu-id="0da2a-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="0da2a-140">Instalowanie Anaconda3 2.3.0 64-bit na Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0da2a-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="0da2a-141">Na przykład jest to, jak można zainstalować na Ubuntu Anaconda</span><span class="sxs-lookup"><span data-stu-id="0da2a-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

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

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="0da2a-143">Konfigurowanie Jupyter i przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="0da2a-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="0da2a-144">Po zainstalowaniu musimy Poświęć chwilę, aby skonfigurować pliki konfiguracji dla Jupyter.</span><span class="sxs-lookup"><span data-stu-id="0da2a-144">After installing we need to take a moment to setup the configuration files for Jupyter.</span></span> <span data-ttu-id="0da2a-145">W przypadku napotkania troubles przy konfigurowaniu Jupyter mogą być pomocne dla przyjrzeć się [dokumentacji systemem Server notesu Jupyter](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="0da2a-145">If you experience troubles with configuring Jupyter it may be helpful to look at the [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="0da2a-146">Dalej będziemy `cd` do katalogu profilu można tworzyć naszych certyfikatu SSL i edytować plik konfiguracji profilów.</span><span class="sxs-lookup"><span data-stu-id="0da2a-146">Next we `cd` to the profile directory to create our SSL certificate and edit the profiles configuration file.</span></span>

<span data-ttu-id="0da2a-147">W systemie Linux należy użyć następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="0da2a-147">On Linux use the following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="0da2a-148">Użyj następującego polecenia, aby utworzyć certyfikat SSL (Linux i Windows).</span><span class="sxs-lookup"><span data-stu-id="0da2a-148">Use the following command to create the SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="0da2a-149">Należy pamiętać, że ponieważ podpisany certyfikat SSL, jest tworzone podczas nawiązywania połączenia z notesu przeglądarki zostaną wyświetlone ostrzeżenie o zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="0da2a-149">Note that since we are creating a self-signed SSL certificate, when connecting to the notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="0da2a-150">Długoterminowego użycia w środowisku produkcyjnym można użyć certyfikatu są poprawnie podpisane skojarzonego z Twoją organizacją.</span><span class="sxs-lookup"><span data-stu-id="0da2a-150">For long-term production use, you will want to use a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="0da2a-151">Ponieważ zarządzanie certyfikatami jest poza zakres tego pokazu, firma Microsoft będzie osadzania certyfikatu z podpisem własnym teraz.</span><span class="sxs-lookup"><span data-stu-id="0da2a-151">Since certificate management is beyond the scope of this demo, we will stick to a self-signed certificate for now.</span></span>

<span data-ttu-id="0da2a-152">Oprócz używa certyfikatu, musisz także podać hasło, aby chronić notesu przed nieautoryzowanym użyciem.</span><span class="sxs-lookup"><span data-stu-id="0da2a-152">In addition to using a certificate, you must also provide a password to protect your notebook from unauthorized use.</span></span>  <span data-ttu-id="0da2a-153">Ze względów bezpieczeństwa Jupyter używa hasła szyfrowane w jego pliku konfiguracji, musisz najpierw szyfrowania hasła.</span><span class="sxs-lookup"><span data-stu-id="0da2a-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need to encrypt your password first.</span></span>  <span data-ttu-id="0da2a-154">IPython udostępnia narzędzia do tego; w wierszu polecenia Uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="0da2a-154">IPython provides a utility to do so; at a command prompt run the following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="0da2a-155">Wyświetli monit o hasło i potwierdzenie, a następnie będzie drukować hasło.</span><span class="sxs-lookup"><span data-stu-id="0da2a-155">This will prompt you for a password and confirmation, and will then print the password.</span></span> <span data-ttu-id="0da2a-156">Uwaga to następny krok.</span><span class="sxs-lookup"><span data-stu-id="0da2a-156">Note this for the following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

<span data-ttu-id="0da2a-157">Następnie zostanie Edytuj plik konfiguracyjny ten profil, który jest `jupyter_notebook_config.py` pliku w znajdują się w katalogu.</span><span class="sxs-lookup"><span data-stu-id="0da2a-157">Next, we will edit the profile's configuration file, which is the `jupyter_notebook_config.py` file in the directory you are in.</span></span>  <span data-ttu-id="0da2a-158">Należy pamiętać, że ten plik nie istnieje — wystarczy utworzyć sytuacji.</span><span class="sxs-lookup"><span data-stu-id="0da2a-158">Note that this file may not exist -- just create it if that is the case.</span></span>  <span data-ttu-id="0da2a-159">Ten plik zawiera liczbę pól i domyślnie wszystkie są oznaczone jako komentarz.</span><span class="sxs-lookup"><span data-stu-id="0da2a-159">This file has a number of fields and by default all are commented out.</span></span>  <span data-ttu-id="0da2a-160">Ten plik można otworzyć za pomocą dowolnego edytora tekstów, z Twoim preferencjom i należy upewnić się, że ma co najmniej następującą zawartość.</span><span class="sxs-lookup"><span data-stu-id="0da2a-160">You can open this file with any text editor of your liking, and you should ensure that it has at least the following content.</span></span> <span data-ttu-id="0da2a-161">**Pamiętaj zastąpić c.NotebookApp.password w pliku config sha1 z poprzedniego kroku**.</span><span class="sxs-lookup"><span data-stu-id="0da2a-161">**Be sure to replace the c.NotebookApp.password in the config with the sha1 from the previous step**.</span></span>

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

### <a name="run-the-jupyter-notebook"></a><span data-ttu-id="0da2a-162">Uruchom notesu Jupyter</span><span class="sxs-lookup"><span data-stu-id="0da2a-162">Run the Jupyter Notebook</span></span>
<span data-ttu-id="0da2a-163">W tym momencie możemy rozpocząć notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="0da2a-163">At this point we are ready to start the Jupyter Notebook.</span></span> <span data-ttu-id="0da2a-164">Aby to zrobić, przejdź do katalogu, który chcesz przechowywać notesów w i uruchomić serwera notesu Jupyter przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="0da2a-164">To do this, navigate to the directory you want to store notebooks in and start the Jupyter Notebook server with the following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="0da2a-165">Teraz powinien mieć możliwość dostępu notesu Jupyter pod adresem `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="0da2a-165">You should now be able to access your Jupyter Notebook at the address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="0da2a-166">Przy pierwszym uzyskaniu dostępu notesu strony logowania monituje o podanie hasła.</span><span class="sxs-lookup"><span data-stu-id="0da2a-166">When you first access your notebook, the login page asks for your password.</span></span> <span data-ttu-id="0da2a-167">I po zalogowaniu zostanie wyświetlona "Jupyter Notebook pulpitu nawigacyjnego", który jest Centrum kontrolne dla wszystkich operacji notesu.</span><span class="sxs-lookup"><span data-stu-id="0da2a-167">And once you log in, you will see the "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="0da2a-168">Na tej stronie można tworzyć nowych notesów i otworzyć istniejące.</span><span class="sxs-lookup"><span data-stu-id="0da2a-168">From this page you can create new notebooks and open existing ones.</span></span>

![Zrzut ekranu](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a><span data-ttu-id="0da2a-170">Za pomocą notesu Jupyter</span><span class="sxs-lookup"><span data-stu-id="0da2a-170">Using the Jupyter Notebook</span></span>
<span data-ttu-id="0da2a-171">Jeśli klikniesz przycisk **nowy** przycisku, zostanie wyświetlona następująca strona otwierania.</span><span class="sxs-lookup"><span data-stu-id="0da2a-171">If you click the **New** button, you will see the following opening page.</span></span>

![Zrzut ekranu](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="0da2a-173">Obszar oznaczonych `In []:` monit jest pole wejściowe, w tym miejscu można wpisać prawidłowy kod języka Python i wykona naciśnięcie `Shift-Enter` lub kliknij ikonę "Play" (wskazująca w prawo trójkąt na pasku narzędzi).</span><span class="sxs-lookup"><span data-stu-id="0da2a-173">The area marked with an `In []:` prompt is the input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on the "Play" icon (the right-pointing triangle in the toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="0da2a-174">Zaawansowanego modelu: obliczeniowa dokumentów za pomocą multimedialną na żywo</span><span class="sxs-lookup"><span data-stu-id="0da2a-174">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="0da2a-175">Sam notesu powinien możesz bardzo fizycznych dla każdego, kto został użyty, Python i Edytor tekstów, ponieważ znajduje się w pewnym sensie kombinację obu: można wykonywać bloki kodu języka Python, ale można również zarejestrować zmieniając stylu komórki z "Code" do "Markdo uwagi i inny tekst dół"przy użyciu menu rozwijanego na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="0da2a-175">The notebook itself should feel very natural to anyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing the style of a cell from "Code" to "Markdown" using the drop-down menu in the toolbar.</span></span>

<span data-ttu-id="0da2a-176">Jupyter jest znacznie więcej niż edytora tekstów, który zezwala na łączenie obliczeń i rozbudowane nośnika (tekstu, grafiki, wideo i praktycznie coś, co umożliwia wyświetlanie Nowoczesna przeglądarka sieci web).</span><span class="sxs-lookup"><span data-stu-id="0da2a-176">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="0da2a-177">Można łączyć, tekst, kod, klipów wideo i inne!</span><span class="sxs-lookup"><span data-stu-id="0da2a-177">You can mix, text, code, videos and more!</span></span>

![Zrzut ekranu](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="0da2a-179">I dzięki możliwościom języka Python wiele znakomity biblioteki naukowo komputerów na poniższym zrzucie ekranu prostego obliczenia można wykonywać za pomocą tego samego łatwość jako analizy złożoną siecią, wszystko w jednym środowisku.</span><span class="sxs-lookup"><span data-stu-id="0da2a-179">And with the power of Python's many excellent libraries for scientific and technical computing, in the following screenshot, a simple calculation can be performed with the same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="0da2a-180">Ten model mieszania zasilania nowoczesnych witryn sieci web z obliczeń na żywo oferuje wiele możliwości i doskonale nadaje się do chmury; można użyć notesu:</span><span class="sxs-lookup"><span data-stu-id="0da2a-180">This paradigm of mixing the power of the modern web with live computation offers many possibilities, and is ideally suited for the cloud; the Notebook can be used:</span></span>

* <span data-ttu-id="0da2a-181">Jako obliczeniową Notatnik, aby zarejestrować poznawcze działają w problem.</span><span class="sxs-lookup"><span data-stu-id="0da2a-181">As a computational scratchpad to record exploratory work on a problem.</span></span>
* <span data-ttu-id="0da2a-182">Aby udostępnić wyniki swojemu współpracowników, w postaci obliczeniową "live" lub w pisemnie formatów (HTML, plików PDF).</span><span class="sxs-lookup"><span data-stu-id="0da2a-182">To share results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="0da2a-183">Do rozpowszechniania i prezentowanie na żywo nauczania materiały, które obejmują obliczeń, więc studentów można natychmiast eksperymentować rzeczywisty kod zmodyfikuj ją i ponownie wykonaj interaktywnie.</span><span class="sxs-lookup"><span data-stu-id="0da2a-183">To distribute and present live teaching materials that involve computation, so students can immediately experiment with the real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="0da2a-184">Aby zapewnić "wykonywalny dokumenty", udostępniające wyników badań w taki sposób, który można natychmiast odtworzyć, zweryfikowane i rozszerzać przez innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0da2a-184">To provide "executable papers" that present the results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="0da2a-185">Jako platforma do współpracy obliczeniowych: wiele użytkownicy mogą zalogować się do tego samego serwera notesu, aby udostępnić obliczeniową sesji na żywo.</span><span class="sxs-lookup"><span data-stu-id="0da2a-185">As a platform for collaborative computing: multiple users can log in to the same notebook server to share a live computational session.</span></span>

<span data-ttu-id="0da2a-186">Jeśli przejdziesz do kodu źródłowego IPython [repozytorium][repository], można znaleźć cały katalog wraz z przykładami notesu, które można pobrać i eksperymentować na maszynie Wirtualnej własne Azure Jupyter.</span><span class="sxs-lookup"><span data-stu-id="0da2a-186">If you go to the IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="0da2a-187">Wystarczy pobrać `.ipynb` plików z lokacji i przekazać je na pulpicie nawigacyjnym notesu maszyny Wirtualnej platformy Azure (lub pobrać je bezpośrednio do maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="0da2a-187">Simply download the `.ipynb` files from the site and upload them onto the dashboard of your notebook Azure VM (or download them directly into the VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="0da2a-188">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="0da2a-188">Conclusion</span></span>
<span data-ttu-id="0da2a-189">Notesu Jupyter zapewnia zaawansowany interfejs do uzyskiwania dostępu do interaktywnego zasilania ekosystemu języka Python na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0da2a-189">The Jupyter Notebook provides a powerful interface for accessing interactively the power of the Python ecosystem on Azure.</span></span>  <span data-ttu-id="0da2a-190">Obejmuje ona szeroką gamę przypadków użycia w tym proste eksploracji i Nauka języka Python, analizy danych i wizualizacji, symulacji oraz przetwarzania równoległego.</span><span class="sxs-lookup"><span data-stu-id="0da2a-190">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="0da2a-191">Wynikowa dokumenty notesu zawierają pełny rekord obliczeń, które są wykonywane i może być współużytkowane z innymi użytkownikami Jupyter.</span><span class="sxs-lookup"><span data-stu-id="0da2a-191">The resulting Notebook documents contain a complete record of the computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="0da2a-192">Notesu Jupyter mogą być używane jako lokalnych aplikacji, ale najlepiej nadaje się do wdrożenia w chmurze na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0da2a-192">The Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="0da2a-193">Są także dostępne w programie Visual Studio za pomocą podstawowych funkcji oprogramowania Jupyter [narzędzi Python Tools for Visual Studio] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="0da2a-193">The core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="0da2a-194">PTVS to bezpłatny i wtyczki firmy Microsoft, które włącza Visual Studio do zaawansowanego środowiska programowania Python obejmuje Zaawansowany edytor z funkcji IntelliSense, debugowania, profilowania i równoległych open source obliczeniowych integracji.</span><span class="sxs-lookup"><span data-stu-id="0da2a-194">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0da2a-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0da2a-195">Next steps</span></span>
<span data-ttu-id="0da2a-196">Więcej informacji możesz znaleźć w [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="0da2a-196">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
