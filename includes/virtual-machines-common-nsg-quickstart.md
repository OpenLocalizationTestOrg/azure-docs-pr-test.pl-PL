Otwarcie portu lub tworzenie punktu końcowego tooa maszyny wirtualnej (VM) na platformie Azure przez utworzenie filtru sieci w podsieci lub interfejsu sieciowego maszyny Wirtualnej. Te filtry, które kontrolują ruchu przychodzącego i wychodzącego, należy umieścić na zasób toohello dołączony sieciowej grupy zabezpieczeń, który odbiera ruch hello.

Użyjmy typowym przykładem ruchu w sieci web na porcie 80. Po utworzeniu maszyny Wirtualnej, który jest skonfigurowany tooserve żądań sieci web na powitania standardowy port TCP 80 (Pamiętaj toostart hello odpowiednie usługi i otworzyć reguł zapory systemu operacyjnego na powitania również maszyny Wirtualnej), możesz:

1. Utwórz grupę zabezpieczeń sieci.
2. Utwórz regułę ruchu przychodzącego zezwala na ruch z:
   * zakres portów docelowych Hello "80"
   * zakres portów źródłowych z Witaj "*" (dzięki czemu dowolnego portu źródłowego)
   * wartość priorytetu mniej 65,500 (toobe wyższy priorytet niż hello wychwytywania domyślne Odmów reguły dla ruchu przychodzącego)
3. Skojarz hello sieciową grupę zabezpieczeń z interfejsu sieciowego maszyny Wirtualnej hello lub podsieci.

Można utworzyć środowiska przy użyciu grup zabezpieczeń sieci i reguł toosecure konfiguracje złożoną siecią. Przedstawiony przykład używa tylko jedna lub dwie reguły zezwalające na ruch HTTP lub do zdalnego zarządzania. Aby uzyskać więcej informacji, zobacz następujące hello ["Więcej informacji"](#more-information-on-network-security-groups) sekcji lub [co to jest grupa zabezpieczeń sieci?](../articles/virtual-network/virtual-networks-nsg.md)

