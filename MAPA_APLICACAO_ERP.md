# MAPA DA APLICAÇÃO ERP - BARRACAS DE COMIDA DE RUA

## 📋 VISÃO GERAL DO SISTEMA

```
┌─────────────────────────────────────────────────────────────────┐
│                    SISTEMA ERP FOODRP                           │
│                 Barracas de Comida de Rua                       │
└─────────────────────────────────────────────────────────────────┘
```

## 🏗️ ARQUITETURA PRINCIPAL

### Frontend (Interface do Usuário)
```
┌─────────────────────────────────────────────────────────────────┐
│                        FRONTEND                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │   LOGIN     │  │  DASHBOARD  │  │   PDV       │              │
│  │             │  │             │  │             │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │  ESTOQUE    │  │ FINANCEIRO  │  │  RECEITAS   │              │
│  │             │  │             │  │             │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │ RELATÓRIOS  │  │CONFIGURAÇÕES│  │   AJUDA     │              │
│  │             │  │             │  │             │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
└─────────────────────────────────────────────────────────────────┘
```

### Backend (API e Lógica de Negócio)
```
┌─────────────────────────────────────────────────────────────────┐
│                        BACKEND                                  │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │   AUTH      │  │   SALES     │  │  INVENTORY  │              │
│  │             │  │             │  │             │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │ FINANCIAL   │  │  RECIPES    │  │  REPORTS    │              │
│  │             │  │             │  │             │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │  NOTIFY     │  │   CONFIG    │  │   UTILS     │              │
│  │             │  │             │  │             │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
└─────────────────────────────────────────────────────────────────┘
```

### Banco de Dados
```
┌─────────────────────────────────────────────────────────────────┐
│                      BANCO DE DADOS                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │   USERS     │  │   PRODUCTS  │  │  INVENTORY  │              │
│  │             │  │             │  │             │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │   SALES     │  │  RECIPES    │  │  EXPENSES   │              │
│  │             │  │             │  │             │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │ PAYMENTS    │  │  CATEGORIES │  │  SETTINGS   │              │
│  │             │  │             │  │             │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
└─────────────────────────────────────────────────────────────────┘
```

## 📱 MÓDULOS PRINCIPAIS

### 1. 🔐 MÓDULO DE AUTENTICAÇÃO
```
┌─────────────────────────────────────────────────────────────────┐
│                    AUTENTICAÇÃO                                 │
├─────────────────────────────────────────────────────────────────┤
│ • Login/Logout                                                  │
│ • Recuperação de Senha                                          │
│ • Gerenciamento de Sessão:                                     │
│   - Manter usuário logado por tempo determinado                │
│   - "Lembrar-me" para acesso rápido                            │
│   - Logout automático por inatividade                          │
│   - Sessão única (evitar múltiplos logins)                     │
│ • Controle de Acesso:                                          │
│   - Diferentes níveis de usuário (Admin, Operador)             │
│   - Permissões por módulo (vendas, estoque, relatórios)        │
│   - Bloqueio de funcionalidades por perfil                     │
│   - Auditoria de ações do usuário                              │
└─────────────────────────────────────────────────────────────────┘
```

#### 📋 **Explicação Detalhada das Funcionalidades de Autenticação:**

**🔐 Gerenciamento de Sessão:**
- **Manter usuário logado**: O sistema "lembra" que o usuário está autenticado por um período (ex: 8 horas de trabalho)
- **"Lembrar-me"**: Checkbox que permite manter o login ativo por mais tempo (ex: 30 dias) para acesso rápido
- **Logout automático por inatividade**: Se o usuário não usar o sistema por X minutos, faz logout automático por segurança
- **Sessão única**: Impede que o mesmo usuário faça login em múltiplos dispositivos simultaneamente

**🛡️ Controle de Acesso:**
- **Níveis de usuário**: 
  - **Admin**: Acesso total (configurações, relatórios, usuários)
  - **Operador**: Acesso limitado (apenas vendas e estoque básico)
