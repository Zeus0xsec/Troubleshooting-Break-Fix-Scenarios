# SOC/Blue Team Home Lab – Active Directory i Troubleshooting

[![English](https://img.shields.io/badge/lang-EN-blue.svg)](README.md)

---

## Moduł 2: Active Directory, GPO i Troubleshooting DNS (Scenariusze Break-Fix)

W kolejnym etapie budowy mojego domowego labu SOC/Blue Team przeszedłem od czystego wdrożenia do praktycznych scenariuszy awaryjnych (Break-Fix). Zamiast idealnych konfiguracji, celowo wprowadzałem błędy i uczyłem się je diagnozować ze stacji roboczej, co pozwala realnie zrozumieć działanie systemów pod maską.


#### 1. GPO Hardening i Diagnozowanie Awarii
Wdrożono politykę GPO blokującą Wiersz polecenia (CMD) oraz Panel Sterowania dla użytkowników domeny.
* Break-Fix (Błędny link GPO): Symulacja pomyłki administratora – przypisanie polisy do złego OU. Diagnostyka poprawności nakładania zasad bezpośrednio na kliencie za pomocą narzędzi CLI.
* Filtrowanie Zabezpieczeń (Security Filtering): Skonfigurowano zaawansowane uprawnienia. Nadano regułę Odmów (Deny) na uprawnieniu Apply Group Policy dla grupy Domain Admins, dzięki czemu administratorzy zyskali "tarczę" chroniącą ich przed restrykcjami.

#### 2. Zarządzanie DNS oraz Metryki Interfejsów (Routing)
Utrzymanie stref wyszukiwania do przodu i wstecz na kontrolerze domeny (obsługa rekordów A, CNAME oraz PTR).
* Break-Fix (Utrata wzroku DNS): Wstrzyknięcie błędnego DNS-a na karcie klienta i diagnozowanie problemu za pomocą `ipconfig /flushdns` oraz `nslookup dc01.cyberlab.local`.
* Konflikt w środowisku wirtualnym (Dwie karty sieciowe): Klient posiadał NAT (Internet) oraz sieć wewnętrzną (AD). Windows faworyzował ruch z Internetu, odpytując domowy router o zasoby domeny.
* Rozwiązanie (Interface Metrics): Ręczna zmiana priorytetów trasowania protokołu IPv4. Nadano wyższy priorytet (metryka 10) karcie wewnętrznej i niższy (metryka 100) karcie NAT. Uzyskano stabilną sieć domeny i pełny dostęp do Internetu jednocześnie.
