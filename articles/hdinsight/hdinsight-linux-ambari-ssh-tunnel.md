---
title: "Używanie protokołu SSH tunneling można uzyskać dostępu do usługi Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak bezpiecznie przeglądać zasobów sieci web znajdujących się na węzły HDInsight opartych na systemie Linux za pomocą tunelu SSH."
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
ms.openlocfilehash: 4b606ea3797d685b9deacf72f1bd31e0ef007f98
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="34c7a-103">Użyj tunelowania SSH, aby uzyskać dostęp do interfejsu użytkownika sieci web Ambari, JobHistory, NameNode, Oozie i innych sieci web UI</span><span class="sxs-lookup"><span data-stu-id="34c7a-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="34c7a-104">Klastry usługi HDInsight opartej na systemie Linux zapewniają dostęp do interfejsu użytkownika sieci web Ambari w Internecie, ale nie są niektóre funkcje interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="34c7a-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="34c7a-105">Na przykład interfejsu użytkownika sieci web dla innych usług, które są udostępniane za pośrednictwem narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="34c7a-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="34c7a-106">Aby uzyskać pełną funkcjonalność interfejsu użytkownika sieci web Ambari należy użyć tunelu SSH nagłówek klastra.</span><span class="sxs-lookup"><span data-stu-id="34c7a-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="34c7a-107">Dlaczego warto korzystać z tunelowania SSH</span><span class="sxs-lookup"><span data-stu-id="34c7a-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="34c7a-108">Tylko kilka Ambari menu pracy za pośrednictwem tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="34c7a-108">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="34c7a-109">Tych menu korzystają z witryny sieci web i usług działających na inne typy węzłów, takich jak węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="34c7a-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="34c7a-110">Często tych witryn sieci web nie są zabezpieczone, więc nie można bezpiecznie udostępnić je bezpośrednio w Internecie.</span><span class="sxs-lookup"><span data-stu-id="34c7a-110">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span>

