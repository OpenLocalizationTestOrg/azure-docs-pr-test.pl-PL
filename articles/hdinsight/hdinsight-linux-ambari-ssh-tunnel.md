---
title: "tunelowania SSH aaaUse — tooaccess Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse toosecurely tunelu SSH Przeglądaj zasobów sieci web znajdujących się na węzły HDInsight opartych na systemie Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="08543-103">Użyj tunelowania SSH tooaccess interfejsu użytkownika sieci web Ambari, JobHistory, NameNode, Oozie i innych sieci web UI</span><span class="sxs-lookup"><span data-stu-id="08543-103">Use SSH Tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="08543-104">Klastry usługi HDInsight opartej na systemie Linux zapewniają dostęp tooAmbari interfejsu użytkownika sieci web za pośrednictwem Internetu hello, ale niektóre funkcje hello interfejsu użytkownika nie są.</span><span class="sxs-lookup"><span data-stu-id="08543-104">Linux-based HDInsight clusters provide access tooAmbari web UI over hello Internet, but some features of hello UI are not.</span></span> <span data-ttu-id="08543-105">Na przykład hello interfejsu użytkownika sieci web dla innych usług, które są udostępniane za pośrednictwem narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="08543-105">For example, hello web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="08543-106">Funkcje programu hello interfejsu użytkownika sieci web Ambari należy użyć SSH tunelu toohello klastra head.</span><span class="sxs-lookup"><span data-stu-id="08543-106">For full functionality of hello Ambari web UI, you must use an SSH tunnel toohello cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="08543-107">Dlaczego warto korzystać z tunelowania SSH</span><span class="sxs-lookup"><span data-stu-id="08543-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="08543-108">Tylko kilka Ambari hello menu pracy za pośrednictwem tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="08543-108">Several of hello menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="08543-109">Tych menu korzystają z witryny sieci web i usług działających na inne typy węzłów, takich jak węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="08543-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="08543-110">Często tych witryn sieci web nie są zabezpieczone, więc nie toodirectly bezpieczne Uwidacznianie hello je na internet.</span><span class="sxs-lookup"><span data-stu-id="08543-110">Often, these web sites are not secured, so it is not safe toodirectly expose them on hello internet.</span></span>

<span data-ttu-id="08543-111">powitania po UI sieci Web wymagają tunelu SSH:</span><span class="sxs-lookup"><span data-stu-id="08543-111">hello following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="08543-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="08543-112">JobHistory</span></span>
* <span data-ttu-id="08543-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="08543-113">NameNode</span></span>
* <span data-ttu-id="08543-114">Stosy wątków</span><span class="sxs-lookup"><span data-stu-id="08543-114">Thread Stacks</span></span>
* <span data-ttu-id="08543-115">Oozie interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="08543-115">Oozie web UI</span></span>
* <span data-ttu-id="08543-116">Główna baza danych HBase i dzienniki interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="08543-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="08543-117">Jeśli używasz toocustomize akcji skryptu klastra żadnych usług ani narzędzi, które można zainstalować z użyciem interfejsu użytkownika sieci web wymagają tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="08543-117">If you use Script Actions toocustomize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="08543-118">Na przykład po zainstalowaniu aplikacji Hue za pomocą akcji skryptu, należy użyć SSH tunelu tooaccess hello Hue interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="08543-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel tooaccess hello Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08543-119">Jeśli masz tooHDInsight bezpośredni dostęp do sieci wirtualnej, nie trzeba toouse tuneli SSH.</span><span class="sxs-lookup"><span data-stu-id="08543-119">If you have direct access tooHDInsight through a virtual network, you do not need toouse SSH tunnels.</span></span> <span data-ttu-id="08543-120">Przykład bezpośredni dostęp do usługi HDInsight za pośrednictwem sieci wirtualnej, zobacz hello [sieć lokalną tooyour połączyć HDInsight](connect-on-premises-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="08543-120">For an example of directly accessing HDInsight through a virtual network, see hello [Connect HDInsight tooyour on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="08543-121">Co to jest tunelu SSH</span><span class="sxs-lookup"><span data-stu-id="08543-121">What is an SSH tunnel</span></span>