- **Permissões por módulo**: Cada usuário pode ter acesso apenas aos módulos necessários
- **Bloqueio de funcionalidades**: Botões/menus ficam desabilitados se o usuário não tem permissão
- **Auditoria**: Registra todas as ações importantes (quem fez o quê e quando)

### 2. 📊 DASHBOARD PRINCIPAL
```
┌─────────────────────────────────────────────────────────────────┐
│                      DASHBOARD                                  │
├─────────────────────────────────────────────────────────────────┤
│ • Vendas do Dia (Total e por Produto)                           │
│ • Lucro Estimado                                                │
│ • Alertas de Estoque Baixo                                      │
│ • Atalhos Rápidos:                                              │
│   - Nova Venda                                                  │
│   - Adicionar Estoque                                           │
│   - Ver Relatórios                                              │
│ • Gráficos de Performance                                       │
└─────────────────────────────────────────────────────────────────┘
```

### 3. 🛒 MÓDULO PDV (PONTO DE VENDA)
```
┌─────────────────────────────────────────────────────────────────┐
│                        PDV                                      │
├─────────────────────────────────────────────────────────────────┤
│ • Interface de Venda com Botões Grandes                         │
│ • Seleção de Produtos:                                          │
│   - Churros (Doce de Leite, Chocolate, etc.)                    │
│   - Crepes (Salgado, Doce, etc.)                                │
│   - Cachorro Quente (Simples, Completo, etc.)                   │
│   - Bebidas (Refrigerante, Suco, etc.)                          │
│ • Carrinho Virtual                                              │
│ • Ajuste de Quantidade                                          │
│ • Formas de Pagamento:                                          │
│   - Dinheiro                                                    │
│   - Cartão (Crédito/Débito)                                     │
│   - PIX                                                         │
│ • Emissão de Recibo (SMS/WhatsApp/Impressão)                    │
│ • Fechamento de Caixa                                           │
└─────────────────────────────────────────────────────────────────┘
```

### 4. 📦 MÓDULO DE ESTOQUE
```
┌─────────────────────────────────────────────────────────────────┐
│                      ESTOQUE                                    │
├─────────────────────────────────────────────────────────────────┤
│ • Cadastro de Itens:                                            │
│   - Ingredientes (Massa, Salsicha, Pão, etc.)                   │
│   - Produtos Acabados                                           │
│ • Entrada de Estoque (Compras)                                  │
│ • Saída Automática (Vendas)                                     │
│ • Alertas de Estoque Baixo                                      │
│ • Inventário Físico                                             │
│ • Controle de Validade                                          │
│ • Cálculo de Custo Médio                                        │
└─────────────────────────────────────────────────────────────────┘
```

### 5. 💰 MÓDULO FINANCEIRO
```
┌─────────────────────────────────────────────────────────────────┐
│                    FINANCEIRO                                  │
├─────────────────────────────────────────────────────────────────┤
│ • Registro de Despesas:                                        │
│   - Compras de Insumos                                         │
│   - Aluguel da Barraca                                         │
│   - Manutenção                                                 │
│   - Gás e Energia                                              │
│ • Fluxo de Caixa:                                              │
│   - Diário                                                     │
│   - Semanal                                                    │
│   - Mensal                                                     │
│ • Relatório de Lucratividade                                   │
│ • Controle de Receitas vs Despesas                             │
└─────────────────────────────────────────────────────────────────┘
```

### 6. 👨‍🍳 MÓDULO DE RECEITAS
```
┌─────────────────────────────────────────────────────────────────┐
│                      RECEITAS                                  │
├─────────────────────────────────────────────────────────────────┤
│ • Cadastro de Receitas (Ficha Técnica):                        │
│   - Ingredientes e Quantidades                                 │
│   - Modo de Preparo                                            │
│   - Tempo de Preparo                                           │
│ • Cálculo de Custo por Porção                                  │
│ • Sugestão de Preço de Venda                                   │
│ • Margem de Lucro Configurável                                 │
│ • Versionamento de Receitas                                    │
└─────────────────────────────────────────────────────────────────┘
```

