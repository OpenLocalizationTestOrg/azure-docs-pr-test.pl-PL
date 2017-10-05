---
title: "Bazy danych platformy Azure dla reguł zapory serwera MySQL | Dokumentacja firmy Microsoft"
description: "Opisuje reguły zapory bazy danych Azure, aby serwer MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 7456cef7a5da665ee3d70df64265b8186a79f9b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-database-for-mysql-server-firewall-rules"></a><span data-ttu-id="2f175-103">Bazy danych platformy Azure dla reguł zapory serwera MySQL</span><span class="sxs-lookup"><span data-stu-id="2f175-103">Azure Database for MySQL server firewall rules</span></span>
<span data-ttu-id="2f175-104">Zapory uniemożliwić dostęp do serwera bazy danych do chwili określenia komputery, które ma uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="2f175-104">Firewalls prevent all access to your database server until you specify which computers have permission.</span></span> <span data-ttu-id="2f175-105">Zapora udziela dostępu do serwera, na podstawie źródłowego adresu IP dla każdego żądania.</span><span class="sxs-lookup"><span data-stu-id="2f175-105">The firewall grants access to the server based on the originating IP address of each request.</span></span>

<span data-ttu-id="2f175-106">Aby skonfigurować zaporę, należy utworzyć reguły zapory określające zakresy dopuszczalnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="2f175-106">To configure your firewall, you create firewall rules that specify ranges of acceptable IP addresses.</span></span> <span data-ttu-id="2f175-107">Można tworzyć reguły zapory na poziomie serwera.</span><span class="sxs-lookup"><span data-stu-id="2f175-107">You can create firewall rules at the server level.</span></span>

<span data-ttu-id="2f175-108">**Reguły zapory:** reguły te umożliwiają klientom dostęp do całej bazy danych Azure, aby serwer MySQL, oznacza to, że wszystkie bazy danych w tym samym serwerze logicznym.</span><span class="sxs-lookup"><span data-stu-id="2f175-108">**Firewall rules:** These rules enable clients to access your entire Azure Database for MySQL server, that is, all the databases within the same logical server.</span></span> <span data-ttu-id="2f175-109">Reguły zapory poziomu serwera można skonfigurować za pomocą portalu Azure lub przy użyciu poleceń wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2f175-109">Server-level firewall rules can be configured by using the Azure portal or using Azure CLI commands.</span></span> <span data-ttu-id="2f175-110">Aby utworzyć reguły zapory poziomu serwera, musi być właściciela subskrypcji lub współautorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2f175-110">To create server-level firewall rules, you must be the subscription owner or a subscription contributor.</span></span>

## <a name="firewall-overview"></a><span data-ttu-id="2f175-111">Omówienie zapory</span><span class="sxs-lookup"><span data-stu-id="2f175-111">Firewall overview</span></span>
<span data-ttu-id="2f175-112">Wszelki dostęp do bazy danych Azure bazy danych MySQL serwera jest zablokowany przez zaporę domyślnie.</span><span class="sxs-lookup"><span data-stu-id="2f175-112">All database access to your Azure Database for MySQL server is blocked by the firewall by default.</span></span> <span data-ttu-id="2f175-113">Aby rozpocząć korzystanie z serwera z innego komputera, należy określić co najmniej jedną regułę zapory poziomu serwera, aby umożliwić dostęp do serwera.</span><span class="sxs-lookup"><span data-stu-id="2f175-113">To begin using your server from another computer, you need to specify one or more server-level firewall rules to enable access to your server.</span></span> <span data-ttu-id="2f175-114">Użyj reguł zapory do określenia IP zakresów adresów z Internetu, aby umożliwić.</span><span class="sxs-lookup"><span data-stu-id="2f175-114">Use the firewall rules to specify which IP address ranges from the Internet to allow.</span></span> <span data-ttu-id="2f175-115">Dostęp do witryny portalu Azure, sama nie ma wpływu na reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="2f175-115">Access to the Azure portal website itself is not impacted by the firewall rules.</span></span>

<span data-ttu-id="2f175-116">Próby nawiązania połączenia z Internetem i Azure musi najpierw przejść przez zaporę przed dotarciem Azure bazy danych dla bazy danych MySQL, jak pokazano na poniższym diagramie:</span><span class="sxs-lookup"><span data-stu-id="2f175-116">Connection attempts from the Internet and Azure must first pass through the firewall before they can reach your Azure Database for MySQL database, as shown in the following diagram:</span></span>

