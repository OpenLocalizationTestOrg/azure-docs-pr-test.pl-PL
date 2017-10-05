---
title: "Konwertuj WordPress do wdrożenia w wielu lokacjach w usłudze aplikacji Azure"
description: "Dowiedz się, jak wykonać istniejącej aplikacji sieci web WordPress została utworzona za pośrednictwem galerii na platformie Azure i przekształcić ją w wielu lokacjach WordPress"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4a15fb5e97d2ca57e5883c07651c372c54021c92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a><span data-ttu-id="7e100-103">Konwertuj WordPress do wdrożenia w wielu lokacjach w usłudze aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="7e100-103">Convert WordPress to Multisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="7e100-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7e100-104">Overview</span></span>
<span data-ttu-id="7e100-105">*Przez [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="7e100-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="7e100-106">Z tego samouczka dowiesz się, jak wykonać istniejącej aplikacji sieci web WordPress została utworzona za pośrednictwem galerii na platformie Azure oraz przekształcać je do instalacji WordPress wdrożenia w wielu lokacjach.</span><span class="sxs-lookup"><span data-stu-id="7e100-106">In this tutorial, you will learn how to take an existing WordPress web app created through the gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="7e100-107">Ponadto dowiesz jak przypisać niestandardową domenę, wszystkie lokacje podrzędne w ramach instalacji.</span><span class="sxs-lookup"><span data-stu-id="7e100-107">Additionally, you will learn how to assign a custom domain to each of the subsites within your install.</span></span>

<span data-ttu-id="7e100-108">Zakłada się, że masz istniejącą instalację programu WordPress.</span><span class="sxs-lookup"><span data-stu-id="7e100-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="7e100-109">W przeciwnym razie wykonaj wskazówki zamieszczone w [utworzyć witrynę sieci web WordPress z poziomu galerii na platformie Azure][website-from-gallery].</span><span class="sxs-lookup"><span data-stu-id="7e100-109">If you do not, please follow the guidance provided in [Create a WordPress web site from the gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="7e100-110">Konwertowanie istniejących WordPress instalacji jednej lokacji do wdrożenia w wielu lokacjach ogólnie jest dość proste i wiele początkowe kroki pochodzi bezpośrednio z [Utwórz sieć A] [ wordpress-codex-create-a-network] strony na [Kodeksu WordPress](http://codex.wordpress.org).</span><span class="sxs-lookup"><span data-stu-id="7e100-110">Converting an existing WordPress single site install to Multisite is generally fairly simple, and many of the initial steps here come straight from the [Create A Network][wordpress-codex-create-a-network] page on the [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="7e100-111">Zacznijmy od początku.</span><span class="sxs-lookup"><span data-stu-id="7e100-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="7e100-112">Zezwalaj na wdrożenie w wielu lokacjach</span><span class="sxs-lookup"><span data-stu-id="7e100-112">Allow Multisite</span></span>
<span data-ttu-id="7e100-113">Należy najpierw włączyć wdrożenie w wielu lokacjach przy użyciu `wp-config.php` pliku z **WP\_Zezwalaj\_wdrożenia w wielu LOKACJACH** stałej.</span><span class="sxs-lookup"><span data-stu-id="7e100-113">You first need to enable Multisite through the `wp-config.php` file with the **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="7e100-114">Istnieją dwie metody, aby edytować pliki aplikacji sieci web: pierwszy odbywa się za pośrednictwem FTP, a drugi przy użyciu programu Git.</span><span class="sxs-lookup"><span data-stu-id="7e100-114">There are two methods to edit your web app files: the first is through FTP, and the second through Git.</span></span> <span data-ttu-id="7e100-115">Jeśli znasz konfiguracji każdej z tych metod, przeczytaj następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="7e100-115">If you are unfamiliar with how to setup either of these methods, please refer to the following tutorials:</span></span>

* <span data-ttu-id="7e100-116">[Witryny sieci web PHP z MySQL i FTP.][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="7e100-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="7e100-117">[Witryny sieci web PHP, MySQL i Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="7e100-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="7e100-118">Otwórz `wp-config.php` plik w edytorze wybrane i dodaj następującą powyżej `/* That's all, stop editing! Happy blogging. */` wiersza.</span><span class="sxs-lookup"><span data-stu-id="7e100-118">Open the `wp-config.php` file with the editor of your choosing and add the following above the `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="7e100-119">Pamiętaj zapisać plik i przekaż go do serwera!</span><span class="sxs-lookup"><span data-stu-id="7e100-119">Be sure to save the file and upload it back to the server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="7e100-120">Konfiguracja sieci</span><span class="sxs-lookup"><span data-stu-id="7e100-120">Network Setup</span></span>
<span data-ttu-id="7e100-121">Zaloguj się do *wp-admin* obszar aplikacji sieci web i powinien zostać wyświetlony nowy element pod **narzędzia** menu o nazwie **konfiguracja sieci**.</span><span class="sxs-lookup"><span data-stu-id="7e100-121">Log in to the *wp-admin* area of your web app and you should see a new item under the **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="7e100-122">Kliknij przycisk **konfiguracja sieci** i uzupełnij informacje dotyczące sieci.</span><span class="sxs-lookup"><span data-stu-id="7e100-122">Click **Network Setup** and fill in the details of your network.</span></span>

![Ekran konfiguracji sieci][wordpress-network-setup]

<span data-ttu-id="7e100-124">W tym samouczku używana *podkatalogów* lokacji schematu, ponieważ zawsze powinny działać i będą możemy Trwa konfigurowanie domen niestandardowych dla każdej witryny podrzędnej później w samouczku.</span><span class="sxs-lookup"><span data-stu-id="7e100-124">This tutorial uses the *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in the tutorial.</span></span> <span data-ttu-id="7e100-125">Jednak powinno być możliwe Instalatorowi na zainstalowanie poddomeny, jeśli mapowanie domeny przy użyciu [Azure Portal](https://portal.azure.com) i skonfiguruj poprawnie symboli wieloznacznych DNS.</span><span class="sxs-lookup"><span data-stu-id="7e100-125">However, it should be possible to setup a subdomain install if you map a domain through the [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="7e100-126">Więcej informacji na temat wersji programu vs domenę podrzędną podkatalogu konfiguracje dla [typów sieci z wieloma lokacjami] [ wordpress-codex-types-of-networks] artykuł na temat Kodeksu WordPress.</span><span class="sxs-lookup"><span data-stu-id="7e100-126">For more information on sub-domain vs sub-directory setups see the [Types of multisite network][wordpress-codex-types-of-networks] article on the WordPress Codex.</span></span>

## <a name="enable-the-network"></a><span data-ttu-id="7e100-127">Włącz sieci</span><span class="sxs-lookup"><span data-stu-id="7e100-127">Enable the Network</span></span>
<span data-ttu-id="7e100-128">Sieć jest teraz skonfigurowane w bazie danych, ale jest jednym z pozostałych etapów do włączenia funkcji sieci.</span><span class="sxs-lookup"><span data-stu-id="7e100-128">The network is now configured in the database, but there is one remaining step to enable the network functionality.</span></span> <span data-ttu-id="7e100-129">Finalizuj `wp-config.php` ustawienia i upewnij się, `web.config` prawidłowo kieruje każdej lokacji.</span><span class="sxs-lookup"><span data-stu-id="7e100-129">Finalize the `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="7e100-130">Po kliknięciu przycisku **zainstalować** znajdującego się na *konfiguracja sieci* strony zaktualizować podejmie WordPress `wp-config.php` i `web.config` plików.</span><span class="sxs-lookup"><span data-stu-id="7e100-130">After clicking the **Install** button on the *Network Setup* page, WordPress will attempt to update the `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="7e100-131">Jednak należy zawsze sprawdzić pliki, aby upewnić się, że aktualizacje zostały pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="7e100-131">However, you should always check the files to ensure the updates were successful.</span></span> <span data-ttu-id="7e100-132">Jeśli nie, spowoduje wyświetlenie tego ekranu z niezbędne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="7e100-132">If not, this screen will present you with the necessary updates.</span></span> <span data-ttu-id="7e100-133">Edytuj i zapisuj pliki.</span><span class="sxs-lookup"><span data-stu-id="7e100-133">Edit and save the files.</span></span>

<span data-ttu-id="7e100-134">Po wykonaniu tych aktualizacji, musisz się wylogować i zalogować z powrotem do pulpitu nawigacyjnego wp administratora.</span><span class="sxs-lookup"><span data-stu-id="7e100-134">After making these updates you will need to log out and log back into the wp-admin dashboard.</span></span>

<span data-ttu-id="7e100-135">Powinny teraz istnieć dodatkowe menu na pasku administratora z etykietą **witryny**.</span><span class="sxs-lookup"><span data-stu-id="7e100-135">There should now be an additional menu on the admin bar labeled **My Sites**.</span></span> <span data-ttu-id="7e100-136">To menu pozwala na kontrolowanie sieci za pomocą **administratora sieci** pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7e100-136">This menu allows you to control your new network through the **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="7e100-137">Dodawanie domeny niestandardowe</span><span class="sxs-lookup"><span data-stu-id="7e100-137">Adding custom domains</span></span>
<span data-ttu-id="7e100-138">[WordPress MU domeny mapowania] [ wordpress-plugin-wordpress-mu-domain-mapping] wtyczki ułatwia błyskawicznie do dodawania niestandardowych domen do dowolnej lokacji w sieci.</span><span class="sxs-lookup"><span data-stu-id="7e100-138">The [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze to add custom domains to any site in your network.</span></span> <span data-ttu-id="7e100-139">Dodatek plug-in, aby działać prawidłowo, należy wykonać pewne dodatkowe ustawienia w portalu, a także u rejestratora domen.</span><span class="sxs-lookup"><span data-stu-id="7e100-139">In order for the plugin to operate properly, you need to do some additional setup on the Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-to-the-web-app"></a><span data-ttu-id="7e100-140">Włącz mapowanie domeny aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="7e100-140">Enable domain mapping to the web app</span></span>
<span data-ttu-id="7e100-141">**Wolne** [usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) planu trybu nie obsługuje dodawania niestandardowych domen do aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7e100-141">The **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains to Web Apps.</span></span> <span data-ttu-id="7e100-142">Musisz przełączyć się do **Shared** lub **standardowe** tryb.</span><span class="sxs-lookup"><span data-stu-id="7e100-142">You will need to switch to **Shared** or **Standard** mode.</span></span> <span data-ttu-id="7e100-143">W tym celu:</span><span class="sxs-lookup"><span data-stu-id="7e100-143">To do this:</span></span>

* <span data-ttu-id="7e100-144">Zaloguj się do portalu Azure i Znajdź aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="7e100-144">Log in to the Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="7e100-145">Polecenie **skalowanie w górę** karcie **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="7e100-145">Click on the **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="7e100-146">W obszarze **ogólne**, wybierz opcję *SHARED* lub *standardowe*</span><span class="sxs-lookup"><span data-stu-id="7e100-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="7e100-147">Kliknij przycisk **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="7e100-147">Click **Save**</span></span>

<span data-ttu-id="7e100-148">Użytkownik może zostać wyświetlony komunikat z pytaniem, aby zweryfikować zmiany i potwierdzić, że aplikacja sieci web teraz może pociągnąć za sobą koszt, w zależności od użycia i konfiguracji, które można ustawić.</span><span class="sxs-lookup"><span data-stu-id="7e100-148">You may receive a message asking you to verify the change and acknowledge your web app may now incur a cost, depending upon usage and the other configuration you set.</span></span>

<span data-ttu-id="7e100-149">Trwa kilka sekund przetworzył nowe ustawienia, więc teraz jest odpowiedni moment, aby rozpocząć konfigurowanie domeny.</span><span class="sxs-lookup"><span data-stu-id="7e100-149">It takes a few seconds to process the new settings, so now is a good time to start setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="7e100-150">Sprawdź domenę</span><span class="sxs-lookup"><span data-stu-id="7e100-150">Verify your domain</span></span>
<span data-ttu-id="7e100-151">Przed Azure aplikacje sieci Web będzie można zamapować domenę do witryny, należy najpierw sprawdź, czy masz autoryzację do mapowania do domeny.</span><span class="sxs-lookup"><span data-stu-id="7e100-151">Before Azure Web Apps will allow you to map a domain to the site, you first need to verify that you have the authorization to map the domain.</span></span> <span data-ttu-id="7e100-152">Aby to zrobić, należy dodać nowy rekord CNAME do wpisu DNS.</span><span class="sxs-lookup"><span data-stu-id="7e100-152">To do so, you must add a new CNAME record to your DNS entry.</span></span>

* <span data-ttu-id="7e100-153">Zaloguj się do Twojej domeny Menedżera DNS</span><span class="sxs-lookup"><span data-stu-id="7e100-153">Log in to your domain's DNS manager</span></span>
* <span data-ttu-id="7e100-154">Tworzenie nowego rekordu CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="7e100-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="7e100-155">Punkt *awverify* do *awverify. YOUR_DOMAIN.azurewebsites.NET*</span><span class="sxs-lookup"><span data-stu-id="7e100-155">Point *awverify* to *awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="7e100-156">Może upłynąć trochę czasu, zanim zmiany DNS zaczynają obowiązywać pełne, więc jeśli poniższe kroki nie działają, przejdź filiżanki kawy, a następnie wróć i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="7e100-156">It may take some time for the DNS changes to go into full effect, so if the following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-the-domain-to-the-web-app"></a><span data-ttu-id="7e100-157">Dodawanie domeny do aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="7e100-157">Add the domain to the web app</span></span>
<span data-ttu-id="7e100-158">Powrót do aplikacji sieci web za pośrednictwem portalu Azure, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **domen niestandardowych i SSL**.</span><span class="sxs-lookup"><span data-stu-id="7e100-158">Return to your web app through the Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="7e100-159">Gdy *ustawienia protokołu SSL* są wyświetlane, zobaczysz pola, w którym możesz wpisać wszystkie domeny, które chcesz przypisać do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7e100-159">When the *SSL settings* are displayed, you will see the fields where you will input all the domains which you wish to assign to your web app.</span></span> <span data-ttu-id="7e100-160">Jeśli domeny nie ma na liście, nie będzie dostępna dla mapowania wewnątrz WordPress, niezależnie od tego, jak domena DNS jest skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="7e100-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how the domain DNS is setup.</span></span>

![Zarządzanie domenami niestandardowymi okna dialogowego][wordpress-manage-domains]

<span data-ttu-id="7e100-162">Po wpisaniu domenę, w polu tekstowym, Azure zweryfikuje rekord CNAME, który utworzono wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7e100-162">After typing your domain into the text box, Azure will verify the CNAME record you created previously.</span></span> <span data-ttu-id="7e100-163">Jeśli DNS nie została w pełni propagowane, wyświetli się czerwone wskaźnika.</span><span class="sxs-lookup"><span data-stu-id="7e100-163">If the DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="7e100-164">Jeśli go zakończyło się pomyślnie, zostanie wyświetlony zielony znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="7e100-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="7e100-165">Zanotuj adres IP wyświetlane w dolnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7e100-165">Take note of the IP Address listed at the bottom of the dialog.</span></span> <span data-ttu-id="7e100-166">Będzie on potrzebny można skonfigurować rekordu A dla domeny.</span><span class="sxs-lookup"><span data-stu-id="7e100-166">You will need this to setup the A record for your domain.</span></span>

## <a name="setup-the-domain-a-record"></a><span data-ttu-id="7e100-167">Konfiguracja domeny rekordu</span><span class="sxs-lookup"><span data-stu-id="7e100-167">Setup the domain A record</span></span>
<span data-ttu-id="7e100-168">Jeśli inne czynności zakończy się powodzeniem, mogą teraz przypisać domeny do aplikacji sieci web platformy Azure za pośrednictwem rekord A systemu DNS.</span><span class="sxs-lookup"><span data-stu-id="7e100-168">If the other steps were successful, you may now assign the domain to your Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="7e100-169">Jest w tym miejscu należy pamiętać, że aplikacje sieci web Azure akceptuje zarówno CNAME i, jednak możesz *musi* umożliwiają rekord A Mapowanie domeny.</span><span class="sxs-lookup"><span data-stu-id="7e100-169">It is important to note here that Azure web apps accept both CNAME and A records, however you *must* use an A record to enable proper domain mapping.</span></span> <span data-ttu-id="7e100-170">Rekord CNAME nie można przesłać dalej do innego CNAME, czyli co Azure utworzony z YOUR_DOMAIN.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="7e100-170">A CNAME cannot be forwarded to another CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="7e100-171">Przy użyciu adresu IP z poprzedniego kroku, wróć do Menedżera DNS i skonfigurować rekord A, aby wskazywał tego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="7e100-171">Using the IP address from the previous step, return to your DNS manager and setup the A record to point to that IP.</span></span>

## <a name="install-and-setup-the-plugin"></a><span data-ttu-id="7e100-172">Zainstaluj i skonfiguruj wtyczki</span><span class="sxs-lookup"><span data-stu-id="7e100-172">Install and setup the plugin</span></span>
<span data-ttu-id="7e100-173">Wdrożenie w wielu lokacjach WordPress aktualnie nie ma wbudowane metodę mapowania domen niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="7e100-173">WordPress Multisite currently does not have a built-in method to map custom domains.</span></span> <span data-ttu-id="7e100-174">Istnieje jednak dodatek o nazwie [WordPress MU domeny mapowania] [ wordpress-plugin-wordpress-mu-domain-mapping] dodaje funkcjonalność dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="7e100-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds the functionality for you.</span></span> <span data-ttu-id="7e100-175">Zaloguj się do administratora sieci część witryny i zainstaluj **WordPress MU domeny mapowania** wtyczki.</span><span class="sxs-lookup"><span data-stu-id="7e100-175">Log in to the Network Admin portion of your site and install the **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="7e100-176">Po zainstalowaniu i aktywowanie wtyczki, odwiedź stronę **ustawienia** > **mapowania domeny** do skonfigurowania wtyczki.</span><span class="sxs-lookup"><span data-stu-id="7e100-176">After installing and activating the plugin, visit **Settings** > **Domain Mapping** to configure the plugin.</span></span> <span data-ttu-id="7e100-177">W pierwszym polu tekstowym *adres IP serwera*, wprowadź adres IP używany można skonfigurować rekordu A dla domeny.</span><span class="sxs-lookup"><span data-stu-id="7e100-177">In the first textbox, *Server IP Address*, input the IP Address you used to setup the A record for the domain.</span></span> <span data-ttu-id="7e100-178">Ustaw dowolne *opcje domeny* można desire (wartości domyślne są często poprawnie), a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7e100-178">Set any *Domain Options* you desire (the defaults are often fine) and click **Save**.</span></span>

## <a name="map-the-domain"></a><span data-ttu-id="7e100-179">Mapa domeny</span><span class="sxs-lookup"><span data-stu-id="7e100-179">Map the domain</span></span>
<span data-ttu-id="7e100-180">Odwiedź stronę **pulpitu nawigacyjnego** chcesz mapy domeny do witryny.</span><span class="sxs-lookup"><span data-stu-id="7e100-180">Visit the **Dashboard** for the site you wish to map the domain to.</span></span> <span data-ttu-id="7e100-181">Polecenie **narzędzia** > **mapowania domeny** i wpisz nazwę nowej domeny w pliku tekstowym i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="7e100-181">Click on **Tools** > **Domain Mapping** and type the new domain into the textbox and click **Add**.</span></span>

<span data-ttu-id="7e100-182">Domyślnie nowej domeny będzie ponownie zapisać do domeny lokacji wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7e100-182">By default, the new domain will be rewritten to the autogenerated site domain.</span></span> <span data-ttu-id="7e100-183">Jeśli chcesz, aby cały ruch wysyłany do nowej domeny, sprawdź *domeny podstawowej ten blog* pole przed zapisaniem.</span><span class="sxs-lookup"><span data-stu-id="7e100-183">If you want to have all traffic sent to the new domain, check the *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="7e100-184">Można dodać dowolną liczbę domen do lokacji, ale może zawierać tylko jeden podstawowy.</span><span class="sxs-lookup"><span data-stu-id="7e100-184">You can add an unlimited number of domains to a site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="7e100-185">Należy go ponownie</span><span class="sxs-lookup"><span data-stu-id="7e100-185">Do it again</span></span>
<span data-ttu-id="7e100-186">Aplikacje sieci Web platformy Azure umożliwiają dodawanie nieograniczoną liczbę domen aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7e100-186">Azure Web Apps allow you to add an unlimited number of domains to a web app.</span></span> <span data-ttu-id="7e100-187">Aby dodać do innej domeny, konieczne będzie wykonanie **Sprawdź domenę** i **ustawienia domeny rekord** sekcje dla każdej domeny.</span><span class="sxs-lookup"><span data-stu-id="7e100-187">To add another domain you will need to execute the **Verify your domain** and **Setup the domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="7e100-188">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="7e100-188">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7e100-189">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="7e100-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="7e100-190">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="7e100-190">What's changed</span></span>
* <span data-ttu-id="7e100-191">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="7e100-191">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


