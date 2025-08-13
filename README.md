# 🚀 Documento para Deploy do sistema Gestão de Escala e Permutas  

**📅 Versão:** 1.0  
**📅 Data:** 13 de Agosto de 2025  
**🏢 Aplicação:** Sistema para gerenciamento de escalas e permutas na Prefeitura de Maricá  

---

## 📋 Visão Geral  
Solução baseada em contêineres Docker composta por:  
- **Backend (API .NET)** → Lógica de negócio e integrações.  
- **Frontend Web** → Interface para desktop.  
- **Frontend Mobile (Flutter Web)** → Interface otimizada para dispositivos móveis.  

---

## 🏗️ Arquitetura  

### 🔧 Componentes  
| Componente               | Descrição                                                                 | Artefato           |
|--------------------------|---------------------------------------------------------------------------|--------------------|
| **Backend (API)**        | Serviço .NET com lógica de negócio, validações e comunicação com banco.  | `backend-app.tar`  |
| **Frontend Web**         | Interface para navegadores em desktop.                                    | `frontend-app.tar` |
| **Frontend Mobile**      | Aplicação Flutter Web para dispositivos móveis.                          | `mobile-app.tar`   |

### 🌐 Comunicação  
- **Frontends** devem ser configurados com a URL do Backend via variáveis de ambiente:  
  - Exemplo: `VITE_API_URL=http://IP_BACKEND:8080`  

---

## 🔒 Configurações Sensíveis  
**Dados sensíveis são injetados via variáveis de ambiente no Backend:**  

| Categoria         | Variáveis de Ambiente                          |
|-------------------|-----------------------------------------------|
| Banco de Dados    | `ConnectionStrings_EmUso`                     |
| Autenticação      | `JwtSettings_Secret`, `JwtSettings_ExpirationHours` |
| RabbitMQ          | `RabbitMQ_HostName`, `RabbitMQ_UserName`, etc. |
| Google reCAPTCHA  | `RecaptchaSettings_SiteKey`                   |

---

## 📌 Plano de Implantação (Checklist)  

| Ordem | Ação                     | Comando/Detalhes                                                                 | Status |
|-------|--------------------------|---------------------------------------------------------------------------------|--------|
| 1     | Receber Artefatos        | Confirmar recebimento dos arquivos `.tar` e documentação.                       | [ ]    |
| 2     | Carregar Imagens Docker  | ```docker load -i backend-app.tar``` <br> ```docker load -i frontend-app.tar```  | [ ]    |
| 3     | Executar Backend         | ```docker run -d --name gestao-backend -p 8080:8080 -e VARI=VALOR...```         | [ ]    |
| 4     | Validar Backend          | Verificar logs: ```docker logs gestao-backend```                                | [ ]    |
| 5     | Executar Frontend Web    | ```docker run -d --name gestao-frontend-web -p 80:80 -e VITE_API_URL="..."```    | [ ]    |
| 6     | Executar Frontend Mobile | ```docker run -d --name gestao-frontend-mobile -p 81:80 -e API_URL="..."```     | [ ]    |
| 7     | Validação Final          | Acessar URLs: `http://IP_SERVIDOR` (Web) e `http://IP_SERVIDOR:81` (Mobile)     | [ ]    |

---

## 📄 Documentação Completa  
Para detalhes técnicos adicionais, **veja o [Guia de Implantação clicando aqui](https://689ca68211f8f9008231d5c8--stately-rolypoly-fd7a95.netlify.app/)**.  

---

## 💬 Suporte  
Em caso de dúvidas, contate a **Equipe de TI da Defesa Civil de Maricá**.  

---
