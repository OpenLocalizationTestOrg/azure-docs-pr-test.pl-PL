---
title: aaaLinux i Open Source przetwarzania na platformie Azure | Dokumentacja firmy Microsoft
description: "Zawiera listę systemów Linux i obliczanie Open Source artykułów na platformie Azure, w tym podstawowe użycie systemu Linux, niektóre podstawowe pojęcia związane z uruchamianiem lub przesyłania obrazów systemu Linux platformy Azure i inne informacje dotyczące określonych technologii i optymalizacje."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: a7e608b5-26ea-41e0-b46b-1a483a257754
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/27/2016
ms.author: rasquill
ms.openlocfilehash: 3ce0dcc65f28d0dddb29f654409f6dae56213bc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a>Zasoby obliczeniowe systemu Linux i typu open-source na platformie Azure
Znajdź całą dokumentację hello muszą toocreate i zarządzanie nimi opartych na systemie Linux maszyn wirtualnych w hello klasycznego modelu wdrażania.

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

## <a name="get-started"></a>Wprowadzenie
* [Wprowadzenie dla systemu Linux na platformie Azure](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Często zadawane pytania dotyczące maszyn wirtualnych Azure utworzonych za pomocą hello klasycznego modelu wdrażania](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Informacje o obrazach dla maszyn wirtualnych](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Przekazywanie obrazu Distro](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (a także instrukcje przy użyciu [dystrybucji Azure-Endorsed](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))
* [Zaloguj się na tooa hello maszynę Wirtualną systemu Linux przy użyciu klasycznego portalu Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a>Konfigurowanie
* [Zainstaluj Azure interfejsu wiersza polecenia (Azure CLI)](../../cli-install-nodejs.md)

## <a name="tutorials"></a>Samouczki
* [Zainstaluj hello stosu światła na maszynie wirtualnej systemu Linux na platformie Azure](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ruby w aplikacji sieci Web szyny na maszynie Wirtualnej platformy Azure](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [Porady: Instalowanie Apache Qpid protonów C dla protokołu AMQP i usługi Service Bus](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a>Bazy danych
* [Optymalizacji wydajności bazy danych MySQL na platformie Azure](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Klastry MySQL](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Uruchamianie Cassandra z systemem Linux na platformie Azure i uzyskiwania dostępu do w oprogramowaniu Node.js](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tworzenie klastra wieloma serwerami głównymi MariaDbs](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a>HPC
* [Rozpoczynanie pracy z węzłów obliczeniowych systemu Linux w klastrze HPC Pack na platformie Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Uruchamianie NAMD z pakietem Microsoft HPC w węzłach obliczeń systemu Linux na platformie Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Skonfiguruj aplikacje MPI toorun Linux RDMA klastra](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a>Docker
* [Przy użyciu hello Docker rozszerzenia maszyny Wirtualnej z hello interfejsu wiersza polecenia platformy Azure (Azure CLI)](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Przy użyciu hello Docker rozszerzenia maszyny Wirtualnej z hello portalu Azure](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Jak toouse komputera docker na platformie Azure](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a>Ubuntu
* [Porady: MySQL klastrów](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Porady: Node.js i Cassandra](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a>OpenSUSE
* [Porady: Instalowanie i uruchamianie MySQL](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a>CoreOS
* [Porady: Użyj CoreOS na platformie Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a>Planowanie
* [Wytyczne dotyczące implementacji usług infrastruktury platformy Azure](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Wybieranie nazwy użytkowników systemu Linux](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Jak tooconfigure, zbiór dostępności, dla maszyn wirtualnych w hello klasycznego modelu wdrażania](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Jak tooSchedule konserwacji zaplanowane na maszynach wirtualnych Azure](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Zarządzanie hello dostępność maszyn wirtualnych](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planowana Konserwacja maszyn wirtualnych systemu Linux na platformie Azure](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a>Wdrożenie
* [Utwórz niestandardowe maszynę wirtualną z systemem Linux](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Witaj podstawy: Przechwytywanie maszyny Wirtualnej systemu Linux tooMake szablonu](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Informacje dotyczące niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a>Zarządzanie
* [SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Jak tooReset hasła lub właściwości SSH dla systemu Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Przy użyciu głównego](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a>Zasoby platformy Azure
* [Hello Azure agenta systemu Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Maszyna wirtualna platformy Azure rozszerzeń i funkcji](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Wstrzykiwania danych niestandardowych do toouse maszyny Wirtualnej z inicjowaniem chmury](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a>Magazyn
* [Dołączanie tooa dysku danych maszyny Wirtualnej systemu Linux](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Odłączanie dysku danych maszyny wirtualnej systemu Linux](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Sieć
* [Jak tooset się punkty końcowe w klasycznym maszyny wirtualnej platformy Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
* [Rozwiązywanie problemów z Secure Shell (SSH) połączeń tooa opartych na systemie Linux maszyny wirtualnej platformy Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Rozwiązywanie problemów wdrożenie klasyczne z Tworzenie nowej maszyny wirtualnej systemu Linux na platformie Azure](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [Rozwiązywanie problemów wdrożenie klasyczne z ponownym uruchomieniem lub zmieniania rozmiaru istniejącej maszyny wirtualnej systemu Linux na platformie Azure](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a>Dokumentacja
* [Azure polecenia interfejsu wiersza polecenia w trybie Azure Service Management (asm)](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Usługa Azure Service Management REST API](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a>Ogólne łącza
Witaj następującego łącza są przeznaczone dla Microsoft blogów, stron w witrynie Technet i zewnętrznych witryn zamiast dokumentacji w witrynie Azure.com jak powyżej. Jako zarówno Azure i hello world obliczeniowych open source fast przenosisz elementy docelowe, jest prawie, hello następujące łącza są nieaktualne, *pomimo* fakt hello możemy dokonują nasze najlepsze toocontinually Dodawanie nowszej tematy i usuwanie nieaktualne z nich. Jeśli firma Microsoft zostało pominięte jedną, sprawdź Daj nam znać w komentarzach hello lub Prześlij tooour żądania ściągnięcia [repozytorium GitHub](https://github.com/Azure/azure-content/).

* [Uruchomiony ASP.NET 5 w systemie Linux przy użyciu rozwiązania Docker kontenerów](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [Jak tooDeploy obraz maszyny Wirtualnej CentOS z OpenLogic](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [SUSE aktualizacji infrastruktury](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [SUSE Linux Enterprise Server dla programu SAP chmury urządzenia biblioteki](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [Tworzenie wysokiej dostępności systemu Linux na platformie Azure w krokach 12](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [Inicjowanie obsługi administracyjnej systemu Linux na platformie Azure przy użyciu wiersza polecenia platformy Azure, node.js, jhawk automatyzacji](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [GlusterFS na platformie Azure](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a>FreeBSD
* [Uruchomione FreeBSD na platformie Azure](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [Łatwe wdrażanie FreeBSD](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [Wdrażanie dostosowanego obrazu FreeBSD](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [Kaspersky AV dla serwera plików systemu Linux](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a>NoSQL
* [8 bazy danych NoSql open source dla platformy Azure](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [Slideshare (MSOpenTech):, Korzystając z CouchDb na platformie Azure](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [Uruchomiona CouchDB jako — usługa node.js, CORS i Grunt](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [Redis w systemie Windows w hello usługi pamięć podręczna Redis Azure](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [Anonsowanie dostawcę stanu sesji ASP.NET dla pamięci podręcznej Redis wersji zapoznawczej](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [Blog: RavenHQ teraz dostępne w hello Azure Marketplace](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a>Duże ilości danych
* [Instalowanie usługi Hadoop na maszynach wirtualnych systemu Linux platformy Azure](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [Usługa Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a>Relacyjna baza danych
* [Architektura dostępności wysokiej MySQL na platformie Microsoft Azure](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [Instalowanie Postgres z corosync, pg_bouncer przy użyciu ILB](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a>Linux wysokiej wydajności (HPC) obliczeniowych
* [Szablon szybkiego startu: aż klastra SLURM](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (i [wpis w blogu](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))
* [Szablon Szybki Start: Tworzenie klastra HPC z węzłami obliczeniowymi systemu Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a>Devops, zarządzania i optymalizacji
Jako hello world opracowywania oprogramowania, zarządzania i optymalizacja jest dość rozszerzania i zmiana bardzo szybko, które należy rozważyć listy hello poniżej punkt początkowy.

* [Wideo: Maszyn wirtualnych platformy Azure: przy użyciu Chef, Puppet i Docker zarządzania maszyn wirtualnych systemu Linux](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [Ukończenie wdrożenia klastra Kubernetes tooautomated przewodnik CoreOS i splot](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Podrzędny Wpięć wtyczki dla platformy Azure](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [Repozytorium GitHub: Wtyczka magazynu rozwiązania Jenkins dla platformy Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [Inna firma: Wtyczka podrzędna rozwiązania Hudson dla platformy Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [Inna firma: Wtyczka magazynu rozwiązania Hudson dla platformy Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Wideo: Co to jest Chef i jak działa?](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [Wideo: Jak tooUse usługi Automatyzacja Azure z maszyn wirtualnych systemu Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [Blog: Jak toodo DSC środowiska Powershell dla systemu Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [GitHub: Rozszerzenie DSC klienta platformy Docker](https://github.com/anweiss/DockerClientDSC)
* [Dodatek pakujący dla platformy Azure](https://github.com/msopentech/packer-azure)