<span data-ttu-id="08543-122">[Secure Shell (SSH) tunelowania](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) kieruje ruch przesyłany portu tooa na lokalnej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="08543-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent tooa port on your local workstation.</span></span> <span data-ttu-id="08543-123">Witaj, ruch jest kierowany przez SSH połączenia tooyour HDInsight węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="08543-123">hello traffic is routed through an SSH connection tooyour HDInsight cluster head node.</span></span> <span data-ttu-id="08543-124">Żądanie hello jest rozwiązywany tak, jakby pochodziły hello węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="08543-124">hello request is resolved as if it originated on hello head node.</span></span> <span data-ttu-id="08543-125">odpowiedź Hello jest następnie kierowane za pośrednictwem stacji roboczej tooyour tunelu hello.</span><span class="sxs-lookup"><span data-stu-id="08543-125">hello response is then routed back through hello tunnel tooyour workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08543-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="08543-126">Prerequisites</span></span>

* <span data-ttu-id="08543-127">Klient SSH.</span><span class="sxs-lookup"><span data-stu-id="08543-127">An SSH client.</span></span> <span data-ttu-id="08543-128">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="08543-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="08543-129">Przeglądarki sieci web, które mogą być skonfigurowane toouse SOCKS5 serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="08543-129">A web browser that can be configured toouse a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="08543-130">Obsługa serwera proxy SOCKS Hello wbudowanych w system Windows nie obsługuje SOCKS5 i nie działa z hello kroków w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="08543-130">hello SOCKS proxy support built into Windows does not support SOCKS5, and does not work with hello steps in this document.</span></span> <span data-ttu-id="08543-131">Witaj następujące przeglądarki zależą od ustawień serwera proxy systemu Windows, a nie obecnie pracy hello kroków w tym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="08543-131">hello following browsers rely on Windows proxy settings, and do not currently work with hello steps in this document:</span></span>
    >
    > * <span data-ttu-id="08543-132">Przeglądarka Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="08543-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="08543-133">Program Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="08543-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="08543-134">Google Chrome również zależy od ustawień serwera proxy systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="08543-134">Google Chrome also relies on hello Windows proxy settings.</span></span> <span data-ttu-id="08543-135">Można jednak zainstalować rozszerzenia, które obsługują SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="08543-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="08543-136">Firma Microsoft zaleca [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="08543-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="08543-137"><a name="usessh"></a>Tworzenie tunelu przy użyciu polecenia SSH hello</span><span class="sxs-lookup"><span data-stu-id="08543-137"><a name="usessh"></a>Create a tunnel using hello SSH command</span></span>

<span data-ttu-id="08543-138">Użyj hello następujące polecenie toocreate tunelu SSH za pomocą hello `ssh` polecenia.</span><span class="sxs-lookup"><span data-stu-id="08543-138">Use hello following command toocreate an SSH tunnel using hello `ssh` command.</span></span> <span data-ttu-id="08543-139">Zastąp **USERNAME** użytkownika SSH dla klastra usługi HDInsight i Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="08543-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="08543-140">To polecenie tworzy połączenia, który przekierowuje ruch toolocal portu 9876 toohello klastra za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="08543-140">This command creates a connection that routes traffic toolocal port 9876 toohello cluster over SSH.</span></span> <span data-ttu-id="08543-141">dostępne są opcje Hello:</span><span class="sxs-lookup"><span data-stu-id="08543-141">hello options are:</span></span>

