---
title: "aaaSecure klastra sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Opisano scenariusze zabezpieczeń hello tooimplement różne technologie używane sieci szkieletowej usług, jak klaster i hello tych scenariuszy."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.openlocfilehash: 249a9e85b8fbe174e2accee85a94d95b2872a3af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>Scenariusze zabezpieczeń klastra sieci szkieletowej usług
Klaster sieci szkieletowej usług jest zasób, którego jesteś właścicielem. Klastry muszą być użytkownikami zabezpieczonych tooprevent nieautoryzowany łączenie tooyour klastra, szczególnie w przypadku, gdy ma na nim uruchomione obciążeń produkcyjnych. Możliwe toocreate niezabezpieczona klastra, ale dzięki temu tooit tooconnect użytkowników anonimowych, jeśli eksponuje toohello punkty końcowe zarządzania publicznej sieci Internet. 

Ten artykuł zawiera omówienie hello scenariusze zabezpieczeń w przypadku klastrów w systemie Azure albo autonomicznej i hello różne technologie używane tooimplement tych scenariuszy. scenariusze zabezpieczeń klastra Hello są następujące:

* Zabezpieczenia węzła do węzła
* Węzeł klienta zabezpieczeń
* Kontrola dostępu oparta na rolach (RBAC)

## <a name="node-to-node-security"></a>Zabezpieczenia węzła do węzła
Zabezpiecza komunikację między hello maszyn wirtualnych lub maszyn w klastrze hello. Daje to pewność, że tylko komputery, które są autoryzowane toojoin hello klastra mogą uczestniczyć w hosting aplikacji i usług w klastrze hello.

![Diagram komunikacji między węzłami][Node-to-Node]