<span data-ttu-id="34c7a-111">Następujące UI sieci Web wymagają tunelu SSH:</span><span class="sxs-lookup"><span data-stu-id="34c7a-111">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="34c7a-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="34c7a-112">JobHistory</span></span>
* <span data-ttu-id="34c7a-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="34c7a-113">NameNode</span></span>
* <span data-ttu-id="34c7a-114">Stosy wątków</span><span class="sxs-lookup"><span data-stu-id="34c7a-114">Thread Stacks</span></span>
* <span data-ttu-id="34c7a-115">Oozie interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="34c7a-115">Oozie web UI</span></span>
* <span data-ttu-id="34c7a-116">Główna baza danych HBase i dzienniki interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="34c7a-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="34c7a-117">Jeśli akcji skryptu można użyć do dostosowania z klastrem, usługi lub narzędzi, które można zainstalować z użyciem interfejsu użytkownika sieci web wymagają tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="34c7a-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="34c7a-118">Na przykład po zainstalowaniu aplikacji Hue za pomocą akcji skryptu, można użyć tunelu SSH dostępu do sieci web aplikacji Hue interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="34c7a-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34c7a-119">Jeśli masz bezpośredni dostęp do usługi HDInsight za pośrednictwem sieci wirtualnej jest konieczne używanie tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="34c7a-119">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="34c7a-120">Przykład bezpośredni dostęp do usługi HDInsight za pośrednictwem sieci wirtualnej, zobacz [HDInsight połączyć się z siecią lokalną](connect-on-premises-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-120">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="34c7a-121">Co to jest tunelu SSH</span><span class="sxs-lookup"><span data-stu-id="34c7a-121">What is an SSH tunnel</span></span>

<span data-ttu-id="34c7a-122">[Secure Shell (SSH) tunelowania](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) kieruje ruch wysyłany do znajdującego się na lokalnej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="34c7a-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation.</span></span> <span data-ttu-id="34c7a-123">Ruch jest kierowany przez połączenie SSH do węzła głównego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34c7a-123">The traffic is routed through an SSH connection to your HDInsight cluster head node.</span></span> <span data-ttu-id="34c7a-124">Żądanie zostanie rozwiązany, tak jakby jego występowania w węźle głównym.</span><span class="sxs-lookup"><span data-stu-id="34c7a-124">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="34c7a-125">Odpowiedź jest następnie kierowane wstecz przez tunel do stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="34c7a-125">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34c7a-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="34c7a-126">Prerequisites</span></span>

* <span data-ttu-id="34c7a-127">Klient SSH.</span><span class="sxs-lookup"><span data-stu-id="34c7a-127">An SSH client.</span></span> <span data-ttu-id="34c7a-128">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="34c7a-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="34c7a-129">Przeglądarka sieci web, które mogą być skonfigurowane do korzystania z serwera proxy SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="34c7a-129">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="34c7a-130">Obsługa serwera proxy SOCKS wbudowanych w system Windows nie obsługuje SOCKS5 i nie działa z kroki opisane w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="34c7a-130">The SOCKS proxy support built into Windows does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="34c7a-131">Następujące przeglądarki zależą od ustawień serwera proxy systemu Windows i obecnie nie współpracujesz z kroki opisane w tym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="34c7a-131">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="34c7a-132">Przeglądarka Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="34c7a-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="34c7a-133">Program Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="34c7a-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="34c7a-134">Google Chrome również korzysta z ustawień serwera proxy systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="34c7a-134">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="34c7a-135">Można jednak zainstalować rozszerzenia, które obsługują SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="34c7a-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="34c7a-136">Firma Microsoft zaleca [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="34c7a-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="34c7a-137"><a name="usessh"></a>Tworzenie tunelu przy użyciu polecenia SSH</span><span class="sxs-lookup"><span data-stu-id="34c7a-137"><a name="usessh"></a>Create a tunnel using the SSH command</span></span>

<span data-ttu-id="34c7a-138">Użyj tunelowania następujące polecenie, aby utworzyć SSH za pomocą `ssh` polecenia.</span><span class="sxs-lookup"><span data-stu-id="34c7a-138">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="34c7a-139">Zastąp **USERNAME** użytkownika SSH dla klastra usługi HDInsight i Zastąp **CLUSTERNAME** o nazwie z klastrem usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="34c7a-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="34c7a-140">To polecenie tworzy połączenie kieruje ruchem do portu lokalnego 9876 do klastra za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="34c7a-140">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="34c7a-141">Dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="34c7a-141">The options are:</span></span>

* <span data-ttu-id="34c7a-142">**D 9876** — port lokalny, który przekierowuje ruch za pośrednictwem tunelu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-142">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="34c7a-143">**C** -Kompresuj wszystkich danych, ponieważ ruchu w sieci web jest przeważnie tekstu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="34c7a-144">**2** -force SSH próby tylko w wersji 2 protokołu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-144">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="34c7a-145">**q** — tryb cichy.</span><span class="sxs-lookup"><span data-stu-id="34c7a-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="34c7a-146">**T** — Wyłącz pseudo-tty alokacji, ponieważ będziemy są po prostu przekazywania portu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="34c7a-147">**n**— Wartość pola Zapobiegaj odczytu STDIN, ponieważ będziemy są po prostu przekazywania portu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="34c7a-148">**N** -nie wykonuj polecenia zdalnego, ponieważ będziemy są po prostu przekazywania portu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="34c7a-149">**f** -uruchomione w tle.</span><span class="sxs-lookup"><span data-stu-id="34c7a-149">**f** - Run in the background.</span></span>

<span data-ttu-id="34c7a-150">Po zakończeniu działania polecenia ruch wysyłany do portu 9876 na komputerze lokalnym jest przekierowywane do węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="34c7a-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <span data-ttu-id="34c7a-151"><a name="useputty"></a>Tworzenie tunelu przy użyciu programu PuTTY</span><span class="sxs-lookup"><span data-stu-id="34c7a-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="34c7a-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) graficznego klienta SSH dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="34c7a-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="34c7a-153">Poniższe kroki umożliwiają utworzenie tunelu SSH przy użyciu programu PuTTY:</span><span class="sxs-lookup"><span data-stu-id="34c7a-153">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="34c7a-154">Otwórz program PuTTY i wprowadzić informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="34c7a-155">Jeśli nie masz doświadczenia w obsłudze programu PuTTY, zobacz [programu PuTTY dokumentacji (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="34c7a-155">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="34c7a-156">W **kategorii** z lewej strony okna dialogowego, rozwiń **połączenia**, rozwiń węzeł **SSH**, a następnie wybierz **tuneli**.</span><span class="sxs-lookup"><span data-stu-id="34c7a-156">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="34c7a-157">Podaj następujące informacje w **przekierowanie portów opcje kontrolujące SSH** formularza:</span><span class="sxs-lookup"><span data-stu-id="34c7a-157">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="34c7a-158">**Source port** (Port źródłowy) — port na komputerze klienckim, który ma być przekierowany.</span><span class="sxs-lookup"><span data-stu-id="34c7a-158">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="34c7a-159">Na przykład **9876**.</span><span class="sxs-lookup"><span data-stu-id="34c7a-159">For example, **9876**.</span></span>

   * <span data-ttu-id="34c7a-160">**Docelowy** — adres SSH dla klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="34c7a-160">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="34c7a-161">Na przykład **mójklaster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="34c7a-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="34c7a-162">**Dynamic** (Dynamiczny) — umożliwia dynamiczny routing serwera proxy SOCKS.</span><span class="sxs-lookup"><span data-stu-id="34c7a-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![Obraz tunelowania opcje](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="34c7a-164">Kliknij przycisk **Dodaj** dodać ustawienia, a następnie kliknij przycisk **Otwórz** można otworzyć połączenia SSH.</span><span class="sxs-lookup"><span data-stu-id="34c7a-164">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="34c7a-165">Po wyświetleniu monitu zaloguj się do serwera.</span><span class="sxs-lookup"><span data-stu-id="34c7a-165">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="34c7a-166">Użyj tunelu z przeglądarki</span><span class="sxs-lookup"><span data-stu-id="34c7a-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34c7a-167">Kroki opisane w tej sekcji Korzystanie z przeglądarki Mozilla FireFox, ponieważ zapewnia te same ustawienia serwera proxy na wszystkich platformach.</span><span class="sxs-lookup"><span data-stu-id="34c7a-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="34c7a-168">Inne nowoczesne przeglądarki, takich jak Google Chrome, mogą wymagać rozszerzenia, takie jak FoxyProxy do pracy z tunelu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="34c7a-169">Skonfiguruj przeglądarkę, aby użyć **localhost** i port używany podczas tworzenia tunelu jako **SOCKS v5** serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="34c7a-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="34c7a-170">Poniżej przedstawiono wygląd ustawienia przeglądarki Firefox.</span><span class="sxs-lookup"><span data-stu-id="34c7a-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="34c7a-171">Jeśli użyto innego portu niż 9876 zmienić port ten, który został użyty:</span><span class="sxs-lookup"><span data-stu-id="34c7a-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![Obraz ustawień przeglądarki Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="34c7a-173">Wybieranie **DNS zdalnego** rozpoznaje żądania systemu nazw domen (DNS, Domain Name System) przy użyciu klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34c7a-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="34c7a-174">To ustawienie jest rozpoznawany jako DNS za pomocą węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="34c7a-174">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="34c7a-175">Sprawdź, czy tunelu działa odwiedzając witrynę, takich jak [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="34c7a-175">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="34c7a-176">Adres IP zwrócony powinien być używany przez centrum danych Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="34c7a-176">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="34c7a-177">Weryfikacja Ambari web UI</span><span class="sxs-lookup"><span data-stu-id="34c7a-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="34c7a-178">Po ustanowieniu klastra, wykonaj następujące kroki, aby sprawdzić, czy są dostępne usługi sieci web UI sieci Ambari Web:</span><span class="sxs-lookup"><span data-stu-id="34c7a-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="34c7a-179">W przeglądarce przejdź do http://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="34c7a-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="34c7a-180">`headnodehost` Adres są wysyłane za pośrednictwem tunelu do klastra i Rozwiąż, aby headnode, uruchomionym Ambari.</span><span class="sxs-lookup"><span data-stu-id="34c7a-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="34c7a-181">Po wyświetleniu monitu wprowadź nazwę użytkownika admin (Administrator) i hasło dla klastra.</span><span class="sxs-lookup"><span data-stu-id="34c7a-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="34c7a-182">Może pojawić się prośba po raz drugi przez interfejs użytkownika sieci web Ambari.</span><span class="sxs-lookup"><span data-stu-id="34c7a-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="34c7a-183">Jeśli tak, należy ponownie wprowadzić informacje.</span><span class="sxs-lookup"><span data-stu-id="34c7a-183">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="34c7a-184">Połącz się z klastrem za pomocą adresu http://headnodehost:8080, jest nawiązywane za pośrednictwem tunelu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="34c7a-185">Komunikacja jest zabezpieczone przy użyciu tunelu SSH, a nie protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="34c7a-185">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="34c7a-186">Aby połączyć się przez internet przy użyciu protokołu HTTPS, należy użyć https://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="34c7a-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="34c7a-187">Z poziomu interfejsu użytkownika sieci Web Ambari wybierz system plików HDFS z listy po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="34c7a-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![Obraz o wybrany system plików HDFS](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="34c7a-189">Podczas wyświetlania informacji usług systemu plików HDFS wybierz **szybkie linki**.</span><span class="sxs-lookup"><span data-stu-id="34c7a-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="34c7a-190">Zostanie wyświetlona lista głównymi węzłami klastra.</span><span class="sxs-lookup"><span data-stu-id="34c7a-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="34c7a-191">Wybierz jeden z węzłów głównych, a następnie wybierz **interfejsu użytkownika NameNode**.</span><span class="sxs-lookup"><span data-stu-id="34c7a-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![Obraz menu QuickLinks rozwinięty](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="34c7a-193">Po wybraniu __szybkie linki__, mogą wystąpić wskaźnik oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="34c7a-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="34c7a-194">Ten stan może wystąpić, jeśli masz wolne połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="34c7a-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="34c7a-195">Zaczekaj minutę lub dwie danych z serwera, a następnie spróbuj ponownie listy.</span><span class="sxs-lookup"><span data-stu-id="34c7a-195">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="34c7a-196">Niektóre wpisy w **szybkie linki** menu mogą obcięty z prawej strony ekranu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-196">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="34c7a-197">Jeśli tak, rozwiń menu za pomocą myszy, a następnie użyj klawisza Strzałka w prawo, aby przewiń ekran w prawo, aby zobaczyć pozostałą część menu.</span><span class="sxs-lookup"><span data-stu-id="34c7a-197">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="34c7a-198">Wyświetlane są stronę podobną do poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="34c7a-198">A page similar to the following image is displayed:</span></span>

    ![Obraz NameNode interfejsu użytkownika](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="34c7a-200">Zwróć uwagę, adres URL dla tej strony; powinna być podobna do **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/klaster**.</span><span class="sxs-lookup"><span data-stu-id="34c7a-200">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="34c7a-201">Ten identyfikator URI węzła przy użyciu wewnętrznego pełną nazwę domeny (FQDN) i jest dostępny tylko przy użyciu tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="34c7a-201">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34c7a-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34c7a-202">Next steps</span></span>

<span data-ttu-id="34c7a-203">Teraz, kiedy znasz sposobu tworzenia i używania tunelu SSH, można znaleźć w dokumencie następujące inne sposoby używania narzędzia Ambari:</span><span class="sxs-lookup"><span data-stu-id="34c7a-203">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="34c7a-204">Zarządzanie klastrami usługi HDInsight przy użyciu Ambari</span><span class="sxs-lookup"><span data-stu-id="34c7a-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="34c7a-205">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="34c7a-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