![Przykładowy przepływ działania zapory](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-the-internet"></a><span data-ttu-id="2f175-118">Łączenie się z Internetu</span><span class="sxs-lookup"><span data-stu-id="2f175-118">Connecting from the Internet</span></span>
<span data-ttu-id="2f175-119">Reguły zapory na poziomie serwera dotyczą wszystkich baz danych w bazie danych Azure dla serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="2f175-119">Server-level firewall rules apply to all databases on the Azure Database for MySQL server.</span></span>

<span data-ttu-id="2f175-120">Jeśli adres IP żądania należy do jednego z zakresów określonych w regułach zapory na poziomie serwera, ustanawiane jest połączenie.</span><span class="sxs-lookup"><span data-stu-id="2f175-120">If the IP address of the request is within one of the ranges specified in the server-level firewall rules, the connection is granted.</span></span>

<span data-ttu-id="2f175-121">Jeśli adres IP żądania nie jest w zakresie określony w żadnym z reguły zapory poziomu serwera lub na poziomie bazy danych, żądanie połączenia zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="2f175-121">If the IP address of the request is not within the ranges specified in any of the database-level or server-level firewall rules, the connection request fails.</span></span>

## <a name="programmatically-managing-firewall-rules"></a><span data-ttu-id="2f175-122">Programowe zarządzanie regułami zapory</span><span class="sxs-lookup"><span data-stu-id="2f175-122">Programmatically managing firewall rules</span></span>
<span data-ttu-id="2f175-123">Oprócz portalu Azure można zarządzać reguły zapory, programowo przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2f175-123">In addition to the Azure portal, firewall rules can be managed programmatically using Azure CLI.</span></span> <span data-ttu-id="2f175-124">Zobacz też [tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure](./howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2f175-124">See also [Create and manage Azure Database for MySQL firewall rules using Azure CLI](./howto-manage-firewall-using-cli.md)</span></span>

## <a name="troubleshooting-the-database-firewall"></a><span data-ttu-id="2f175-125">Rozwiązywanie problemów z zaporą bazy danych</span><span class="sxs-lookup"><span data-stu-id="2f175-125">Troubleshooting the database firewall</span></span>
<span data-ttu-id="2f175-126">Podczas dostępu do bazy danych Microsoft Azure dla usługi serwera MySQL nie działają zgodnie z oczekiwaniami, należy rozważyć następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="2f175-126">Consider the following points when access to the Microsoft Azure Database for MySQL server service does not behave as you expect:</span></span>

* <span data-ttu-id="2f175-127">**Zmiany na liście dozwolonych nie zostały uwzględnione jeszcze:** może być jak opóźnienie 5 minutową zmienia się z bazą danych Azure konfiguracji zapory serwera MySQL zaczęły obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="2f175-127">**Changes to the allow list have not taken effect yet:** There may be as much as a five-minute delay for changes to the Azure Database for MySQL Server firewall configuration to take effect.</span></span>

* <span data-ttu-id="2f175-128">**Nazwa logowania nie jest autoryzowany lub niepoprawne hasło było używane:** nazwy logowania nie ma uprawnień w bazie danych Azure MySQL serwera lub hasło jest niepoprawne, odmowa połączenia z bazą danych Azure dla serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="2f175-128">**The login is not authorized or an incorrect password was used:** If a login does not have permissions on the Azure Database for MySQL server or the password used is incorrect, the connection to the Azure Database for MySQL server is denied.</span></span> <span data-ttu-id="2f175-129">Utworzenie ustawień zapory zapewnia klientom jedynie możliwość próby nawiązania połączenia z serwerem, ale każdy klient musi podać niezbędne poświadczenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2f175-129">Creating a firewall setting only provides clients with an opportunity to attempt connecting to your server; each client must provide the necessary security credentials.</span></span>

* <span data-ttu-id="2f175-130">**Dynamiczny adres IP:** jeśli używane jest połączenie internetowe za pomocą dynamicznego adresowania IP i występują problemy z przejściem przez zaporę, można wypróbować jedno z poniższych rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="2f175-130">**Dynamic IP address:** If you have an Internet connection with dynamic IP addressing and you are having trouble getting through the firewall, you could try one of the following solutions:</span></span>

* <span data-ttu-id="2f175-131">Zakres adresów IP, które są przypisane do komputerów klienckich łączących się z bazą danych Azure dla serwera MySQL poproś o usługodawcy internetowego (ISP), a następnie Dodaj zakres adresów IP reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="2f175-131">Ask your Internet Service Provider (ISP) for the IP address range assigned to your client computers that access the Azure Database for MySQL server, and then add the IP address range as a firewall rule.</span></span>

* <span data-ttu-id="2f175-132">Pobierz statyczne adresy IP dla komputerów klienckich, a następnie dodaj te adresy IP jako reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="2f175-132">Get static IP addressing instead for your client computers, and then add the IP addresses as firewall rules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f175-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2f175-133">Next steps</span></span>

<span data-ttu-id="2f175-134">[Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure](./howto-manage-firewall-using-portal.md)
[tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure](./howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2f175-134">[Create and manage Azure Database for MySQL firewall rules using the Azure portal](./howto-manage-firewall-using-portal.md)
[Create and manage Azure Database for MySQL firewall rules using Azure CLI](./howto-manage-firewall-using-cli.md)</span></span>
