# 🛡️ SOC/Blue Team Home Lab – Active Directory & Troubleshooting

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

---

#### Moduł 2: Active Directory, GPO i Troubleshooting DNS (Scenariusze Break-Fix)

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

## 📸 Screeny
<img width="941" height="633" alt="1" src="https://github.com/user-attachments/assets/b73f77bf-7f12-4da6-b391-c7c56f542eda" />

<img width="659" height="587" alt="2" src="https://github.com/user-attachments/assets/cce36dec-8ef2-4326-a93b-5eec7001c29c" />

<img width="779" height="563" alt="3" src="https://github.com/user-attachments/assets/cbe9bdf0-b76d-4795-87be-407f76de6424" />