* <span data-ttu-id="08543-142">**D 9876** — Witaj port lokalny, który przekierowuje ruch za pośrednictwem tunelu hello.</span><span class="sxs-lookup"><span data-stu-id="08543-142">**D 9876** - hello local port that routes traffic through hello tunnel.</span></span>
* <span data-ttu-id="08543-143">**C** -Kompresuj wszystkich danych, ponieważ ruchu w sieci web jest przeważnie tekstu.</span><span class="sxs-lookup"><span data-stu-id="08543-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="08543-144">**2** -force SSH tootry protocol w wersji 2 tylko.</span><span class="sxs-lookup"><span data-stu-id="08543-144">**2** - Force SSH tootry protocol version 2 only.</span></span>
* <span data-ttu-id="08543-145">**q** — tryb cichy.</span><span class="sxs-lookup"><span data-stu-id="08543-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="08543-146">**T** — Wyłącz pseudo-tty alokacji, ponieważ będziemy są po prostu przekazywania portu.</span><span class="sxs-lookup"><span data-stu-id="08543-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="08543-147">**n**— Wartość pola Zapobiegaj odczytu STDIN, ponieważ będziemy są po prostu przekazywania portu.</span><span class="sxs-lookup"><span data-stu-id="08543-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="08543-148">**N** -nie wykonuj polecenia zdalnego, ponieważ będziemy są po prostu przekazywania portu.</span><span class="sxs-lookup"><span data-stu-id="08543-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="08543-149">**f** -wykonywane w tle hello.</span><span class="sxs-lookup"><span data-stu-id="08543-149">**f** - Run in hello background.</span></span>

<span data-ttu-id="08543-150">Po zakończeniu działania polecenia hello ruch wysyłany tooport 9876 na komputerze lokalnym hello jest kierowany toohello węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="08543-150">Once hello command finishes, traffic sent tooport 9876 on hello local computer is routed toohello cluster head node.</span></span>