Klastry z systemem Azure lub autonomiczne klastry z systemem Windows można użyć dowolnego [certyfikatu zabezpieczeń](https://msdn.microsoft.com/library/ff649801.aspx) lub [zabezpieczenia systemu Windows](https://msdn.microsoft.com/library/ff649396.aspx) dla komputerów z systemem Windows Server.

### <a name="node-to-node-certificate-security"></a>Zabezpieczenia certyfikatów węzła do węzła
Sieć szkieletowa usług korzysta z certyfikatów X.509, określone jako część konfiguracji typu węzła hello podczas tworzenia klastra. Szybki przegląd certyfikaty te są i jak uzyskać lub utworzyć je znajduje się na końcu hello w tym artykule.

Certyfikat zabezpieczeń jest skonfigurowany podczas tworzenia klastra hello za pośrednictwem portalu Azure hello, szablony usługi Azure Resource Manager lub szablonu JSON w autonomicznych. Można określić podstawowy certyfikat i opcjonalne dodatkowej certyfikat, który jest używany do najazdy certyfikatu. Witaj certyfikatów głównych i dodatkowych, możesz określić powinien być inny niż powitania klienta administratora i określ dla certyfikatów klienta tylko do odczytu [zabezpieczeń węzeł klient](#client-to-node-security).

Dla odczytu Azure [Konfigurowanie klastra za pomocą szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) toolearn jak tooconfigure certyfikatu zabezpieczeń w klastrze.

Dla autonomicznej odczytu systemu Windows Server [Secure autonomiczny klastra w systemie Windows za pomocą certyfikatów X.509](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>Zabezpieczenia systemu windows węzła do węzła
Dla autonomicznej odczytu systemu Windows Server [Secure autonomiczny klastra w systemie Windows przy użyciu zabezpieczeń systemu Windows](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>Węzeł klienta zabezpieczeń
Uwierzytelnianie klientów i zabezpiecza komunikację między klientem a poszczególne węzły w klastrze hello. Ten typ zabezpieczeń uwierzytelnia i zabezpiecza komunikację klienta, który zapewnia, że tylko autoryzowani użytkownicy mogą uzyskać dostęp hello klastra i aplikacji hello wdrożonych w klastrze hello. Klienci są identyfikowane za pomocą ich poświadczeń zabezpieczeń systemu Windows lub poświadczeń zabezpieczeń certyfikatów.

![Diagram komunikacji klienta do węzła][Client-to-Node]

Klastry z systemem Azure lub autonomiczne klastry z systemem Windows można użyć dowolnego [certyfikatu zabezpieczeń](https://msdn.microsoft.com/library/ff649801.aspx) lub [zabezpieczenia systemu Windows](https://msdn.microsoft.com/library/ff649396.aspx).

### <a name="client-to-node-certificate-security"></a>Zabezpieczenia certyfikatów klienta do węzła
 Węzeł klient certyfikat zabezpieczeń jest skonfigurowany podczas tworzenia klastra hello za pośrednictwem hello portalu Azure, szablonów usługi Resource Manager lub szablonu JSON w autonomicznej, określając administracyjnej certyfikatu klienta i/lub certyfikatu klienta użytkownika.  Hello klientów i użytkowników certyfikatów klienta administracyjnego można określić powinien być inny niż hello podstawowe i pomocnicze certyfikaty, należy określić dla [zabezpieczeń węzła do węzła](#node-to-node-security) najlepszym rozwiązaniem. Domyślnie certyfikaty klastra hello węzła do węzła zabezpieczeń są dodawane toohello dozwolone Admin listy certyfikatów klienta.

Klienci łączący toohello klastra przy użyciu certyfikatu admin hello ma pełny dostęp toomanagement możliwości.  Klienci łączący się za pomocą certyfikatu klienta użytkownika tylko do odczytu hello klastra toohello mają tylko możliwości toomanagement dostęp do odczytu. Innymi słowy te certyfikaty są używane do hello roli zasad kontroli dostępu (RBAC) opisane w dalszej części tego artykułu.

Dla odczytu Azure [Konfigurowanie klastra za pomocą szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) toolearn jak tooconfigure certyfikatu zabezpieczeń w klastrze.

Dla autonomicznej odczytu systemu Windows Server [Secure autonomiczny klastra w systemie Windows za pomocą certyfikatów X.509](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Węzeł Klient zabezpieczeń usługi Azure Active Directory (AAD) na platformie Azure
Klastry z systemem Azure można również bezpieczny dostęp do punktów końcowych zarządzania toohello przy użyciu usługi Azure Active Directory (AAD). Zobacz [Konfigurowanie klastra za pomocą szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) informacji na temat jak toocreate hello niezbędne artefaktów usługi AAD, jak toopopulate ich podczas klastra tworzenie i jak tooconnect toothose klastrów później.

## <a name="security-recommendations"></a>Zalecenia dotyczące zabezpieczeń
W przypadku klastrów platformy Azure zaleca się korzystać klienci tooauthenticate zabezpieczeń usługi AAD i certyfikaty zabezpieczeń węzła do węzła.

Dla autonomicznego systemu Windows Server klastrów, zaleca się użycie zabezpieczeń systemu Windows z grupy zarządzane konta (GMA), jeśli masz system Windows Server 2012 R2 i usługi Active Directory. W przeciwnym razie nadal używać zabezpieczeń systemu Windows z konta systemu Windows.

## <a name="role-based-access-control-rbac"></a>Kontrola dostępu oparta na rolach (RBAC)
Kontrola dostępu umożliwia hello klastra administrator toolimit dostępu toocertain klastra operacje dla różnych grup użytkowników, co klaster hello bardziej bezpieczne. Dwa typy kontroli dostępu różnych są obsługiwane dla klientów łączących się z klastrem tooa: rola administratora i roli użytkownika.

Administratorzy mają pełny dostęp toomanagement możliwości (w tym możliwości odczytu/zapisu). Użytkownicy mają domyślnie tylko możliwości toomanagement dostęp do odczytu (na przykład możliwość wykonywania kwerend), a hello możliwości tooresolve aplikacji i usług.

Można określić hello administratora i użytkownika klienta role w czasie tworzenia klastra hello podając oddzielne tożsamości (certyfikaty, AAD itp.) dla każdego. Aby uzyskać więcej informacji na hello domyślne uprawnienia kontroli dostępu i jak toochange hello domyślnych ustawień, zobacz [kontrola dostępu oparta na rolach dla klientów usługi sieć szkieletowa](service-fabric-cluster-security-roles.md).

## <a name="x509-certificates-and-service-fabric"></a>Certyfikaty X.509 i sieci szkieletowej usług
Certyfikaty cyfrowe X.509 są często używane tooauthenticate klientów i serwerów oraz tooencrypt i cyfrowego podpisywania wiadomości. Aby uzyskać więcej informacji o tych certyfikatów, przejdź zbyt[Praca z certyfikatami](http://msdn.microsoft.com/library/ms731899.aspx).

Tooconsider kilka ważnych rzeczy:

* Certyfikaty używane w klastrach z systemem obciążeń produkcyjnych powinny zostać utworzone przy użyciu poprawnie skonfigurowanej usługi certyfikatów systemu Windows Server lub uzyskane z zatwierdzonych [urzędu certyfikacji,](https://en.wikipedia.org/wiki/Certificate_authority).
* Nigdy nie używaj żadnych tymczasowej lub certyfikaty testów w środowisku produkcyjnym, które są tworzone za pomocą narzędzi, takich jak MakeCert.exe.
* Można użyć certyfikatu z podpisem własnym, ale powinien tylko zrobić dla klastrów testowych, a nie w środowisku produkcyjnym.

### <a name="server-x509-certificates"></a>Certyfikaty X.509 serwera
Certyfikaty serwera zostały hello zadań podstawowego uwierzytelniania tooclients serwer (węzeł) lub uwierzytelniania serwera (węzeł) server tooa (węzeł). Jednym z hello wstępne kontrole kiedy klienta lub węzeł uwierzytelnia węzła jest wartość hello toocheck hello wspólnej nazwy w polu podmiotu hello. Ta nazwa pospolita lub jedną z alternatywnych nazw podmiotu certyfikatów hello musi występować w hello lista dozwolonych nazw pospolitych.

Witaj następujący artykuł w tym artykule opisano sposób toogenerate certyfikaty z alternatywnych nazw podmiotu (SAN): [jak LDAP certyfikat protokołu secure tooadd tooa alternatywnej nazwy podmiotu](http://support.microsoft.com/kb/931351).

pole tematu Hello może zawierać kilka wartości, prefiksem każdego typu wartości hello tooindicate inicjowania. Najczęściej inicjowania hello jest "CN" dla nazwy pospolitej; na przykład "CN = www.contoso.com". Istnieje również możliwość toobe pole podmiotu hello puste. Jeśli zostanie wypełnione pole alternatywna nazwa podmiotu opcjonalne hello, musi ona zawierać zarówno hello nazwa pospolita certyfikatu hello i jednego wpisu na alternatywnej nazwy podmiotu. Te są wprowadzane jako wartości nazwy DNS.

wartość Hello hello zamierzone cele pole certyfikatu hello powinna zawierać odpowiednią wartość, takie jak "Uwierzytelnianie serwera" lub "Uwierzytelnienie klienta".

### <a name="client-x509-certificates"></a>Certyfikaty X.509 klienta
Certyfikaty klienta nie są zwykle wystawiony przez urząd certyfikacji innych firm. Zamiast tego hello magazynie osobistym hello bieżącej lokalizacji użytkownika zwykle zawiera certyfikaty klienta, umieszczone w nim przez urząd główny z przeznaczeniem "Uwierzytelnienie klienta". Hello klient może używać takich certyfikatów, gdy jest wymagane uwierzytelnianie wzajemne.

> [!NOTE]
> Wszystkie operacje zarządzania w klastrze usługi sieć szkieletowa usług wymagają certyfikatów serwera. Nie można używać certyfikatów klienta do zarządzania.
> 
> 

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->


## <a name="next-steps"></a>Następne kroki
Ten artykuł zawiera informacje o pojęciach dotyczących zabezpieczeń klastra. Następnie


1.  [Tworzenie klastra na platformie Azure przy użyciu szablonu usługi Resource Manager](service-fabric-cluster-creation-via-arm.md) 
2.  [Azure portal](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