### 7. 📈 MÓDULO DE RELATÓRIOS
```
┌─────────────────────────────────────────────────────────────────┐
│                    RELATÓRIOS                                  │
├─────────────────────────────────────────────────────────────────┤
│ • Vendas por Período (Gráficos)                                │
│ • Produtos Mais Vendidos                                       │
│ • Despesas por Categoria                                       │
│ • Relatório de Lucratividade                                   │
│ • Análise de Performance                                       │
│ • Exportação (PDF, Excel)                                      │
└─────────────────────────────────────────────────────────────────┘
```

## 🔧 FUNCIONALIDADES TÉCNICAS

### Integrações
```
┌─────────────────────────────────────────────────────────────────┐
│                    INTEGRAÇÕES                                 │
├─────────────────────────────────────────────────────────────────┤
│ • Maquininha de Cartão (Bluetooth)                             │
│ • WhatsApp Business API                                         │
│ • SMS Gateway                                                   │
│ • Impressora Portátil                                           │
│ • Backup em Nuvem                                              │
└─────────────────────────────────────────────────────────────────┘
```

### Notificações
```
┌─────────────────────────────────────────────────────────────────┐
│                  NOTIFICAÇÕES                                  │
├─────────────────────────────────────────────────────────────────┤
│ • Estoque Baixo                                                │
│ • Produtos Próximos do Vencimento                              │
│ • Meta de Vendas Diária                                        │
│ • Lembretes de Tarefas                                         │
│ • Alertas de Sistema                                           │
└─────────────────────────────────────────────────────────────────┘
```

## 🎯 FLUXO PRINCIPAL DE USO

```
┌─────────────────────────────────────────────────────────────────┐
│                    FLUXO DE USO                                │
├─────────────────────────────────────────────────────────────────┤
│ 1. LOGIN → Dashboard                                           │
│ 2. Dashboard → PDV (Nova Venda)                               │
│ 3. PDV → Seleção de Produtos → Carrinho → Pagamento           │
│ 4. Venda → Baixa Automática no Estoque                        │
│ 5. Estoque Baixo → Alerta → Compra de Insumos                 │
│ 6. Fim do Dia → Fechamento de Caixa → Relatórios              │
└─────────────────────────────────────────────────────────────────┘
```

## 📱 RESPONSIVIDADE E ACESSIBILIDADE

```
┌─────────────────────────────────────────────────────────────────┐
│              RESPONSIVIDADE                                    │
├─────────────────────────────────────────────────────────────────┤
│ • Mobile First Design                                          │
│ • Botões Grandes para Touch                                    │
│ • Interface Limpa e Intuitiva                                  │
│ • Funcionamento Offline (Cache)                                │
│ • Sincronização Automática                                     │
└─────────────────────────────────────────────────────────────────┘
```

## 🛡️ SEGURANÇA E BACKUP

```
┌─────────────────────────────────────────────────────────────────┐
│                  SEGURANÇA                                     │
├─────────────────────────────────────────────────────────────────┤
│ • Autenticação Segura                                          │
│ • Criptografia de Dados                                        │
│ • Backup Automático                                            │
│ • Controle de Versão                                           │
│ • Logs de Auditoria                                            │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📋 RESUMO DOS BENEFÍCIOS

✅ **Agilidade**: Processo de venda rápido e intuitivo  
✅ **Controle**: Visão clara do estoque e finanças  
✅ **Lucratividade**: Precificação correta e economia  
✅ **Simplicidade**: Fácil de usar para qualquer pessoa  
✅ **Mobilidade**: Funciona em qualquer lugar, a qualquer hora  

---

*Este mapa serve como base para o desenvolvimento do sistema ERP FoodRP, focando nas necessidades específicas das barracas de comida de rua.*
