---
title: "Uwierzytelnianie oparte na nagłówka z PingAccess dla serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Publikowania aplikacji za pomocą PingAccess i serwera Proxy aplikacji do obsługi uwierzytelniania opartego na nagłówka."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 58034ab8830cf655199875b448948ea14dc04a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="e2f63-103">Nagłówek uwierzytelniania dla logowania jednokrotnego z serwera Proxy aplikacji i PingAccess</span><span class="sxs-lookup"><span data-stu-id="e2f63-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="e2f63-104">Azure Active Directory serwera Proxy aplikacji i PingAccess ma współpracę ze sobą aby zapewnić klientom usługi Azure Active Directory dostępu do nawet więcej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2f63-104">Azure Active Directory Application Proxy and PingAccess have partnered together to provide Azure Active Directory customers with access to even more applications.</span></span> <span data-ttu-id="e2f63-105">Rozwija PingAccess [istniejący serwer Proxy aplikacji ofert](active-directory-application-proxy-get-started.md) uwzględnienie dostępu pojedynczego logowania do aplikacji, które nagłówków jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e2f63-105">PingAccess expands the [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) to include single sign-on access to applications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="e2f63-106">Co to jest PingAccess dla usługi Azure AD?</span><span class="sxs-lookup"><span data-stu-id="e2f63-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="e2f63-107">PingAccess dla usługi Azure Active Directory jest oferty PingAccess umożliwiającą można umożliwić użytkownikom dostępu i logowanie jednokrotne do aplikacji, które używają nagłówki uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e2f63-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you to give users access and single sign-on to applications that use headers for authentication.</span></span> <span data-ttu-id="e2f63-108">Serwer Proxy aplikacji traktuje te aplikacje, takie jak każdy inny, za pomocą usługi Azure AD w celu uwierzytelniania dostępu i następnie przekazywanie ruchu przez usługę łącznika.</span><span class="sxs-lookup"><span data-stu-id="e2f63-108">Application Proxy treats these apps like any other, using Azure AD to authenticate access and then passing traffic through the connector service.</span></span> <span data-ttu-id="e2f63-109">PingAccess znajduje się przed aplikacje i tłumaczy token dostępu z usługi Azure AD na nagłówka, tak aby po otrzymaniu uwierzytelnianie w formacie, który można odczytać.</span><span class="sxs-lookup"><span data-stu-id="e2f63-109">PingAccess sits in front of the apps and translates the access token from Azure AD into a header so that the application receives the authentication in the format it can read.</span></span>

<span data-ttu-id="e2f63-110">Użytkownicy nie będą Zwróć uwagę, inne po zalogowaniu się do użycia w aplikacjach firmowych.</span><span class="sxs-lookup"><span data-stu-id="e2f63-110">Your users won’t notice anything different when they sign in to use your corporate apps.</span></span> <span data-ttu-id="e2f63-111">Wciąż pracować z dowolnego miejsca na dowolnym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="e2f63-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="e2f63-112">Ponieważ łączniki serwera Proxy aplikacji kierować zdalnego ruch do wszystkich aplikacji niezależnie od ich typ uwierzytelniania, nadal równoważenia obciążenia, automatycznie, jak również.</span><span class="sxs-lookup"><span data-stu-id="e2f63-112">Since the Application Proxy connectors direct remote traffic to all apps regardless of their authentication type, they’ll continue to load balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="e2f63-113">Jak uzyskać dostęp?</span><span class="sxs-lookup"><span data-stu-id="e2f63-113">How do I get access?</span></span>

