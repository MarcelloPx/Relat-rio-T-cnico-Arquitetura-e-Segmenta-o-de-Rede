# 🛡️ Laboratório de Arquitetura e Segmentação de Rede

Um projeto prático de Segurança Cibernética focado em defesa em profundidade (Defense in Depth) e segmentação de rede corporativa.

## 🎯 Objetivo
Este repositório documenta a implementação de um ambiente laboratorial de rede corporativa. A infraestrutura foi projetada para garantir o isolamento entre ambientes de diferentes níveis de confiança (Zone-Based Topology), utilizando um firewall central e zonas desmilitarizadas (DMZs).

## 🛠️ Tecnologias e Ferramentas
* **Sistemas Operacionais:** Linux Debian 12 (Bookworm)
* **Firewall & Roteamento:** pfSense (v2.7.x)
* **WAF (Web Application Firewall):** Nginx (v1.24.x)
* **SIEM / Log Centralization:** Graylog (v5.x)
* **IDS/IPS:** Snort (v2.9.x)

---

## 🗺️ Topologia e Zonas de Segurança

O ambiente é gerenciado por um firewall pfSense central, atuando como único ponto de inspeção e roteamento. A rede foi segmentada da seguinte forma:

* 🌐 **WAN (Internet / em0):** Interface externa simulada (`192.168.15.100/24`).
* 💻 **LAN (Intranet / em2):** Rede interna de alta confiança (`192.168.1.1/24`).
* 🗄️ **DMZ Graylog (FIREWALL / em1):** Zona isolada dedicada ao servidor central de logs (`172.100.1.1/24`).
* 🛡️ **DMZEXT WAF (DMZEXT / em3):** Zona hospedando o Nginx como WAF para proteção de aplicações web (`172.100.2.1/24`).

---

## ⚙️ Principais Funcionalidades Implementadas

### 1. Roteamento e Regras Estritas (pfSense)
* Bloqueio padrão (*Default Deny*) em portas não essenciais.
* Port Forwarding (NAT) configurado para expor serviços web controlados através de IPs Virtuais (VIP).

### 2. Web Application Firewall (Nginx)
* Implantado na DMZ de borda para inspecionar requisições maliciosas.
* Configurado para redirecionar de forma contínua seus arquivos `access_log` e `error_log` para a central de monitoramento.

### 3. Centralização de Logs (Graylog)
* Recepção de eventos críticos do WAF via protocolo Syslog.
* Ingestão de logs do firewall e eventos de rede isolados em um servidor dedicado na DMZ.

### 4. Sistema de Detecção de Intrusão (Snort)
* Operando em modo Legacy para inspecionar pacotes que trafegam na interface WAN.
* Escrita de regras customizadas para alertas imediatos de varreduras ou tráfegos específicos (ex: pacotes ICMP).

---

## 👨‍💻 Sobre o Autor

**Marcello Paixão da Cruz**
Estudante de Defesa Cibernética focado em arquitetura segura e infraestrutura. Possuo um perfil proativo e forte raciocínio lógico, valorizando sempre o trabalho em grupo para a resolução de problemas complexos e simulações corporativas. Tenho experiência em implantação de topologias de rede avançadas, englobando configuração de firewalls, DHCP, DNS e análise de vulnerabilidades.

📍 São Paulo, SP