## <span data-ttu-id="08543-151"><a name="useputty"></a>Tworzenie tunelu przy użyciu programu PuTTY</span><span class="sxs-lookup"><span data-stu-id="08543-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="08543-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) graficznego klienta SSH dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="08543-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="08543-153">Użyj hello następujące kroki toocreate tunelu SSH przy użyciu programu PuTTY:</span><span class="sxs-lookup"><span data-stu-id="08543-153">Use hello following steps toocreate an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="08543-154">Otwórz program PuTTY i wprowadzić informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="08543-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="08543-155">Jeśli nie masz doświadczenia w obsłudze programu PuTTY, zobacz hello [programu PuTTY dokumentacji (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="08543-155">If you are not familiar with PuTTY, see hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="08543-156">W hello **kategorii** toohello sekcji lewej strony okna dialogowego hello, rozwiń **połączenia**, rozwiń węzeł **SSH**, a następnie wybierz **tuneli**.</span><span class="sxs-lookup"><span data-stu-id="08543-156">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="08543-157">Podaj następujące informacje na powitania hello **przekierowanie portów opcje kontrolujące SSH** formularza:</span><span class="sxs-lookup"><span data-stu-id="08543-157">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="08543-158">**Port źródłowy** — Witaj port na powitania klienta, że chcesz tooforward.</span><span class="sxs-lookup"><span data-stu-id="08543-158">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="08543-159">Na przykład **9876**.</span><span class="sxs-lookup"><span data-stu-id="08543-159">For example, **9876**.</span></span>

   * <span data-ttu-id="08543-160">**Docelowy** — Witaj adres SSH dla klastra usługi HDInsight opartej na systemie Linux hello.</span><span class="sxs-lookup"><span data-stu-id="08543-160">**Destination** - hello SSH address for hello Linux-based HDInsight cluster.</span></span> <span data-ttu-id="08543-161">Na przykład **mójklaster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="08543-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="08543-162">**Dynamic** (Dynamiczny) — umożliwia dynamiczny routing serwera proxy SOCKS.</span><span class="sxs-lookup"><span data-stu-id="08543-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![Obraz tunelowania opcje](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="08543-164">Kliknij przycisk **Dodaj** tooadd hello ustawienia, a następnie kliknij przycisk **Otwórz** tooopen połączenie SSH.</span><span class="sxs-lookup"><span data-stu-id="08543-164">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>

5. <span data-ttu-id="08543-165">Po wyświetleniu monitu zaloguj się na serwerze toohello.</span><span class="sxs-lookup"><span data-stu-id="08543-165">When prompted, log in toohello server.</span></span>

## <a name="use-hello-tunnel-from-your-browser"></a><span data-ttu-id="08543-166">Użyj tunelu hello z przeglądarki</span><span class="sxs-lookup"><span data-stu-id="08543-166">Use hello tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08543-167">Witaj kroki w tej sekcji hello użyj przeglądarki Mozilla FireFox, ponieważ tworzy ona hello tych samych ustawień serwera proxy na wszystkich platformach.</span><span class="sxs-lookup"><span data-stu-id="08543-167">hello steps in this section use hello Mozilla FireFox browser, as it provides hello same proxy settings across all platforms.</span></span> <span data-ttu-id="08543-168">Inne nowoczesne przeglądarki, takich jak Google Chrome, mogą wymagać rozszerzenia, takie jak toowork FoxyProxy z hello tunelu.</span><span class="sxs-lookup"><span data-stu-id="08543-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy toowork with hello tunnel.</span></span>

1. <span data-ttu-id="08543-169">Skonfiguruj hello przeglądarki toouse **localhost** i portu hello używane podczas tworzenia tunelu hello jako **SOCKS v5** serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="08543-169">Configure hello browser toouse **localhost** and hello port you used when creating hello tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="08543-170">Poniżej przedstawiono wygląd hello Firefox ustawienia.</span><span class="sxs-lookup"><span data-stu-id="08543-170">Here's what hello Firefox settings look like.</span></span> <span data-ttu-id="08543-171">Jeśli użyto innego portu niż 9876 zmienić toohello portu hello, używanego jednego:</span><span class="sxs-lookup"><span data-stu-id="08543-171">If you used a different port than 9876, change hello port toohello one you used:</span></span>
   
    ![Obraz ustawień przeglądarki Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="08543-173">Wybieranie **DNS zdalnego** rozpoznaje żądania systemu nazw domen (DNS, Domain Name System) przy użyciu hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="08543-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using hello HDInsight cluster.</span></span> <span data-ttu-id="08543-174">To ustawienie jest rozpoznawany jako DNS za pomocą węzła głównego hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="08543-174">This setting resolves DNS using hello head node of hello cluster.</span></span>

2. <span data-ttu-id="08543-175">Weryfikowanie działania tego tunelu hello odwiedzając witrynę, takich jak [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="08543-175">Verify that hello tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="08543-176">Hello IP zwrócił powinna być jeden używana przez hello Microsoft Azure w centrum danych.</span><span class="sxs-lookup"><span data-stu-id="08543-176">hello IP returned should be one used by hello Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="08543-177">Weryfikacja Ambari web UI</span><span class="sxs-lookup"><span data-stu-id="08543-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="08543-178">Po ustanowieniu hello klastra, użyj hello następujące kroki tooverify, czy są dostępne usługi sieci web UI hello Ambari Web:</span><span class="sxs-lookup"><span data-stu-id="08543-178">Once hello cluster has been established, use hello following steps tooverify that you can access service web UIs from hello Ambari Web:</span></span>

1. <span data-ttu-id="08543-179">W przeglądarce Przejdź toohttp://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="08543-179">In your browser, go toohttp://headnodehost:8080.</span></span> <span data-ttu-id="08543-180">Witaj `headnodehost` adres są wysyłane za pośrednictwem hello tunelu toohello klastra i rozwiązać headnode toohello, który Ambari działa na.</span><span class="sxs-lookup"><span data-stu-id="08543-180">hello `headnodehost` address is sent over hello tunnel toohello cluster and resolve toohello headnode that Ambari is running on.</span></span> <span data-ttu-id="08543-181">Po wyświetleniu monitu wprowadź nazwę użytkownika hello admin (Administrator) i hasło dla klastra.</span><span class="sxs-lookup"><span data-stu-id="08543-181">When prompted, enter hello admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="08543-182">Może pojawić się prośba po raz drugi przez hello Ambari web UI.</span><span class="sxs-lookup"><span data-stu-id="08543-182">You may be prompted a second time by hello Ambari web UI.</span></span> <span data-ttu-id="08543-183">Jeśli tak, należy ponownie wprowadzić informacje o hello.</span><span class="sxs-lookup"><span data-stu-id="08543-183">If so, reenter hello information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="08543-184">Używając hello http://headnodehost:8080 adres tooconnect toohello klastra jest nawiązywane za pośrednictwem tunelu hello.</span><span class="sxs-lookup"><span data-stu-id="08543-184">When using hello http://headnodehost:8080 address tooconnect toohello cluster, you are connecting through hello tunnel.</span></span> <span data-ttu-id="08543-185">Komunikat jest zabezpieczony przy użyciu tunelu SSH hello zamiast protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="08543-185">Communication is secured using hello SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="08543-186">tooconnect ponad hello internet przy użyciu protokołu HTTPS, należy użyć https://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="08543-186">tooconnect over hello internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of hello cluster.</span></span>

2. <span data-ttu-id="08543-187">Hello Interfejsu sieci Web Ambari zaznacz na liście hello na powitania po lewej stronie powitania systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="08543-187">From hello Ambari Web UI, select HDFS from hello list on hello left of hello page.</span></span>

    ![Obraz o wybrany system plików HDFS](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="08543-189">Po wyświetleniu hello informacje o systemie plików HDFS usługi wybierz **szybkie linki**.</span><span class="sxs-lookup"><span data-stu-id="08543-189">When hello HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="08543-190">Zostanie wyświetlona lista hello głównymi węzłami klastra.</span><span class="sxs-lookup"><span data-stu-id="08543-190">A list of hello cluster head nodes appears.</span></span> <span data-ttu-id="08543-191">Wybierz jeden z węzłów głównych hello, a następnie wybierz **interfejsu użytkownika NameNode**.</span><span class="sxs-lookup"><span data-stu-id="08543-191">Select one of hello head nodes, and then select **NameNode UI**.</span></span>

    ![Obraz powitania QuickLinks menu rozwinięty](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="08543-193">Po wybraniu __szybkie linki__, mogą wystąpić wskaźnik oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="08543-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="08543-194">Ten stan może wystąpić, jeśli masz wolne połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="08543-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="08543-195">Zaczekaj minutę lub dwie na toobe danych hello otrzymany z serwera hello, a następnie spróbuj ponownie hello listy.</span><span class="sxs-lookup"><span data-stu-id="08543-195">Wait a minute or two for hello data toobe received from hello server, then try hello list again.</span></span>
   >
   > <span data-ttu-id="08543-196">Niektóre wpisy w hello **szybkie linki** menu może zostać przerwane przez hello prawej krawędzi ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="08543-196">Some entries in hello **Quick Links** menu may be cut off by hello right side of hello screen.</span></span> <span data-ttu-id="08543-197">Jeśli tak, rozwiń menu hello przy użyciu myszy i użyj hello strzałki w prawo klucza tooscroll hello ekranu toohello prawo toosee hello reszty hello menu.</span><span class="sxs-lookup"><span data-stu-id="08543-197">If so, expand hello menu using your mouse and use hello right arrow key tooscroll hello screen toohello right toosee hello rest of hello menu.</span></span>

4. <span data-ttu-id="08543-198">Jest wyświetlana strona toohello podobne, po obrazu:</span><span class="sxs-lookup"><span data-stu-id="08543-198">A page similar toohello following image is displayed:</span></span>

    ![Obraz powitania NameNode interfejsu użytkownika](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="08543-200">Zwróć uwagę, adres URL hello na tej stronie; powinien być podobny zbyt**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/klaster**.</span><span class="sxs-lookup"><span data-stu-id="08543-200">Notice hello URL for this page; it should be similar too**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="08543-201">Ten identyfikator URI używa hello wewnętrzny pełną nazwę domeny (FQDN) węzła hello i jest dostępny tylko przy użyciu tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="08543-201">This URI is using hello internal fully qualified domain name (FQDN) of hello node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08543-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="08543-202">Next steps</span></span>

<span data-ttu-id="08543-203">Teraz, kiedy znasz już toocreate i używania tunelu SSH, zobacz temat powitania po dokumentu do innych metod toouse Ambari:</span><span class="sxs-lookup"><span data-stu-id="08543-203">Now that you have learned how toocreate and use an SSH tunnel, see hello following document for other ways toouse Ambari:</span></span>

* [<span data-ttu-id="08543-204">Zarządzanie klastrami usługi HDInsight przy użyciu Ambari</span><span class="sxs-lookup"><span data-stu-id="08543-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="08543-205">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="08543-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