<span data-ttu-id="e2f63-114">Ponieważ ten scenariusz jest dostępna za pośrednictwem usługi Azure Active Directory i PingAccess, potrzebnych licencji dla obu usług.</span><span class="sxs-lookup"><span data-stu-id="e2f63-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="e2f63-115">Jednak subskrypcje usługi Azure Active Directory Premium obejmują podstawowe licencji PingAccess, która obejmuje aplikacje do 20.</span><span class="sxs-lookup"><span data-stu-id="e2f63-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up to 20 applications.</span></span> <span data-ttu-id="e2f63-116">Jeśli potrzebujesz do publikowania aplikacji opartych na nagłówkach więcej niż 20, możesz kupić dodatkowych licencji z PingAccess.</span><span class="sxs-lookup"><span data-stu-id="e2f63-116">If you need to publish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="e2f63-117">Aby uzyskać więcej informacji, zobacz [Wersje usługi Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="e2f63-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="e2f63-118">Publikowanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e2f63-118">Publish your application in Azure</span></span>

<span data-ttu-id="e2f63-119">Ten artykuł jest przeznaczony dla osób, które publikują aplikacji w tym scenariuszu po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="e2f63-119">This article is intended for people who are publishing an app with this scenario for the first time.</span></span> <span data-ttu-id="e2f63-120">Instruktaże jak rozpocząć pracę z aplikacji i PingAccess, oprócz kroki publikowania.</span><span class="sxs-lookup"><span data-stu-id="e2f63-120">It walks through how to get started with both Application and PingAccess, in addition to the publishing steps.</span></span> <span data-ttu-id="e2f63-121">Jeśli skonfigurowano już obie usługi, ale odświeżacz kroki publikowania, możesz pominąć instalacja łącznika i przenieść na [Dodaj aplikację do usługi Azure AD przy użyciu serwera Proxy aplikacji](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="e2f63-121">If you’ve already configured both services but want a refresher on the publishing steps, you can skip the connector installation and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="e2f63-122">Ponieważ ten scenariusz jest powiązanie między usługą Azure AD i PingAccess, niektóre instrukcji istnieje w witrynie tożsamości Ping.</span><span class="sxs-lookup"><span data-stu-id="e2f63-122">Since this scenario is a partnership between Azure AD and PingAccess, some of the instructions exist on the Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="e2f63-123">Instalowanie łącznika serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="e2f63-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="e2f63-124">Jeśli już ma włączony serwer Proxy aplikacji, a ma zainstalowany łącznik, możesz pominąć tę sekcję i przenieść na [Dodaj aplikację do usługi Azure AD przy użyciu serwera Proxy aplikacji](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="e2f63-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="e2f63-125">Łącznik serwera Proxy aplikacji jest usługi systemu Windows Server, który kieruje ruch z zdalnego pracowników do opublikowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2f63-125">The Application Proxy connector is a Windows Server service that directs the traffic from your remote employees to your published apps.</span></span> <span data-ttu-id="e2f63-126">Aby uzyskać szczegółowe instrukcje dotyczące instalacji, zobacz [Włączanie serwera Proxy aplikacji w portalu Azure](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="e2f63-126">For more detailed installation instructions, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="e2f63-127">Zaloguj się do [portalu Azure](https://portal.azure.com) jako administrator globalny.</span><span class="sxs-lookup"><span data-stu-id="e2f63-127">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="e2f63-128">Wybierz **usługi Azure Active Directory** > **serwera proxy aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="e2f63-129">Wybierz **Pobierz łącznik** aby rozpocząć pobieranie łącznika serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2f63-129">Select **Download Connector** to start the Application Proxy connector download.</span></span> <span data-ttu-id="e2f63-130">Postępuj zgodnie z instrukcjami instalacji.</span><span class="sxs-lookup"><span data-stu-id="e2f63-130">Follow the installation instructions.</span></span>

   ![Włącz serwer Proxy aplikacji i Pobierz łącznik](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="e2f63-132">Pobieranie łącznika automatycznie należy włączyć serwer Proxy aplikacji dla katalogu, ale jeśli nie możesz wybrać **Włączanie serwera Proxy aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-132">Downloading the connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-to-azure-ad-with-application-proxy"></a><span data-ttu-id="e2f63-133">Dodaj aplikację do usługi Azure AD przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="e2f63-133">Add your app to Azure AD with Application Proxy</span></span>

<span data-ttu-id="e2f63-134">Istnieją dwie akcje, które należy wykonać w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f63-134">There are two actions you need to take in the Azure portal.</span></span> <span data-ttu-id="e2f63-135">Najpierw należy opublikować aplikację przy użyciu serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2f63-135">First, you need to publish your application with Application Proxy.</span></span> <span data-ttu-id="e2f63-136">Następnie które należy zebrać pewne informacje o aplikacji, którą można użyć podczas wykonywania czynności PingAccess.</span><span class="sxs-lookup"><span data-stu-id="e2f63-136">Then, you need to collect some information about the app that you can use during the PingAccess steps.</span></span>

<span data-ttu-id="e2f63-137">Wykonaj następujące kroki, aby opublikować aplikację.</span><span class="sxs-lookup"><span data-stu-id="e2f63-137">Follow these steps to publish your app.</span></span> <span data-ttu-id="e2f63-138">Bardziej szczegółowe wskazówki kroki 1 – 8, zobacz [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e2f63-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="e2f63-139">Jeśli nie w ostatniej sekcji, zaloguj się do [portalu Azure](https://portal.azure.com) jako administrator globalny.</span><span class="sxs-lookup"><span data-stu-id="e2f63-139">If you didn't in the last section, sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="e2f63-140">Wybierz **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="e2f63-141">Wybierz **Dodaj** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="e2f63-141">Select **Add** at the top of the blade.</span></span>
4. <span data-ttu-id="e2f63-142">Wybierz **lokalnej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="e2f63-143">Wypełnij wymagane pola informacje o nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2f63-143">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="e2f63-144">Użyj poniższych wskazówek dla ustawienia:</span><span class="sxs-lookup"><span data-stu-id="e2f63-144">Use the following guidance for the settings:</span></span>
   - <span data-ttu-id="e2f63-145">**Wewnętrzny adres URL**: zwykle Podaj adres URL, który przyjmuje stronę logowania aplikacji podczas pracy w sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="e2f63-145">**Internal URL**: Normally you provide the URL that takes you to the app’s sign in page when you’re on the corporate network.</span></span> <span data-ttu-id="e2f63-146">W tym scenariuszu łącznik musi traktować PingAccess proxy jako pierwsza strona aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2f63-146">For this scenario the connector needs to treat the PingAccess proxy as the front page of the app.</span></span> <span data-ttu-id="e2f63-147">Użyj tego formatu: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="e2f63-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="e2f63-148">Numer portu to 3000 domyślnie, ale można go skonfigurować w PingAccess.</span><span class="sxs-lookup"><span data-stu-id="e2f63-148">The port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="e2f63-149">**Metoda wstępnego uwierzytelnienia**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2f63-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="e2f63-150">**Tłumaczenie adresów URL w nagłówkach**: nie</span><span class="sxs-lookup"><span data-stu-id="e2f63-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="e2f63-151">Jeśli swoją pierwszą aplikację, aby uruchomić i wrócić i zaktualizować to ustawienie, jeśli zmienisz konfigurację PingAccess za pomocą port 3000.</span><span class="sxs-lookup"><span data-stu-id="e2f63-151">If this is your first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="e2f63-152">Jeśli jest to drugi lub nowszym aplikacji, będzie to musi być zgodny odbiornika skonfigurowaniu PingAccess.</span><span class="sxs-lookup"><span data-stu-id="e2f63-152">If this is your second or later app, this will need to match the Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="e2f63-153">Dowiedz się więcej o [odbiorników w PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="e2f63-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="e2f63-154">Wybierz **Dodaj** w dolnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="e2f63-154">Select **Add** at the bottom of the blade.</span></span> <span data-ttu-id="e2f63-155">Aplikacja zostanie dodany, a następnie otwiera menu szybki start.</span><span class="sxs-lookup"><span data-stu-id="e2f63-155">Your application is added, and the quick start menu opens.</span></span>
7. <span data-ttu-id="e2f63-156">Wybierz z menu szybki start **przypisać użytkownika do testowania**, i Dodaj przynajmniej jednego użytkownika do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2f63-156">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="e2f63-157">Upewnij się, że to konto testu ma dostęp do aplikacji lokalnych.</span><span class="sxs-lookup"><span data-stu-id="e2f63-157">Make sure this test account has access to the on-premises application.</span></span>
8. <span data-ttu-id="e2f63-158">Wybierz **przypisać** można zapisać przypisanie użytkownika testu.</span><span class="sxs-lookup"><span data-stu-id="e2f63-158">Select **Assign** to save the test user assignment.</span></span>
9. <span data-ttu-id="e2f63-159">W bloku zarządzania aplikacjami, wybierz **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-159">On the app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="e2f63-160">Wybierz **na podstawie nagłówka logowania jednokrotnego** z menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="e2f63-160">Choose **Header-based sign-on** from the drop-down menu.</span></span> <span data-ttu-id="e2f63-161">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="e2f63-162">Jeśli jest to pierwsza przy użyciu opartych na nagłówkach logowania jednokrotnego, musisz zainstalować PingAccess.</span><span class="sxs-lookup"><span data-stu-id="e2f63-162">If this is your first time using header-based single sign-on, you need to install PingAccess.</span></span> <span data-ttu-id="e2f63-163">Aby upewnić się, że subskrypcji platformy Azure jest automatycznie kojarzony z instalacją PingAccess, skorzystaj z łącza po tej jednej strony logowania do pobrania PingAccess.</span><span class="sxs-lookup"><span data-stu-id="e2f63-163">To make sure your Azure subscription is automatically associated with your PingAccess installation, use the link on this single sign-on page to download PingAccess.</span></span> <span data-ttu-id="e2f63-164">Teraz Otwórz witrynę pobierania lub powracanie do tej strony.</span><span class="sxs-lookup"><span data-stu-id="e2f63-164">You can open the download site now, or come back to this page later.</span></span> 

   ![Wybierz na podstawie nagłówka logowania jednokrotnego](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="e2f63-166">Zamknij bloku aplikacji przedsiębiorstwa lub przewiń do lewej strony, aby wrócić do menu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2f63-166">Close the Enterprise applications blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
12. <span data-ttu-id="e2f63-167">Wybierz **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-167">Select **App registrations**.</span></span>

   ![Wybierz rejestracji aplikacji](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="e2f63-169">Wybierz aplikację, dodaną, następnie **adresy URL odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-169">Select the app you just added, then **Reply URLs**.</span></span>

   ![Wybierz adresy URL odpowiedzi](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="e2f63-171">Sprawdź, czy zewnętrznego adresu URL, który zostanie przypisany do aplikacji w kroku 5 znajduje się na liście adresów URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e2f63-171">Check to see if the external URL that you assigned to your app in step 5 is in the Reply URLs list.</span></span> <span data-ttu-id="e2f63-172">Jeśli nie, dodaj go.</span><span class="sxs-lookup"><span data-stu-id="e2f63-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="e2f63-173">W bloku ustawień aplikacji, wybierz **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-173">On the app settings blade, select **Required permissions**.</span></span>

  ![Wybierz wymagane uprawnienia](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="e2f63-175">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-175">Select **Add**.</span></span> <span data-ttu-id="e2f63-176">W interfejsie API, wybierz opcję **Windows Azure Active Directory**, następnie **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-176">For the API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="e2f63-177">Uprawnienia, wybierz **odczytu i zapisu wszystkie aplikacje** i **Zaloguj się i odczytuj profil użytkownika**, następnie **wybierz** i **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-177">For the permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![Wybierz uprawnienia](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-the-pingaccess-steps"></a><span data-ttu-id="e2f63-179">Zbieranie informacji o krokach PingAccess</span><span class="sxs-lookup"><span data-stu-id="e2f63-179">Collect information for the PingAccess steps</span></span>

1. <span data-ttu-id="e2f63-180">W bloku ustawień aplikacji, wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-180">On your app settings blade, select **Properties**.</span></span> 

  ![Wybierz polecenie Właściwości](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="e2f63-182">Zapisz **identyfikator aplikacji** wartość.</span><span class="sxs-lookup"><span data-stu-id="e2f63-182">Save the **Application Id** value.</span></span> <span data-ttu-id="e2f63-183">Służy to do tego Identyfikatora klienta po skonfigurowaniu PingAccess.</span><span class="sxs-lookup"><span data-stu-id="e2f63-183">This is used for the client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="e2f63-184">W bloku ustawień aplikacji, wybierz **klucze**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-184">On the app settings blade, select **Keys**.</span></span>

  ![Wybierz klucze](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="e2f63-186">Utwórz klucz, wprowadzając opis klucza i wybierając z menu rozwijanego datę wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="e2f63-186">Create a key by entering a key description and choosing an expiration date from the drop-down menu.</span></span>
5. <span data-ttu-id="e2f63-187">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-187">Select **Save**.</span></span> <span data-ttu-id="e2f63-188">Identyfikator GUID jest wyświetlana w **wartość** pola.</span><span class="sxs-lookup"><span data-stu-id="e2f63-188">A GUID appears in the **Value** field.</span></span>

  <span data-ttu-id="e2f63-189">Zapisz tę wartość teraz, ponieważ nie można go ponownie wyświetlić po zamknięciu tego okna.</span><span class="sxs-lookup"><span data-stu-id="e2f63-189">Save this value now, as you won’t be able to see it again after you close this window.</span></span>

  ![Utwórz nowy klucz](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="e2f63-191">Zamknij bloku rejestracji aplikacji lub przewiń do lewej strony, aby wrócić do menu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2f63-191">Close the App registrations blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
7. <span data-ttu-id="e2f63-192">Wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-192">Select **Properties**.</span></span>
8. <span data-ttu-id="e2f63-193">Zapisz **identyfikator katalogu** identyfikatora GUID.</span><span class="sxs-lookup"><span data-stu-id="e2f63-193">Save the **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-to-send-custom-fields"></a><span data-ttu-id="e2f63-194">Opcjonalne - GraphAPI aktualizacji do wysyłania niestandardowych pól</span><span class="sxs-lookup"><span data-stu-id="e2f63-194">Optional - Update GraphAPI to send custom fields</span></span>

<span data-ttu-id="e2f63-195">Aby uzyskać listę tokeny zabezpieczające, które wysyła usługi Azure AD do uwierzytelniania, zobacz [odwołania do tokenu usługi Azure AD](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="e2f63-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="e2f63-196">Jeśli potrzebujesz niestandardowych oświadczenie, które wysyła innych tokenów, użyj GraphAPI, aby ustawić pole aplikacji *acceptMappedClaims* do **True**.</span><span class="sxs-lookup"><span data-stu-id="e2f63-196">If you need a custom claim that sends other tokens, use GraphAPI to set the app field *acceptMappedClaims* to **True**.</span></span> <span data-ttu-id="e2f63-197">Eksplorator usługi Azure AD Graph lub MS Graph umożliwia ta konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="e2f63-197">You can use either Azure AD Graph Explorer or MS Graph to make this configuration.</span></span> 

<span data-ttu-id="e2f63-198">W tym przykładzie użyto wykres Explorer:</span><span class="sxs-lookup"><span data-stu-id="e2f63-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="e2f63-199">Pobierz PingAccess i konfigurowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e2f63-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="e2f63-200">Teraz, zostały ukończone wszystkie kroki konfiguracji usługi Azure Active Directory, możesz przejść do konfigurowania PingAccess.</span><span class="sxs-lookup"><span data-stu-id="e2f63-200">Now that you've completed all the Azure Active Directory setup steps, you can move on to configuring PingAccess.</span></span> 

<span data-ttu-id="e2f63-201">Szczegółowe informacje na temat PingAccess częścią tego scenariusza kontynuować w dokumentacji polecenia Ping tożsamości [PingAccess konfigurowanie dla usługi Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="e2f63-201">The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="e2f63-202">Tych krokach objaśniono proces pobierania konta PingAccess, jeśli nie masz już konto, instalowany serwer PingAccess i tworzenie połączenia dostawcy usługi Azure AD OIDC o identyfikatorze katalogu, który został skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f63-202">Those steps walk you through the process of getting a PingAccess account if you don't already have one, installing the PingAccess Server, and creating an Azure AD OIDC Provider connection with the Directory ID that you copied from the Azure portal.</span></span> <span data-ttu-id="e2f63-203">Następnie należy użyć wartości Identyfikatora aplikacji i klucza do utworzenia sesji sieci Web na PingAccess.</span><span class="sxs-lookup"><span data-stu-id="e2f63-203">Then, you use the Application ID and Key values to create a Web Session on PingAccess.</span></span> <span data-ttu-id="e2f63-204">Po wykonaniu tej można Konfigurowanie mapowania tożsamości i tworzenia hostów wirtualnych, witryn i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2f63-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="e2f63-205">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e2f63-205">Test your app</span></span>

<span data-ttu-id="e2f63-206">Po zakończeniu wszystkich tych kroków aplikacji powinna być uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="e2f63-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="e2f63-207">Aby ją przetestować, otwórz przeglądarkę i przejdź do zewnętrzny adres URL utworzony po opublikowaniu aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f63-207">To test it, open a browser and navigate to the external URL that you created when you published the app in Azure.</span></span> <span data-ttu-id="e2f63-208">Zaloguj się przy użyciu konta testowego przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2f63-208">Sign in with the test account that you assigned to the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2f63-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e2f63-209">Next steps</span></span>

- [<span data-ttu-id="e2f63-210">Skonfiguruj PingAccess dla usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2f63-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="e2f63-211">W jaki sposób serwera Proxy aplikacji usługi Azure AD zapewnia rejestrację jednokrotną</span><span class="sxs-lookup"><span data-stu-id="e2f63-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="e2f63-212">Rozwiązywanie problemów z serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="e2f63-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
